---
published: true
layout: post
title: php+swoole即时聊天
category: swoole
tags:
  - php
  - swoole
time: 2016.11.04 15:12:00
excerpt: 使用PHP+Swoole实现的网页即时聊天工具：PHPWebIM

---

<div class="repository-meta js-details-container ">
<div class="repository-description">
<p>使用PHP+Swoole实现的网页即时聊天工具</p>
</div>
</div>
<ul class=" list-paddingleft-2">
<li>
<p>全异步非阻塞Server，可以同时支持数百万TCP连接在线</p>
</li>
<li>
<p>同时支持websocket+comet2种兼容协议，可用于所有种类的浏览器包括IE</p>
</li>
<li>
<p>拥有完整的UI界面</p>
</li>
<li>
<p>支持单聊/群聊/组聊等功能</p>
</li>
<li>
<p>支持发送表情</p>
</li>
<li>
<p>支持永久保存聊天记录</p>
</li>
<li>
<p>基于Server PUSH的即时内容更新，登录/登出/状态变更/消息等会内容即时更新</p>
<blockquote>
<p>最新的版本已经可以原生支持IE系列浏览器了，基于Http长连接</p>
</blockquote>
<h2 id="articleHeader0"><a aria-hidden="true" id="user-content-安装" class="anchor" href="https://github.com/matyhtf/PHPWebIM#%E5%AE%89%E8%A3%85"></a>安装</h2>
<p>swoole扩展</p>
<div class="highlight highlight-shell"><pre>pecl install swoole</pre></div>
<p>swoole框架</p>
<div class="highlight highlight-shell"><pre>composer install</pre></div>
<h2 id="articleHeader1"><a aria-hidden="true" id="user-content-运行" class="anchor" href="https://github.com/matyhtf/PHPWebIM#%E8%BF%90%E8%A1%8C"></a>运行</h2>
<p>将client目录配置到Nginx/Apache的虚拟主机目录中，使client/index.html可访问。修改client/config.js中，IP和端口为对应的配置。</p>
<div class="highlight highlight-shell"><pre>php webim_server.php</pre></div>
<h2 id="articleHeader2"><a aria-hidden="true" id="user-content-详细部署说明" class="anchor" href="https://github.com/matyhtf/PHPWebIM#%E8%AF%A6%E7%BB%86%E9%83%A8%E7%BD%B2%E8%AF%B4%E6%98%8E"></a>详细部署说明</h2>
<p><strong>1.安装composer(php依赖包工具)</strong></p>
<div class="highlight highlight-shell"><pre>curl -sS https://getcomposer.org/installer <span class="pl-k">|</span> php
mv composer.phar /usr/local/bin/composer</pre></div>
<p>注意：如果未将php解释器程序设置为环境变量PATH中，需要设置。因为composer文件第一行为#!/usr/bin/env php，并不能修改。更加详细的对composer说明：<a href="http://blog.csdn.net/zzulp/article/details/18981029">http://blog.csdn.net/zzulp/article/details/18981029</a></p>
<p><strong>2.composer install</strong></p>
<p>切换到PHPWebIM项目目录，执行指令composer install，如很慢则</p>
<div class="highlight highlight-shell"><pre>composer install --prefer-dist</pre></div>
<p>3.Ningx/Apache配置（这里未使用swoole_framework提供的Web AppServer）</p>
<p>nginx</p><pre class="brush:shell; toolbar: true; auto-links: false;">server
{
    listen       80;
    server_name  im.swoole.com;
    index index.shtml index.html index.htm index.php;
    root  /path/to/PHPWebIM/client;
    location ~ .*\.(php|php5)?$
    {
        fastcgi_pass  127.0.0.1:9000;
        fastcgi_index index.php;
        include fastcgi.conf;
    }
    access_log  /Library/WebServer/nginx/logs/im.swoole.com  access;
}</pre> <p></p>
<p>apache</p><pre class="brush:shell; toolbar: true; auto-links: false;">&lt;VirtualHost *:80&gt;
    DocumentRoot "path/to/PHPWebIM/client"
    ServerName im.swoole.com
    AddType application/x-httpd-php .php
    &lt;Directory /&gt;
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
        DirectoryIndex index.php
    &lt;/Directory&gt;
