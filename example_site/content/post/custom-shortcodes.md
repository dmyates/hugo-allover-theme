+++
date = 2019-05-07T20:16:18+02:00
title = "Custom Shortcodes"
draft = false
tags = ["shortcodes", "formatting"]
# image = "/images/201X/XX/"

+++

Allover comes with a couple of shortcodes that I find quite useful, and perhaps you will too.

# Captions

Markdown-capable image captions, for if you don't want to use `{{</* figure */>}}`:

![](/hugo-allover-theme/images/1890/01/i021.jpg)
{{% caption "This is a caption. It can `contain` **markdown**. However, it's forced italic through CSS." %}}

Because captions are independent of what they're captions, you can use them for codeblocks, video embeds, and anything else you want, not just images.

You can create create captions like this:

```
{{%/* caption "Caption text." */%}}
```

# Hint boxes

You can intersperse your text bodies with nice pale yellow inline "hint boxes" with a sans-serif font. These can be short notes...

{{% hint-box %}}
**Warning**: It is very dangerous to run with scissors.
{{% /hint-box %}}

...or long sidebars with their own complex formatting.

{{% hint-box %}}
These boxes can also be used for long sidebars. I generally use them for anything that's too important for a footnote but doesn't quite flow with the main text.

![](/hugo-allover-theme/images/1890/01/i022.jpg)
{{% caption "Shortcodes can be used in hint boxes." %}}

You can put any formatting in here. Footnotes[^1] can be used as long as you keep both the ref and actual note in the box. 

```python
print "Hello World!"
```

[^1]: Like this.
{{% /hint-box %}}

The syntax for hint boxes looks like this:

```
{{%/* hint-box */%}}
**Warning**: It is very dangerous to run with scissors.
{{%/* /hint-box */%}}
```
