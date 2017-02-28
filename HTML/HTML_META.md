&lt;div class="show-content"&gt;

&lt;p&gt;之前学习前端中，对meta标签的了解仅仅只是这一句。&lt;/p&gt;

&lt;pre class="hljs xml"&gt;&lt;code class="xml"&gt;&lt;span class="hljs-tag"&gt;&lt;&lt;span class="hljs-name"&gt;meta&lt;/span&gt; &lt;span class="hljs-attr"&gt;charset&lt;/span&gt;=&lt;span class="hljs-string"&gt;"UTF-8"&lt;/span&gt;&gt;&lt;/span&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;但是打开任意的网站，其head标签内都有一列的meta标签。比如我博客的。&lt;br&gt;&lt;/p&gt;&lt;div class="image-package"&gt;

&lt;img src="https://segmentfault.com/image?src=http://7xoxxe.com1.z0.glb.clouddn.com/metas.jpg&amp;objectId=1190000004279791&amp;token=8eeeda626b04ac54d607ce4be3fc432a" data-original-src="https://segmentfault.com/image?src=http://7xoxxe.com1.z0.glb.clouddn.com/metas.jpg&amp;objectId=1190000004279791&amp;token=8eeeda626b04ac54d607ce4be3fc432a" style="cursor: zoom-in;"&gt;&lt;br&gt;&lt;div class="image-caption"&gt;&lt;/div&gt;

&lt;/div&gt;&lt;p&gt;&lt;br&gt;但是自己却很不熟悉，于是把meta标签加入了寒假学习计划的最前方。&lt;/p&gt;

&lt;h1&gt;简介&lt;/h1&gt;

&lt;hr&gt;

&lt;p&gt; 在查阅w3school中，第一句话中的“元数据”就让我开始了Google之旅。然后很顺利的在英文版的w3school找到了想要的结果。（中文w3school说的是元信息，Google和百度都没有相关的词条。但元数据在Google就有详细解释。所以这儿采用英文版W3school的解释。）&lt;/p&gt;

&lt;blockquote&gt;&lt;p&gt;The &lt;meta&gt; tag provides metadata about the HTML document. Metadata will not be displayed on the page, but will be machine parsable.&lt;/p&gt;&lt;/blockquote&gt;

&lt;p&gt;不难看出，其中的关键是metadata，中文名叫元数据，是用于描述数据的数据。它不会显示在页面上，但是机器却可以识别。这么一来meta标签的作用方式就很好理解了。&lt;/p&gt;

&lt;h1&gt;用处&lt;/h1&gt;

&lt;hr&gt;

&lt;blockquote&gt;&lt;p&gt;Meta elements are typically used to specify page description, keywords, author of the document, last modified, and other metadata.&lt;/p&gt;&lt;/blockquote&gt;

&lt;p&gt;The metadata can be used by browsers \(how to display content or reload page\), search engines \(keywords\), or other web services&lt;br&gt;这句话对meta标签用处的介绍，简洁明了。翻译过来就是：meta常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页面），搜索引擎和其它网络服务。&lt;/p&gt;

&lt;h1&gt;组成&lt;/h1&gt;

&lt;hr&gt;

&lt;p&gt;meta标签共有两个属性，分别是http-equiv属性和name属性。&lt;/p&gt;

&lt;h3&gt;1. name属性&lt;/h3&gt;

&lt;p&gt;name属性主要用于描述网页，比如网页的关键词，叙述等。与之对应的属性值为content，content中的内容是对name填入类型的具体描述，便于搜索引擎抓取。meta标签中name属性语法格式是：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"参数"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"具体的描述"&lt;/span&gt;&gt;。&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;其中name属性共有以下几种参数。&lt;strong&gt;\(A-C为常用属性\)&lt;/strong&gt;&lt;/p&gt;

&lt;h3&gt;A. keywords\(关键字\)&lt;/h3&gt;

&lt;p&gt;说明：用于告诉搜索引擎，你网页的关键字。举例：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"keywords"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"Lxxyx,博客，文科生，前端"&lt;/span&gt;&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;B. description\(网站内容的描述\)&lt;/h3&gt;

&lt;p&gt;说明：用于告诉搜索引擎，你网站的主要内容。举例：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"description"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"文科生，热爱前端与编程。目前大二，这是我的前端博客"&lt;/span&gt;&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;C. viewport\(移动端的窗口\)&lt;/h3&gt;

