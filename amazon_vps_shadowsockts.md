amazone vps + ShadowSocks 科学上网配置方法
========================================


#服务端


##1. 注册AWS并创建Ubuntu实例，参考 http://bbs.eve-china.com/thread-634935-1-1.html
1. 要有双币信用卡，没有的话，下面也不用看了
2. 创建的机器选新加坡的，网速快（据说）
3. 不要乱动其它选项

##2. SSH登录
##3. 下载 python gevent 和 pip ,    命令： sudo apt-get install python-gevent python-pip
1. 如果报错，基本就是下载的源无效连接不上，解决方法参见 http://askubuntu.com/questions/135932/apt-get-update-failure-to-fetch-cant-connect-to-any-sources
2. 上步解决完了，应该还会接着报错 
<pre><code> The following packages have unmet dependencies:
 python-pip : Depends: python-setuptools (>= 0.6c1) but it is not going to be installed
 E: Unable to correct problems, you have held broken packages.
 </code></pre>
 
    <br/>
    解决方法，参见 http://askubuntu.com/questions/529217/not-able-to-fix-the-error-unable-to-correct-problems-you-have-held-broken-pack

    1. sudo apt-get purge python-pkg-resources
    2. sudo apt-get -f install
    3. sudo apt-get install python-gevent python-pip

##4.用 Pip下载 shadowsocks ， 命令：sudu pip install shadowsocks
##5. 新建 config.json 在/etc/shadowsocks/下（默认没有这个文件，你要自己创建一个），或者home或者其他地方。
<pre><code>
{
    "server":"my_server_ip",
    "server_port":8388,
    "local_port":1080,
    "password":"barfoo!",
    "timeout":600,
    "method":"aes-256-cfb"
}
</code></pre>

1. 端口号 不用改了，下面也方便配置，server 写成 0.0.0.0， 啥原因我也没搞明白
2. 安装加密算法包， sudo apt-get install python-m2crypto
3. 运行， ssserver -c /etc/shadowsocks/config.json 
4. 完成， 这以上是服务端处理，还算不太麻烦的，上面的server日志是打到console里的，也可以后台运行 nohup ssserver -c /etc/shadowsocks/config.json


---

#客户端

这个就很简单了，PC、Mac手机 都有相应的客户端 ，参见 http://ttt.tt/150/


另外， 昨天涧硕推荐的wallproxy也挺好用的，昨天晚上我也试了下，还算挺快，看它的源码有很多是和goagent一样的，报错的日志也一样…… ，不过还是需要能访问google的机器才行，我也是用amazon的vps上传成功的，  论网速的话，个人感觉没有ss快~






