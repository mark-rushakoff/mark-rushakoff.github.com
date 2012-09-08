---
layout: post
title: "Use scss mixins to handle special cases indicated by ancestor elements"
date: 2012-09-07 20:44
comments: true
categories: scss, sass
---

I've been using [Sass's parent selector (`&`)](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#referencing_parent_selectors_) routinely for about a year now, mostly in situations where I'm adding extra qualifiers to the parent selector:

{% codeblock lang:sass %}
a {
  color: red;
  &.disabled {
    color: lightgray;
  }
  &:hover {
    text-decoration: underline;
  }
}
{% endcodeblock  %}

It wasn't until very recently that I learned the `&` operator wasn't a special "append the following qualifier to the parent selector" but rather just "the full parent selector."
This means you can "break out of nesting" like so:

{% codeblock lang:sass %}
p, em, strong {
  font-size: 12px;
  color: black;
  .disabled & {
    color: gray;
    font-style: italic;
  }
}
{% endcodeblock  %}

which is the same as writing:

{% codeblock lang:sass %}
p, em, strong {
  font-size: 12px;
  color: black;
}

.disabled {
  p, em, strong {
    color: gray;
    font-style: italic;
  }
}
{% endcodeblock  %}

Under most circumstances, I wouldn't recommend putting a selector before the `&` in Sass; but sometimes desperate measures are necessary.
Maybe you are supporting multiple browsers and one of them can't handle a particular feature.
You might start with CSS like:

{% codeblock lang:sass %}
.my-button {
  border-radius: 5px;
  height: 30px;
  width: 100px;
  background-color: blue;
}

body.border-radius-unsupported .my-button {
  background-image: url('img/rounded-blue-button.png');
}
{% endcodeblock  %}

You could rewrite this as

{% codeblock lang:sass %}
.my-button {
  border-radius: 5px;
  height: 30px;
  width: 100px;
  background-color: blue;
  body.border-radius-unsupported & {
    background-image: url('img/rounded-blue-button.png');
  }
}
{% endcodeblock  %}

It's ugly, but at least it leaves your .scss file a little less cluttered.
But if you have a large number of rounded buttons in different colors, you might want to write a mixin to handle this (and you might want to reconsider your design!):

{% codeblock lang:sass %}
@mixin no-border-radius {
  body.border-radius-unsupported & {
    @content;
  }
}

.my-button {
  border-radius: 5px;
  height: 30px;
  width: 100px;
  background-color: blue;
  @include no-border-radius {
    background-image: url('img/rounded-blue-button.png');
  }
}
{% endcodeblock %}

Although this is a bit of a contrived example, I hope you can use this approach to help ease the pain of dealing with difficult cross-browser incompatibilities.
