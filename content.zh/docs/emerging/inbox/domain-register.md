+++
title = "域名注册"
date = 2022-03-12T16:00:00+08:00
lastmod = 2022-03-14T15:51:45+08:00
categories = ["Opportunity"]
draft = false
+++

域名是需要每年续费的，不续费就会过期，过期之后就会被删除，也就回到了“未注册”的状态，这个时候，任何人都可以重新注册这个域名了。


## [Sedo.com](https://www.sedo.com/) {#sedo-dot-com}

世界上最大的域名交易网站，可以注册在 Sedo 搜索中意的域名，很有可能这个域名正在出售中。


## [Pool.com](https://www.pool.com/) {#pool-dot-com}

最大的过期域名抢注商，每天公布即将过期的域名，并帮助你抢注，抢注成功只收 60 美金的手续费，不成功不收钱

具体的操作办法如下：

-   访问 Pool.com 并点击上方的“Deleting Domains”菜单，然后点击页面底部的“Download the Full List” 下载所有即将删除的域名列表。
-   解压后这个列表是个 txt 文档，每一行一个域名，如果你在 Linux 或 Mac 的系统里，运行一个简短的 Shell 脚本：

<!--listend-->

```shell
 #!/bin/sh
fname=”$1″
exec<$fname
regex='^([a-z]{1,1})([a|e|i|o|u]{1,1})([a-z]{1,4})\.com(.+)'
while read line
do
    if [[ “$line” =~ $regex ]];then
        echo $line
    fi
done
```

-   判断是否是长度 6 位以内、并且第二个字母是元音的.com 域名.

**为什么第二个字母要元音（a,e,i,o,u）呢?**

因为根据发音规则，第二个字母是元音的话，域名的可读性更强，比如 facebook, youtube, vimeo, mint, techcrunch, google, yahoo 等都符合这个规则， twitter 是极其少见的前两位合成一个双音节声母，导致元音后移到了第三位。