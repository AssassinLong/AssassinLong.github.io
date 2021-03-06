---
published: true
layout: post
title: github+jekyll搭建博客
category: jekyll
tags: 
  - jekyll
  - 引用
time: 2016.10.15 15:50:00
excerpt: 如何利用Github和Jekyll搭建一个博客.
---
<p>喜欢写博客的人，会经历三个阶段：</p>
<p>大多数人都停留在第一和第二个阶段，但是现在越来越多的人，主要是程序员喜欢在Github上写博客，一切都任由你左右，一个commit就能提交一篇文章，还有着无限流量免费的空间，想想就惬意不止。</p>
   第一阶段，刚接触Blog，觉得很新鲜，试着选择一个免费空间来写。
   第二阶段，发现免费空间限制太多，就自己购买域名和空间，搭建独立博客。
   第三阶段，觉得独立博客的管理太麻烦，最好在保留控制权的前提下，让别人来管，自己只负责写文章。
<p>进入正题，如何利用Github和Jekyll搭建一个博客：</p>
<h3>介绍</h3>

<p>　Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的</p>

<p>　使用 Jekyll 搭建博客之前要确认下本机环境，Git 环境（用于部署到远端）、<a href="http://www.ruby-lang.org/en/downloads/">Ruby</a> 环境（Jekyll 是基于 Ruby 开发的）、包管理器 <a href="http://rubygems.org/pages/download">RubyGems</a>              <br />
　　如果你是 Mac 用户，你就需要安装 Xcode 和 Command-Line Tools了。下载方式 Preferences → Downloads → Components。</p>

<p>　　Jekyll 是一个免费的简单静态网页生成工具，可以配合第三方服务例如： Disqus（评论）、多说(评论) 以及分享 等等扩展功能，Jekyll 可以直接部署在 Github（国外） 或 Coding（国内） 上，可以绑定自己的域名。<a href="http://jekyll.bootcss.com/">Jekyll中文文档</a>、<a href="https://jekyllrb.com/">Jekyll英文文档</a>、<a href="http://jekyllthemes.org/">Jekyll主题列表</a>。</p>

<h3 id="jekyll-">Jekyll 环境配置</h3>

<p>安装 jekyll</p>

 <code>$ gem install jekyll
</code>  

<p>创建博客</p>

 <code>$ jekyll new myBlog
</code>  

<p>进入博客目录</p>

 <code>$ cd myBlog
</code>  


<p>启动本地服务</p>

 <code>$ jekyll serve
</code>  


<p>在浏览器里输入： <a href="http://localhost:4000">http://localhost:4000</a>，就可以看到你的博客效果了。</p>

<p><img src="/assets/images/jekyll/image1.png" alt="" /></p>

<p>so easy !</p>

<h3 id="section-1">目录结构</h3>
<p>　
　Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是： 你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile,或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。</p>

<p>一个基本的 Jekyll 网站的目录结构一般是像这样的：</p>

<pre>
<code>
├── _config.yml
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   ├── post.html
|   └── page.html
├── _posts
|   └── 2016-10-08-welcome-to-jekyll.markdown
├── _sass
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md
├── css
|   └── main.scss
├── feed.xml
└── index.html
</code>
</pre>
<p>这些目录结构以及具体的作用可以参考 <a href="http://jekyll.com.cn/docs/structure/">官网文档</a></p>

<p>进入 _config.yml 里面，修改成你想看到的信息，重新 jekyll server ，刷新浏览器就可以看到你刚刚修改的信息了。</p>

<p>到此，博客初步搭建算是完成了，</p>

<h3 id="section-2">博客部署到远端</h3>

<p>　我这里讲的是部署到 Github Page 创建一个 github 账号，然后创建一个跟你账户名一样的仓库，如我的 github 账户名叫 <a href="https://github.com/leezhiy">leezhiy</a>，我的 github 仓库名就叫 <a href="https://github.com/leezhiy/leezhiy.github.io">leezhiy.github.io</a>，创建好了之后，把刚才建立的 myBlog 项目 push 到 username.github.io仓库里去（username指的是你的github用户名），检查你远端仓库已经跟你本地 myBlog 同步了，然后你在浏览器里输入 username.github.io ，就可以访问你的博客了。</p>

<h3 id="section-3">编写文章</h3>

<p>　　所有的文章都是 _posts 目录下面，文章格式为 mardown 格式，文章文件名可以是 .mardown 或者 .md。</p>

<p>　　编写一篇新文章很简单，你可以直接从 _posts/ 目录下复制一份出来 <code>2016-10-16-welcome-to-jekyll副本.markdown</code> ，修改名字为 2016-10-16-article1.markdown ，注意：文章名的格式前面必须为 2016-10-16- ，日期可以修改，但必须为 年-月-日- 格式，后面的 article1 是整个文章的连接 URL，如果文章名为中文，那么文章的连接URL就会变成这样的：http://baixin.io/2015/08/%E6%90%AD%E5/ ， 所以建议文章名最好是英文的或者阿拉伯数字。 双击 2016-10-16-article1.markdown 打开</p>

<code>
---
layout: post
title:  "Welcome to Jekyll!"
date:   2015-7-14 10:29:08 +0800
categories: jekyll update
---

正文...

</code>  
</div>

<p>title: 显示的文章名， 如：title: 我的第一篇文章                  <br />
date:  显示的文章发布日期，如：date: 2016-10-16                        <br />
categories: tag标签的分类，如：categories: 随笔</p>

<p>注意：文章头部格式必须为上面的，…. 就是文章的正文内容。</p>

