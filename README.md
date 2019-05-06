# Allover theme for Hugo

Black & white & red **all over**. A flat monochromatic theme with a splash of crimson. This was previously the theme for [my Hugo blog](https://davidyat.es). It supports posts and pages out of the box, is intended for use with tags only, and has some cool extras, including site search and a couple of shortcodes.

## Randomised taglines

These will appear in italics directly beneath the site title, with a different one appearing on each page, randomised every build. You can specify the taglines to choose from in the `descriptions` array in your `params`.

`config.toml`:
```
[params]
...
descriptions = [
		"A tagline",
		"Another tagline",
		"Yet another tagline",
]
...
```

## Site search

This theme includes a search page at `/search/` which implements [this gist by Eddie Web](https://gist.github.com/eddiewebb/735feb48f50f0ddd65ae5606a1cb41ae). Said gist uses [fuse.js](https://fusejs.io/), a light-weight fuzzy search library. To get it working, you'll need to do the following:

Add a JSON output to the index page in `config.toml`:

```
...
[outputs]
  home = ["HTML", "RSS", "JSON"]
```

Create the file `content/search.md`. It won't be rendered and only exists to make the `/search` path work.

```
---
title: "Search Results"
sitemap:
  priority : 0.1
layout: "search"
---

No content here will be rendered.
```

The rest of the gist is in the theme.

## Post images

Each post can have an optional image. This will be displayed to the right of the post excerpt on list pages and at the top of the post content on content pages.

You can prevent the second behaviour on an ad-hoc basis by adding the below line to your post's frontmatter. This is useful for when you want to have an image represent the post but actually appear somewhere specific in the text body rather than at the very top.

```
image_within = true
```

## Shortcodes

This theme includes a couple of neat shortcodes for non-standard formatting I use often.

### Hint boxes

Nice pale yellow inline hint boxes with a sans-serif font.

```
{{% hint-box-env %}}
Some tangential subject that's still too long/relevant to be relegated to a footnote.
{{% /hint-box-env %}}
```

Which looks like:

![]()

### Captions

Markdown-capable image captions, for if you don't want to use `{{< figure >}}`:

```
{{% caption "Figure 1: A cat" %}}
```

will be rendered as:

```
<div class="caption">Figure 1: A cat</div>
```

## Custom excerpts

The partial `post-list-item.html` generates its own post summary/excerpts by taking the first 90 characters of the post content and removing elements that don't look right without formatting. This worked reasonably well for me when I was using this theme, but it's not fool-proof or comprehensive, so you may prefer to replace it with Hugo's built-in `.Summary`.

The code in question:

```
{{ $firstninety := split .Content " " | first 90 }}
{{ $stripnewlines := replace (delimit $firstninety " ") "\n" "" }}
{{ $stripcaptions := replaceRE "<sup.*?>.*?</sup>" "" $stripnewlines }}
{{ $stripheadings := replaceRE "<h[1-6].*?>.*?</h[1-6]>" "" $stripcaptions }}
{{ $stripfootnotes := replaceRE "<div class=\"footnotes\">.*?</div>" "" $stripheadings }}
{{ $excerpt := $stripfootnotes | plainify | safeHTML }}
```
