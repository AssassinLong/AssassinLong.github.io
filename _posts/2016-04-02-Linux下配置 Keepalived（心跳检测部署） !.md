---
published: true
layout: post
title: Linux下配置 Keepalived（心跳检测部署） !
category: linux
tags:
  - linux
  - Keepalived
time: 2016.04.02 08:46:22
excerpt:  Linux下配置 Keepalived

---

<h5><a id="user-content-首先呢我想先给大家简单介绍一下什么是keepalived" class="anchor" href="#首先呢我想先给大家简单介绍一下什么是keepalived" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>首先呢，我想先给大家简单介绍一下什么是keepalived：</h5>

<p>Keepalived的作用是检测服务器的状态，如果有一台web服务器死机，或工作出现故障，Keepalived将检测到，并将有故障的服务器从系统中剔除，同时使用其他服务器代替该服务器的工作，当服务器工作正常后Keepalived自动将服务器加入到服务器群中，这些工作全部自动完成，不需要人工干涉，需要人工做的只是修复故障的服务器。</p>

<p>1.准备两台服务器</p>

<p>主服务器：192.168.1.111</p>

<p>从服务器：192.168.1.199</p>

<p>虚拟ip:192.168.1.223</p>

<p>两台机器安装</p>

<p>2.安装keepalived需要的依赖包</p>

<pre><code>
yum install openssl-devel
yum install popt-devel
yum install ipvsadm
yum install libnl*
</code></pre>

<p>3.下载keepalived</p>

<pre><code>
yum install keepalived
</code></pre>

<p>4.修改主服务器配置文件</p>

<pre><code>
vim /etc/keepalived/keepalived.conf
! Configuration File for keepalived

global_defs {
   notification_email {
     #acassen@firewall.loc没有服务器配置邮箱可将其注释掉
     #failover@firewall.loc
     #sysadmin@firewall.loc
   }
   #notification_email_from Alexandre.Cassen@firewall.loc
   #smtp_server 192.168.200.1
   #smtp_connect_timeout 30
   router_id LVS_DEVEL
}

vrrp_instance VI_1 {
    state MASTER
    interface eno16777736 #绑定虚拟IP的网络接口
    virtual_router_id 51#和slave一样
    priority 100#主机高于slave
    advert_int 1#检测服务器状态间隔时间
    authentication {
        auth_type PASS
        auth_pass 1111
    }
    virtual_ipaddress {
       &nbsp;192.168.1.223#虚拟IP地址，可以为多个
    }
}
</code></pre>

<p>开启服务</p>

<pre><code>
systemctl start keepalived
</code></pre>

<p>5.修改slave配置</p>

<pre><code>
vim /etc/keepalived/keepalived.conf
! Configuration File for keepalived

global_defs {
  #notification_email {
  #  644856452@qq.com
  #}
  #notification_email_from Alexandre.Cassen@firewall.loc
  #smtp_server 127.0.0.1
  #smtp_connect_timeout 30
  router_id LVS_DEVEL
}

vrrp_instance VI_1 {
   state SLAVE
   interface eno16777736
   virtual_router_id 51
   priority 80#低于主服务器100
   advert_int 1
   authentication {
       auth_type PASS
       auth_pass 1111#验证密码，两台机器保持一致
   }

  &nbsp;virtual_ipaddress {
       192.168.1.223
   }
}
</code></pre>

<p>开启服务</p>

<pre><code>
systemctl start keepalived
</code></pre>

<p>1.启动两台机器上的nginx</p>

<p>2.启动两台机器上的keepalived</p>

<p>此时使用命令 ip addr 查看虚拟IP绑定 可以看到主 有，从没有，将主机的keepalived关掉，可以看到vip绑定到了从的上面。</p>

<p>那么如何根据服务某个端口的开与关来进行虚拟Ip的绑定呢？</p>

<pre><code>
Vim /usr/share/doc/keepalived-1.2.13/samples/keepalived.conf.vrrp.localcheck
</code></pre>

<p>参考提供的例子</p>

<pre><code>
Configuration File for keepalived
vrrp_script chk_http_port {
       script "</code></pre><code>

<p>将将以上信息复制到两台服务器的/etc/keepalived/keepalived.conf文件里
变成如下，参考，注意从机不一样，为了讲清楚上面的信息放入的位置。</p>

<pre><code>
global_defs {
   notification_email {
     acassen@firewall.loc
     failover@firewall.loc
     sysadmin@firewall.loc
   }
   notification_email_from Alexandre.Cassen@firewall.loc
   smtp_server 192.168.200.1
   smtp_connect_timeout 30
   router_id LVS_DEVEL
}
vrrp_script chk_http_port {
       script "</code></pre><code>

<p>此时再重启两台机器的keepalived服务</p>

<p>Systemctl restart keepalived</p>

<p>此时分别关闭主机80和3306端口服务</p>

<p>可以发现虚拟Ip绑定到了从机上。<span id="transmark" style="display: none; width: 0px; height: 0px;"></span></p>
</code></code>