<p>我写文章使用的是 Sublime Text2 编辑器，如果你对 markdown 语法不熟悉的话，可以看看<a href="https://www.zybuluo.com/">作业部落的教程</a></p>

<h3 id="section-4">使用我的博客模板</h3>

<p>虽然博客部署完成了，你会发现博客太简单不是你想要的，如果你喜欢我的模板的话，可以使用我的模板。</p>

<p>首先你要获取的我博客，<a href="https://AssassinLong.github.io">Github项目地址</a>，你可以直接<a href="https://github.com/AssassinLong/AssassinLong.github.io/archive/master.zip">点击下载博客</a>，进去AssassinLong.github.io/ 目录下， 使用命令部署本地服务</p>

 <code>$ jekyll server
</code>  


<h3>如果你本机没配置过任何jekyll的环境，可能会报错</h3>

 <pre><code>
 /Users/xxxxxxxx/.rvm/rubies/ruby-2.2.2/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in
  `require': cannot load such file -- bundler (LoadError)
from /Users/xxxxxxxx/.rvm/rubies/ruby-2.2.2/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in
`require'
from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/gems/jekyll-3.3.0/lib/jekyll/plugin_manager.rb:34:in
`require_from_bundler'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/gems/jekyll-3.3.0/exe/jekyll:9:in `&lt;top (required)&gt;'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/jekyll:23:in `load'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/jekyll:23:in `&lt;main&gt;'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/ruby_executable_hooks:15:in `eval'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/ruby_executable_hooks:15:in `&lt;main&gt;'

</code>
</pre>


<p>原因： 没有安装 bundler ，执行安装 bundler 命令</p>
<pre>
<code>
$ gem install bundler
</code>  
</pre>

<p>提示：</p>

<pre>
<code>
 Fetching: bundler-1.13.5.gem (100%)
Successfully installed bundler-1.13.5
Parsing documentation for bundler-1.13.5
Installing ri documentation for bundler-1.13.5
Done installing documentation for bundler after 5 seconds
1 gem installed
</code>  
</pre>

<p>再次执行 $ jekyll server  ，提示</p>

<pre>
<code>
Could not find proper version of jekyll (3.1.1) in any of the sources
Run `bundle install` to install missing gems.
</code>  
</pre>

<p>跟着提示运行命令</p>

 <code>$ bundle install
</code>  


<p>这个时候你可能会发现 bundle install 运行卡主不动了。</p>

<p>如果很长时间都没任何提示的话，你可以尝试修改 gem 的 source</p>

<pre>
<code>
$ gem sources --remove https://rubygems.org/
$ gem sources -a http://gems.ruby-china.org/
$ gem sources -l
*** CURRENT SOURCES ***
http://gems.ruby-china.org/
</code>
</pre>


<p>再次执行命令 $ bundle install，发现开始有动静了</p>

<pre>
<code>
Fetching gem metadata from http://gems.ruby-china.org/...........
Fetching version metadata from http://gems.ruby-china.org/..
Fetching dependency metadata from http://gems.ruby-china.org/.
。。。
Installing jekyll-watch 1.3.1
Installing jekyll 3.1.1
Bundle complete! 3 Gemfile dependencies, 17 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
</code>
</pre>


<p>bundler安装完成，后再次启动本地服务</p>

<code>$ jekyll server</code>


<p>继续报错</p>
<pre>
<code>
Configuration file: /Users/tendcloud-Caroline/Desktop/leopardpan.github.io/_config.yml
Dependency Error: Yikes! It looks like you don't have jekyll-sitemap or one of its dependencies installed. In order to use
Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file
-- jekyll-sitemap' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!
jekyll 3.1.1 | Error:  jekyll-sitemap
</code>
</pre>

<p>表示 当前的 jekyll 版本是 3.1.1 ，无法使用 jekyll-sitemap</p>

<p>解决方法有两个</p>

<blockquote>
  <p>1、打开当前目录下的 _config.yml 文件，把 gems: [jekyll-paginate,jekyll-sitemap] 换成 gems: [jekyll-paginate] ，也就是去掉jekyll-sitemap。</p>
</blockquote>

<blockquote>
  <p>2、升级 jekyll 版本，我当前的是 jekyll 3.1.2 。</p>
</blockquote>

<p>修改完成后保存配置，再次执行</p>

<code>$ jekyll server</code>

<p>提示</p>
<pre>
<code>
Configuration file: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_config.yml
            Source: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github
       Destination: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.901 seconds.
Auto-regeneration: enabled for '/Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github'
Configuration file: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
</code>
</pre>


<p>表示本地服务部署成功。</p>

<p>在浏览器输入 <a href="127.0.0.1:4000">127.0.0.1:4000</a> ， 就可以看到<a href="http://leezhiy.github.io">leezhiy.github.io</a>博客效果了。</p>

<h3 id="section-5">修改成你自己的博客</h3>

<blockquote>
  <ul>
    <li>如果你想使用我的模板请把 _posts/ 目录下的文章都去掉。</li>
    <li>修改 _config.yml 文件里面的内容为你自己的。</li>
  </ul>
</blockquote>

<p>然后使用 git push 到你自己的仓库里面去，检查你远端仓库，就会发现，你有一个漂亮的主题模板了。</p>

<h3 id="jekyll-1">为什么要是用 Jekyll</h3>

<p>使用了 Jekyll 你会发现如果你想使用多台电脑发博客都很方便，只要把远端 github 仓库里的博客 clone 下来，写文章后再提交就可以了</p>