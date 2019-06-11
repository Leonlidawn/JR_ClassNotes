Documentations:
https://developer.mozilla.org/en-US/docs/Learn
https://webplatform.github.io/docs/html/

    <!doctype html>
    <html lang="eng">
        <head>
        <meta charset="utf-8">
        
        <meta name ="keywords" content="science,education,culture,politics,ecnomics,relationships,entertainment,human">

        <meta name="description" content="Buy Books Online With Huge Discounts. We Make Buying Books Online Easier for Various Categories Such as College, Horror, Philosophy, Love Story & more." />

        <mata name="author" content="Leon">

        <title>Buy Books Online - Up to 70% Off Discounts on Books Online</title>

 
        </head>
    </html>

lang attribute是用来区分内容语言的，可被继承。

lang值的合集
http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry

关于如何选择lang 值 （它不是tag，谢谢。）
https://www.w3.org/International/questions/qa-choosing-language-tags

meta 的 description 有语序
meta 的 keyword 就是 keyword，用逗号区分


Bad Practices of Creating Meta Tags:

    Repeating primary keyword or related keywords multiple times (keyword stuffing)
    Not placing the main keyword in the beginning of title tag
    Exceeding the character count in the Title & Meta description tag
    Duplicate meta tags
    Using spaces and | symbol instead of using comma to separate keywords in meta tags
    Note: Make sure the title tag is not too short and not too long. Characters between 55-60 would be perfectly fine. You may use FREE online tools to check the character count.

more on how to use meta tag for SEO:
http://www.semcmd.com/seo-rumen/98/

title tag 很重要，它是browser上方显示的标题

content models
==
https://www.w3.org/TR/html5/dom.html#kinds-of-content
在html5之前只有inline 和 block 两种
现在有 
Metadata content：
setting up the presentation or behavior for the rest of the content.

Flow content:
content that are presented in the normal flow of document

Sectioning content:
defines the scope of the cotents in the document.

Heading content:
header of a section

Phrasing content:
text of the document. almost same as inline elements in html4.

Embedded content:
contents that imports other content into the document

Interactive content:
contents that involve interaction


html formatting
==
<pre>pre tag, it literally display the text here as it is, 
with no trimming of spaces or line breaks</pre>

<i>i tag, italic, just for visual presentation, no meaning for screen readers</i>

<em>em tag, emphasized text, this is logical tag</em>

<strong>strong tag, strongly emphasized</strong>

xhtml need tags to be closed, while html does not.
Therefore 《br》 can be written as 《br /》 with no harm.

<dt><b>dt tag</b></dt>
<dd>in dd tag</dd>

named character entity 
https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references
eg.
&copy
&trade
&amp

&nbsp is used if some texts should be treated as one word under line wrapping

img 的width height 在css设置优先度比html高:
    
- css上设置的权限高于直接在img上面设置。
- 固有尺寸：img图片的自身大小，如果html尺寸不设置，并且Css尺寸不设置，则展现资源图片的固有宽高。
- html尺寸：通过html设置height，width属性，且没有Css限制，则展现为html尺寸。
- Css尺寸：通过Css属性设置宽高，展现为Css属性设置的结果。

html有三套标签系统去帮助机器分析网站结构
ouliners 是html5特有的内容标识 标签，显示内容之间的关联性
non-sectional and sementic elements:除了div以外，其它划分页面的主要内容和次要内容,illustrates the meaning of the content, you are using semantics .

ARIA： 用attribute来辅助screen reader



html5 outliner/section elements
===
https://gsnedders.html5.org/outliner/


html5 sectional elements are not supported by many outlining algorithms yet. therefore just keep using headings for outlinning and html5 sectionning tags for sementic usage.

h1 h2 h3 h4 h5 h6:
headings are sectional tags which will be shown in the outline.

nav tag:
最好包裹一个list. it creates a new section in the web page. 主要indicate网页的主要内链接组。

article tag：
for stand alone element.   When article elements are nested, the inner article elements represent articles that are in principle related to the contents of the outer article. For instance, a blog entry on a site that accepts user-submitted comments could represent the comments as article elements nested within the article element for the blog entry.

section tag：
does not need to be stand alone, just a thematic grouping of a contant. it is usually used within an article tag. It is for documents explicit outlining usage, with headings in the section. it is not redundant of div tags.

aside tag:
related content that might be replaced in the near future.  Aside elements are related to other contents in its parent.


non-sectional elements:
===
- div tag:
for groupingo of nothing, better use other tags af there are tags that would represent the sementic meaning of the content.

sementic elements:
---

- header:
introductory and navigational aids content for its nearest ancestor sectioning content. 
eg.

    <header>
        <h1></h1>
        <nav></nav>
    </header>

- footer:
information about its section such as who wrote it, links to related documents, copyright data, and the link. 

- main:
identify the main content of the body. consists of content that is directly realted to or expands upon the central topic.

- figure:
The figure element represents a unit of content, optionally with a caption, that is self-contained, that is typically referenced as a single unit from the main flow of the document, and that can be moved away from the main flow of the document without affecting the document’s meaning.
    - figure caption:
    The figcaption element represents a caption or legend for a figure.




WAI-ARIA (Accessible Rich Internet Application)
===
having roles attribute in the tag makes it more accessiblbe for screen readers(not all screen readers are based on the tag names, some are based on the role attributes).

https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles

To ensure download action of clicking a link,also put download attribute(html5) at the end, it is optional to provide a value as a name:
《a href="asfsaf" download="filenameabc"》resouce 《/a》
<a href="asfsaf" download="filenameabc"> resouce </a>

也可以用#代表跳到本页某id。就如href="#section1“
target="_blank" 常用来打开新页

Absolute links must have well formed URLs that include the protocol at the beginning.

The rel attribute describes the relationship of the target object to the linked object.

lists
=======
ul - unordered list
    li - list item
ol - ordered list
    li - list item
dl - discription/definition list, grouping of terms and descriptions
    dt - description/definition term
    dd - definition

