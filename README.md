[简体中文](https://github.com/RuixiZhang42/font-pairing-guide)
/
[English](README-EN.md)

# 字体搭配指南

针对中文与西文的混合排版，本指南着重讨论以下三个需要注意的问题：

1. 中西文不同字体之间相对字号大小（relative font size）的调整；
2. 字重（weight）的搭配；
3. 中文汉字与西文字母、数字之间空白间距的设定。

本指南不涉及「哪种西文字体与中文字体搭配起来比较好看」这类「审美」的问题，而是侧重讨论上述三个「技术性」问题。

对于在这里讨论出来的排版思路，我们以「XeLaTeX 排版系统」为例，提供具体的实现方法。

---

<figure>
<img src="SVG/Example.svg" alt="Example">

<figcaption>
字号：思源宋体&nbsp;Heavy 42&#8239;bp，TeX Gyre Termes&nbsp;Bold 46.41&#8239;bp。<br />
行距：56&#8239;bp / 行间距：14&#8239;bp。&zwj;<sup>&ast;</sup>
</figcaption>

</figure>

<sup>&ast;</sup>在 TeX 中，1&#8239;bp&nbsp;= 1&frasl;72&#8239;in&nbsp;≈ 0.35278&#8239;mm——即
Adobe 软件与 Microsoft Office 中的「1&nbsp;磅」, 而
1&#8239;pt&nbsp;= 100&frasl;7227&#8239;in&nbsp;≈ 0.35146&#8239;mm。

---

## 相对字号大小的调整

我们先来看看下面这段话：

<figure>
<img src="SVG/Example-1-1.svg" alt="Example 1.1">

<figcaption>
字号：思源宋体&nbsp;Regular 16&#8239;bp，STIX&nbsp;Regular 16&#8239;bp。
</figcaption>

</figure>

不难看出，当我们读到「typography」、「τύπος」这些西文单词时，会有一种「西文矮了一截、就像掉下去了」的感觉。为了解决这个「搭配不协调」的问题，我们可以从西文字母的形状出发，探讨解决方法。

<figure>
<img src="SVG/Example-1-2.svg" alt="Example 1.2">
</figure>

因为西文的大写字母「等高」与汉字相似，所以我们可以将**大写字母的中线与汉字的中线对齐**，以此作为指导。

<figure>
<img src="SVG/Example-1-3.svg" alt="Example 1.3">

<figcaption>
上图：通过「<strong>上调西文的基线</strong>」来对齐大写字母与汉字的中线；<br />
下图：通过「<strong>放大西文的字号</strong>」来对齐大写字母与汉字的中线。
</figcaption>

</figure>

事实上，由奥村晴彦开发的 [jsclasses](https://ctan.org/pkg/jsclasses) 文档类就搭配了
13&#8239;Q（3.25&#8239;mm）的日文与
10&#8239;pt（3.5146&#8239;mm）的西文，这意味着西文字号大约是日文字号的
1.08&nbsp;倍。在直排时，jsclasses 会使用 [pLaTeX2e](https://ctan.org/pkg/platex)
提供的 `\adjustbaseline` 机制，对齐大写字母「M」与汉字的中线。

当然了，排版里讲究的是「视觉对齐」而非「数学严格对齐」。