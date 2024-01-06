---
title : 'My First Post'
slug : beginning
date : 2024-01-04T22:05:04+08:00
draft : false
tags : ['备忘']
---

## How to use

- `title`：页面标题
- `slug`：slug 是 URL 的一部分，它以易于阅读的形式标识网站上的特定页面。
- `date`：页面的创建日期。
- `draft`：如果要取消发布页面。
- `featuredImg`：为页面提供唯一的图像，显示为背景图像。可以使用菜单中的特殊按钮切换到全屏。
- `description`：页面的说明。
- `tags`：允许定义标签。
- `categories`：允许定义类别。
- `author`：允许指定页面作者。
- `authorLink`：允许提供单独的作者简介。
- `scrolltotop`：该页的滚动到顶部按钮。
- `mathjax`：启用每页 MathJax 支持。
- `toc`：启用目录。
- `custom_css`：允许通过将 css 文件放在 中来提供自定义 CSS。CSS 将仅针对该页面调用。`/static/css/`
- `custom_js`：允许通过将 css 文件放在 中来提供自定义 CSS。JS 将仅针对该页面调用。`/static/js/`
- `ShowLastmod`：这将启用给定页面的上次修改日期。
- `Lastmod`：在`ShowLastmod=true`时，输入页面的上次修改日期。

> If `ShowLastmod:true` :
>
> - If `enableGitInfo = true`, then Git Hash will be shown in `[...]` after Date.
>
> - If `enableGitInfo = false`, then:
>
>   - If `Lastmod` is not provided or `Lastmod` has same value as `Date`, error will be thrown.
>   - If `Lastmod` is provided or `Lastmod` is different from `Date`, value of `Lastmod` will be displayed in `[...]` after Date.
>
> If `ShowLastmod` is not provided. User response defaults to false. It is equivalent to providing `ShowLastmod:false`.

## Latex

LaTeX 是通过 Mathjax 实现的。

- 如果您将此主题用作适当的数学博客，请在 hugo.toml 中启用 true。它将在站点范围内启用 Mathjax 支持。`global_mathjax`
- 由于 Mathjax 是一个繁重的脚本 （>1 MB），因此在站点范围内运行 Mathjax 并不理想，特别是如果您属于上述队列。但是，如果要使用数学公式，可以在 Page frontmatter 中设置。它将仅为该页面启用 mathjax。`mathjax : true`

## Banner

{{< admonition type=note title="This is a note" >}}
A **note** banner
{{< /admonition >}}

{{< admonition info "This is an info" >}}
A **info** banner
{{< /admonition >}}

{{< admonition tip >}}
A **tip** banner
{{< /admonition >}}

{{< admonition success >}}
A **success** banner
{{< /admonition >}}

{{< admonition warning >}}
A **warning** banner
{{< /admonition >}}

{{< admonition failure >}}
A **failure** banner
{{< /admonition >}}

{{< admonition danger >}}
A **danger** banner
{{< /admonition >}}

{{< admonition bug >}}
A **bug** banner
{{< /admonition >}}

```markdown
{{</* admonition type=tip title="This is a tip" */>}}
A **tip** banner
{{</* /admonition */>}}
Or
{{</* admonition tip "This is a tip" */>}}
A **tip** banner
{{</* /admonition */>}}
```

## image

image at left
{{< figure src="https://placehold.co/400x280" alt="image" caption="figure-left" class="left" >}}

big image
{{< figure src="https://placehold.co/1600x800" alt="image" caption="figure-big" class="big" >}}