&lt;p&gt;说明：这个概念较为复杂，具体的会在下篇博文中讲述。这个属性常用于设计移动端网页。在用bootstrap,AmazeUI等框架时候都有用过viewport。&lt;br&gt;举例（常用范例）：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"viewport"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"width=device-width, initial-scale=1"&lt;/span&gt;&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;D. robots\(定义搜索引擎爬虫的索引方式\)&lt;/h3&gt;

&lt;p&gt;说明：robots用来告诉爬虫哪些页面需要索引，哪些页面不需要索引。content的参数有all,none,index,noindex,follow,nofollow。默认是all。&lt;br&gt;举例：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"robots"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"none"&lt;/span&gt;&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;具体参数如下：&lt;br&gt;1.none : 搜索引擎将忽略此网页，等价于noindex，nofollow。2.noindex : 搜索引擎不索引此网页。&lt;br&gt;3.nofollow: 搜索引擎不继续通过此网页的链接索引搜索其它的网页。&lt;br&gt;4.all : 搜索引擎将索引此网页与继续通过此网页的链接索引，等价于index，follow。&lt;br&gt;5.index : 搜索引擎索引此网页。&lt;br&gt;6.follow : 搜索引擎继续通过此网页的链接索引搜索其它的网页。&lt;/p&gt;

&lt;h3&gt;E. author\(作者\)&lt;/h3&gt;

&lt;p&gt;说明：用于标注网页作者举例：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"author"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"Lxxyx,841380530@qq.com"&lt;/span&gt;&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;F. generator\(网页制作软件\)&lt;/h3&gt;

&lt;p&gt;说明：用于标明网页是什么软件做的举例: \(不知道能不能这样写\)：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"generator"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"Sublime Text3"&lt;/span&gt;&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;G. copyright\(版权\)&lt;/h3&gt;

&lt;p&gt;说明：用于标注版权信息举例：&lt;/p&gt;

&lt;pre class="hljs q"&gt;&lt;code class="q"&gt;&lt;&lt;span class="hljs-built\_in"&gt;meta&lt;/span&gt; name=&lt;span class="hljs-string"&gt;"copyright"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"Lxxyx"&lt;/span&gt;&gt; &lt;span class="hljs-comment"&gt;//代表该网站为Lxxyx个人版权所有。&lt;/span&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;H. revisit-after\(搜索引擎爬虫重访时间\)&lt;/h3&gt;

&lt;p&gt;说明：如果页面不是经常更新，为了减轻搜索引擎爬虫对服务器带来的压力，可以设置一个爬虫的重访时间。如果重访时间过短，爬虫将按它们定义的默认时间来访问。举例：&lt;/p&gt;

&lt;pre class="hljs applescript"&gt;&lt;code class="applescript"&gt;&lt;meta &lt;span class="hljs-built\_in"&gt;name&lt;/span&gt;=&lt;span class="hljs-string"&gt;"revisit-after"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"7 days"&lt;/span&gt; &gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;I. renderer\(双核浏览器渲染方式\)&lt;/h3&gt;

&lt;p&gt;说明：renderer是为双核浏览器准备的，用于指定双核浏览器默认以何种方式渲染页面。比如说360浏览器。举例：&lt;/p&gt;

&lt;pre class="hljs q"&gt;&lt;code class="q"&gt;&lt;&lt;span class="hljs-built\_in"&gt;meta&lt;/span&gt; name=&lt;span class="hljs-string"&gt;"renderer"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"webkit"&lt;/span&gt;&gt; &lt;span class="hljs-comment"&gt;//默认webkit内核&lt;/span&gt;

&lt;&lt;span class="hljs-built\_in"&gt;meta&lt;/span&gt; name=&lt;span class="hljs-string"&gt;"renderer"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"ie-comp"&lt;/span&gt;&gt; &lt;span class="hljs-comment"&gt;//默认IE兼容模式&lt;/span&gt;

&lt;&lt;span class="hljs-built\_in"&gt;meta&lt;/span&gt; name=&lt;span class="hljs-string"&gt;"renderer"&lt;/span&gt; content=&lt;span class="hljs-string"&gt;"ie-stand"&lt;/span&gt;&gt; &lt;span class="hljs-comment"&gt;//默认IE标准模式&lt;/span&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;2. http-equiv属性&lt;/h3&gt;

&lt;p&gt;介绍之前，先说个小插曲。看文档和博客关于http-equiv的介绍时，有这么一句。&lt;/p&gt;

