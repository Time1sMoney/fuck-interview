# HTML

## 什么是 SEO?它为什么对网站至关重要？

SEO 代表搜索引擎优化（Search Engine Optimization），是一种通过优化网站内容和结构，提高网站在搜索引擎结果中排名的方法。
SEO 对网站至关重要，因为搜索引擎是用户获取信息的主要途径之一，而排名靠前的网站往往会获得更多的点击量和流量。通过 SEO 优化，网站可以提高在搜索引擎中的可见性，吸引更多的访问者，从而增加品牌曝光、提升销售量或实现其他商业目标。SEO 可以帮助网站获得有针对性的流量，提高用户体验，增强网站的可持续发展能力。

## SEO 优化的关键点有哪些？开发中你采取了哪些措施来进行 SEO 优化？

1. title 标签。对页面点击率有直接影响，因为这是用户对网站页面的第一印象，而且也是爬虫重点的爬取对象，填写的文字要对网页内容有准确而简洁的描述，能够吸引用户点击，而且长度要适中。
2. meta 标签。使用 http-equiv 和 name 属性以及 OG 标签。
3. 使用语义化标签。例如 H1,header,article,footer,nav 等等，H1~H6 标签作用很大，并且一个页面尽量只有一个 H1 标签，不要断层使用。img 标签设置 alt 属性。
4. 添加 sitemap。站点地图一般是 xml 格式的文件，放在网站的根目录下，文件里包含了每个网页的链接（loc），更新时间（lastmod），权重（priority）等信息，权重从 0 到 1，依次递增，一般主页设为 1，然后其他按重要性递减。
5. 添加 robots 文件。robots.txt 是一个给爬虫下指令的文本文件，能让其合理地抓取网站内资源，而且可以将网站不重要的内容、模块等进行屏蔽，从而抓取更多有价值高质量的内容和网页，提高网站排名。
6. 合理使用内链和外链。
7. 使用数据结构化标记。这不能帮助提高排名，但是可以丰富搜索结果、获得知识面板、支持语义搜索、体现 E-A-T(谷歌算法的一部分)。
8. 使用面包屑导航。
9. 服务端渲染。因为爬虫不执行 js，只会爬取源码，像 React/Vue 等框架都是动态生成 DOM，可供爬虫分析的内容大大减少，使用 SSR 可以让爬虫获取完整的页面数据。注意： 避免使用 iframe，爬虫不会抓取它里面的内容。
10. 合理使用网站地址。
11. 提升网站性能。
12. 使用 https。
13. 提交站点收录。将站点地图提交搜索引擎，以便搜索引擎能够更快更及时地抓取和索引网站。

## script 标签的 defer 和 async 属性有什么区别？

defer 和 async 是用于控制脚本加载和执行顺序的两个属性，它们在浏览器解析和执行脚本时有一些区别：

**defer**：当浏览器遇到带有`defer`属性的脚本标签时，会继续解析文档，同时异步下载脚本文件。待文档解析完成后，按照在文档中出现的顺序依次执行带有`defer`属性的脚本。多个带有`defer`属性的脚本会按照它们在文档中出现的顺序依次执行，且会在`DOMContentLoaded`事件触发前完成执行。

**async**：带有`async`属性的脚本会在异步下载完成后立即执行，不会阻塞文档的解析。多个带有 async 属性的脚本之间的执行顺序是不确定的，可能会因为下载速度等因素而导致执行顺序不同。

总的来说，`defer`保证脚本按照在文档中的顺序执行，并在`DOMContentLoaded`事件触发前执行，而`async`则是在下载完成后立即执行，不保证执行顺序。

## 怎么理解语义化标签？

语义化标签是指在编写网页时使用具有明确含义的 HTML 标签来描述页面内容的结构，使页面结构更具有语义性和可读性。通过使用语义化标签，可以让搜索引擎更好地理解页面内容，提高网页在搜索结果中的排名；同时也有助于屏幕阅读器等辅助技术更好地解释页面内容，提升网站的可访问性。

## HTML 中`data-*`属性是什么？

::: tip MDN
`data-*`全局属性是一类被称为自定义数据属性的属性，它赋予我们在所有 HTML 元素上嵌入自定义数据属性的能力，并可以通过脚本在 HTML 与 DOM 表现之间进行专有数据的交换。
:::

自定义属性命名必须遵循以下规则：

1. 该名称不能以 xml 开头，无论这些字母是大写还是小写。

2. 该名称不能包含任何分号。

3. 该名称不能包含 `A` 至 `Z` 的大写字母。

通过自定义属性，我们可以在 HTML 中嵌入自定义数据，然后在 JavaScript 中通过元素对象的`getAttribute`方法或`dataset`属性来访问这些数据，也能在 CSS 中通过`attr`表达式访问。

::: code-group

``` html [自定义属性]
<div class="title" data-id="999">Hello!</div>
```

``` js [在JS中访问自定义属性]
const element = document.querySelector(".title")

const id_1 = element.getAttribute("data-id");

const id_2 = element.dataset.id;
```

``` css [在CSS中访问自定义属性]
.title:after {
  content: 'Data ID: ' attr(data-id);
  position: absolute;
  top: -22px;
  left: 10px;
  background: black;
  color: white;
  padding: 2px;
  border: 1px solid #eee;
  opacity: 0;
  transition: 0.5s opacity;
}
```

:::

::: warning
`attr()` 理论上能用于所有的 CSS 属性但目前支持的仅有伪元素的 `content` 属性，其他的属性和高级特性目前是实验性的。
:::