&lt;/VirtualHost&gt;</pre> <p></p>
<p>4.修改配置PHPWebIM/config.php</p><pre class="brush:php; toolbar: true; auto-links: false;">$config['server'] = array(
    //监听的HOST
    'host' =&gt; '0.0.0.0',
    //监听的端口
    'port' =&gt; '9503',
    //WebSocket的URL地址，供浏览器使用的
    'url' =&gt; 'ws://127.0.0.1:9503',
);</pre> <p></p>
<ul class="task-list">
<li>server.host server.port 项为WebIM服务器即WebSocket服务器的IP与端口，其他选择项根据具体情况修改</li>
<li>server.url对应的就是服务器IP或域名以及websocket服务的端口，这个就是提供给浏览器的WebSocket地址</li>
<li>webim.data_dir用于修改聊天记录存储的目录，必须有可写权限</li>
</ul>
<p><strong>5.启动WebSocket服务器</strong></p>
<div class="highlight highlight-shell"><pre>php PHPWebIM/webim_server.php</pre></div>
<p>IE浏览器不支持WebSocket，需要使用FlashWebSocket模拟，请修改flash_policy.php中对应的端口，然后启动flash_policy.php。</p>
<div class="highlight highlight-shell"><pre>php PHPWebIM/flash_policy.php</pre></div>
<p><strong>6.绑定host与访问聊天窗口（可选）</strong></p>
<p>如果URL直接使用IP:PORT，这里不需要设置。</p>
<div class="highlight highlight-shell"><pre>vi /etc/hosts</pre></div>
<p>增加</p>
<div class="highlight highlight-shell"><pre>127.0.0.1 im.swoole.com</pre></div>
<p>用浏览器打开：<a href="http://im.swoole.com/">http://im.swoole.com</a></p>
<h2 id="articleHeader3"><a aria-hidden="true" id="user-content-快速了解项目架构" class="anchor" href="https://github.com/matyhtf/PHPWebIM#%E5%BF%AB%E9%80%9F%E4%BA%86%E8%A7%A3%E9%A1%B9%E7%9B%AE%E6%9E%B6%E6%9E%84"></a>快速了解项目架构</h2>
<p>1.目录结构</p>
<pre><code class="hljs cpp">+ PHPWebIM
  |- webim_server.php <span class="hljs-comment">//WebSocket协议服务器</span>
  |- config.php <span class="hljs-comment">// swoole运行配置</span>
  |+ swoole.ini <span class="hljs-comment">// WebSocket协议实现配置</span>
  |+ client
    |+ <span class="hljs-keyword">static</span>
    |- config.js <span class="hljs-comment">// WebSocket client配置</span>
    |- index.html <span class="hljs-comment">// 登录界面</span>
    |- main.html <span class="hljs-comment">// 聊天室主界面</span>
  |+ data <span class="hljs-comment">// 运行数据</span>
  |+ <span class="hljs-built_in">log</span> <span class="hljs-comment">// swoole日志及WebIM日志</span>
  |+ src <span class="hljs-comment">// WebIM 类文件储存目录</span>
    |+ Store
      |- File.php <span class="hljs-comment">// 默认用内存tmpfs文件系统(linux /dev/shm)存放天着数据，如果不是linux请手动修改$shm_dir</span>
      |- Redis.php <span class="hljs-comment">// 将聊天数据存放到Redis</span>
    |- Server.php <span class="hljs-comment">// 继承实现WebSocket的类，完成某些业务功能</span>
  |+ vendor <span class="hljs-comment">// 依赖包目录</span></code></pre> <p>2.Socket Server与Socket Client通信数据格式</p>
<p>如：登录</p>
<p>Client发送数据</p>
<div class="highlight highlight-js"><pre>{<span class="pl-s1"><span class="pl-pds">"</span>cmd<span class="pl-pds">"</span></span><span class="pl-k">:</span><span class="pl-s1"><span class="pl-pds">"</span>login<span class="pl-pds">"</span></span>,<span class="pl-s1"><span class="pl-pds">"</span>name<span class="pl-pds">"</span></span><span class="pl-k">:</span><span class="pl-s1"><span class="pl-pds">"</span>xdy<span class="pl-pds">"</span></span>,<span class="pl-s1"><span class="pl-pds">"</span>avatar<span class="pl-pds">"</span></span><span class="pl-k">:</span><span class="pl-s1"><span class="pl-pds">"</span>http://tp3.sinaimg.cn/1586005914/50/5649388281/1<span class="pl-pds">"</span></span>}</pre></div>
<p>Server响应登录</p>
<div class="highlight highlight-js"><pre>{<span class="pl-s1"><span class="pl-pds">"</span>cmd<span class="pl-pds">"</span></span><span class="pl-k">:</span><span class="pl-s1"><span class="pl-pds">"</span>login<span class="pl-pds">"</span></span>, <span class="pl-s1"><span class="pl-pds">"</span>fd<span class="pl-pds">"</span></span><span class="pl-k">:</span> <span class="pl-s1"><span class="pl-pds">"</span>31<span class="pl-pds">"</span></span>, <span class="pl-s1"><span class="pl-pds">"</span>name<span class="pl-pds">"</span></span><span class="pl-k">:</span><span class="pl-s1"><span class="pl-pds">"</span>xdy<span class="pl-pds">"</span></span>,<span class="pl-s1"><span class="pl-pds">"</span>avatar<span class="pl-pds">"</span></span><span class="pl-k">:</span><span class="pl-s1"><span class="pl-pds">"</span>http://tp3.sinaimg.cn/1586005914/50/5649388281/1<span class="pl-pds">"</span></span>}</pre></div>
<p>可以看到cmd属性，client与server发送时数据都有指定，主要是用于client或者server的回调处理函数。</p>
<p>3.需要理清的几种协议或者服务的关系</p>
<p>http协议：超文本传输协议。单工通信，等着客户端请求之后响应。</p>
<p>WebSocket协议：是HTML5一种新的协议，它是实现了浏览器与服务器全双工通信。服务器端口与客户端都可以推拉数据。</p>
<p>Web服务器：此项目中可以用基于Swoole的App Server充当Web服务器，也可以用传统的nginx/apache作为web服务器</p>
<p>Socket服务器：此项目中浏览器的WebSocket客户端连接的服务器，swoole_framework中有实现WebSocket协议PHP版本的服务器。</p>
<p>WebSocket Client：实现html5的浏览器都支持WebSocket对象，如不支持此项目中有提供flash版本的实现。<span id="transmark" style="display: none; width: 0px; height: 0px;"></span></p>
<p></p>
</li>
</ul>