&lt;pre class="hljs livecodeserver"&gt;&lt;code class="livecodeserver"&gt;&lt;span class="hljs-keyword"&gt;http&lt;/span&gt;-equiv顾名思义，相当于&lt;span class="hljs-keyword"&gt;http&lt;/span&gt;的文件头作用。&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;一开始看到这句话的时候，我是迷糊的。因为我看各类技术名词，都会习惯性的去记住它的英文全称。equiv的全称是"equivalent"，意思是相等，相当于。然后我脑子里出现了大大的迷惑：“HTTP相等？”&lt;br&gt;后来还准备去Segmentfault提问来着。结果在写问题的时候，突然反应出equivalent还有相当于的意思。意思就是相当于http的作用。至于文件头是哪儿出来的，估计是从其作用来分析的。我认为顾名思义并不能得出"相当于http的文件头作用"这个论断。&lt;br&gt;这个我所认为的http-equiv意思的简介。&lt;br&gt;&lt;code&gt;相当于HTTP的作用，比如说定义些HTTP参数啥的。&lt;/code&gt;&lt;/p&gt;

&lt;p&gt;meta标签中http-equiv属性语法格式是：&lt;/p&gt;

&lt;pre class="hljs xml"&gt;&lt;code class="xml"&gt;&lt;span class="hljs-tag"&gt;&lt;&lt;span class="hljs-name"&gt;meta&lt;/span&gt; &lt;span class="hljs-attr"&gt;http-equiv&lt;/span&gt;=&lt;span class="hljs-string"&gt;"参数"&lt;/span&gt; &lt;span class="hljs-attr"&gt;content&lt;/span&gt;=&lt;span class="hljs-string"&gt;"具体的描述"&lt;/span&gt;&gt;&lt;/span&gt;&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;其中http-equiv属性主要有以下几种参数：&lt;/p&gt;

&lt;h3&gt;A. content-Type\(设定网页字符集\)\(推荐使用HTML5的方式\)&lt;/h3&gt;

&lt;p&gt;说明：用于设定网页字符集，便于浏览器解析与渲染页面举例：&lt;/p&gt;

&lt;pre class="hljs xml"&gt;&lt;code class="xml"&gt;&lt;span class="hljs-tag"&gt;&lt;&lt;span class="hljs-name"&gt;meta&lt;/span&gt; &lt;span class="hljs-attr"&gt;http-equiv&lt;/span&gt;=&lt;span class="hljs-string"&gt;"content-Type"&lt;/span&gt; &lt;span class="hljs-attr"&gt;content&lt;/span&gt;=&lt;span class="hljs-string"&gt;"text/html;charset=utf-8"&lt;/span&gt;&gt;&lt;/span&gt; //旧的HTML，不推荐&lt;span class="hljs-tag"&gt;&lt;&lt;span class="hljs-name"&gt;meta&lt;/span&gt; &lt;span class="hljs-attr"&gt;charset&lt;/span&gt;=&lt;span class="hljs-string"&gt;"utf-8"&lt;/span&gt;&gt;&lt;/span&gt; //HTML5设定网页字符集的方式，推荐使用UTF-8&lt;/code&gt;&lt;/pre&gt;

&lt;h3&gt;B. X-UA-Compatible\(浏览器采取何种版本渲染当前页面\)&lt;/h3&gt;

&lt;p&gt;说明：用于告知浏览器以何种版本来渲染页面。（一般都设置为最新模式，在各大框架中这个设置也很常见。）举例：&lt;br&gt;\`\`\`&lt;meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/&gt; //指定IE和Chrome使用最新版本渲染当前页面&lt;/p&gt;

&lt;pre class="hljs awk"&gt;&lt;code class="awk"&gt;&lt;span class="hljs-comment"&gt;\#\#\# C. cache-control\(指定请求和响应遵循的缓存机制\)&lt;/span&gt;

用法&lt;span class="hljs-number"&gt;1&lt;/span&gt;.

说明：指导浏览器如何缓存某个响应以及缓存多长时间。这一段内容我在网上找了很久，但都没有找到满意的。最后终于在Google Developers中发现了我想要的答案。



!\[\]\(https:&lt;span class="hljs-regexp"&gt;//&lt;/span&gt;segmentfault.com&lt;span class="hljs-regexp"&gt;/image?src=http:/&lt;/span&gt;&lt;span class="hljs-regexp"&gt;/7xoxxe.com1.z0.glb.clouddn.com/&lt;/span&gt;cache.png&amp;objectId=&lt;span class="hljs-number"&gt;1190000004279791&lt;/span&gt;&amp;token=&lt;span class="hljs-number"&gt;60&lt;/span&gt;cc5b81792e199feb8a6b032aff4b83\)



举例:&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;&lt;meta http-equiv="cache-control" content="no-cache"&gt;&lt;/p&gt;

&lt;pre class="hljs markdown"&gt;&lt;code class="markdown"&gt;共有以下几种用法：

&lt;span class="hljs-bullet"&gt;1. &lt;/span&gt;no-cache: 先发送请求，与服务器确认该资源是否被更改，如果未被更改，则使用缓存。



&lt;span class="hljs-bullet"&gt;2. &lt;/span&gt;no-store: 不允许缓存，每次都要去服务器上，下载完整的响应。（安全措施）



&lt;span class="hljs-bullet"&gt;3. &lt;/span&gt;public : 缓存所有响应，但并非必须。因为max-age也可以做到相同效果



&lt;span class="hljs-bullet"&gt;4. &lt;/span&gt;private : 只为单个用户缓存，因此不允许任何中继进行缓存。（比如说CDN就不允许缓存private的响应）



&lt;span class="hljs-bullet"&gt;5. &lt;/span&gt;maxage : 表示当前请求开始，该响应在多久内能被缓存和重用，而不去服务器重新请求。例如：max-age=60表示响应可以再缓存和重用 60 秒。



&gt;\[&lt;span class="hljs-string"&gt;参考链接：HTTP缓存&lt;/span&gt;\]\(&lt;span class="hljs-link"&gt;https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=zh-cn\#cache-control&lt;/span&gt;\)



用法2.\(禁止百度自动转码\)

说明：用于禁止当前页面在移动端浏览时，被百度自动转码。虽然百度的本意是好的，但是转码效果很多时候却不尽人意。所以可以在head中加入例子中的那句话，就可以避免百度自动转码了。举例：&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;&lt;meta http-equiv="Cache-Control" content="no-siteapp" /&gt;&lt;/p&gt;

&lt;pre class="hljs clean"&gt;&lt;code class="clean"&gt;\#\#\# D. expires\(网页到期时间\)

说明:用于设定网页的到期时间，过期后网页必须到服务器上重新传输。举例：&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;&lt;meta http-equiv="expires" content="Sunday 26 October 2016 01:00 GMT" /&gt;&lt;/p&gt;

&lt;pre class="hljs clean"&gt;&lt;code class="clean"&gt;\#\#\#E. refresh\(自动刷新并指向某页面\)

说明：网页将在设定的时间内，自动刷新并调向设定的网址。举例:&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;&lt;meta http-equiv="refresh" content="2；URL=http://www.lxxyx.win/"&gt; //意思是2秒后跳转向我的博客&lt;/p&gt;

&lt;pre class="hljs clean"&gt;&lt;code class="clean"&gt;\#\#\# F. Set-Cookie\(cookie设定\)

说明：如果网页过期。那么这个网页存在本地的cookies也会被自动删除。&lt;/code&gt;&lt;/pre&gt;

&lt;p&gt;&lt;meta http-equiv="Set-Cookie" content="name, date"&gt; //格式&lt;/p&gt;

&lt;p&gt;&lt;meta http-equiv="Set-Cookie" content="User=Lxxyx; path=/; expires=Sunday, 10-Jan-16 10:00:00 GMT"&gt; //具体范例&lt;br&gt;\`\`\`&lt;/p&gt;

&lt;h1&gt;最后&lt;/h1&gt;

&lt;p&gt;暂时总结的就这么多了，meta标签的自定义属性实在太多了。所以只去找了常用的一些，还有像&lt;code&gt;Window-target&lt;/code&gt;&lt;br&gt;这样已经基本被废弃的属性，我也没有添加。一开始以为一两个小时就能学习完毕，结果没想到竟然花了五六个小时，各处查资料，推敲文字。敲击文字的时候，也感觉自己学习了非常多。比如基本的SEO，HTTP协议的再次理解等。&lt;br&gt;因为经验尚浅，所以如果有出错的地方，希望各位能帮忙指正。最后附上本人博客地址和原文链接，希望能与各位多多交流。&lt;/p&gt;

&lt;blockquote&gt;&lt;p&gt;转自 &lt;/p&gt;&lt;/blockquote&gt;



      

