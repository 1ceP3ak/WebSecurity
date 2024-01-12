## Web入门

### 信息搜集（1-20）

#### Web1

> ```
> 开发注释未及时删除 
> ```

F12查看源码即可看到flag

#### Web2

> ```
> js前台拦截 === 无效操作
> ```

- view-source查看源码即可看到flag
- 浏览器直接F12查看源码即可看到flag
- 写爬虫requests.get()即可看到flag

#### Web3

> ```
> 没思路的时候抓个包看看，可能会有意外收获
> ```

抓包看响应包的返回头信息即可看到flag

#### Web4

> ```
> 总有人把后台地址写入robots，帮黑阔大佬们引路。
> ```

扫描站点目录发现存在robots.txt，访问后发现flagishere.txt文件，访问即可看到flag

#### Web5

>```
>phps源码泄露有时候能帮上忙
>```

本题考查的是phps作为备份文件，泄露了源码。其他常见的有linux的备份文件，比如index.php.swp还有www.zip等。可以用的工具有：https://github.com/shanyuhe/fzbk或者使用burp打一波fuzz。
[https://github.com/3had0w/Fuzzing-Dicts/blob/master/%E5%B8%B8%E8%A7%81%E7%BD%91%E7%AB%99%E5%A4%87%E4%BB%BD%E6%96%87%E4%BB%B6%E5%AD%97%E5%85%B8%EF%BC%882954%EF%BC%89.txt](https://github.com/3had0w/Fuzzing-Dicts/blob/master/常见网站备份文件字典（2954）.txt)

注意后缀可以结合当前文件，比如index.php来修改，如果是upload.php则可以改为upload.php.zip等。

#### Web6

>```
>解压源码到当前目录，测试正常，收工
>```

www源码泄露，扫描目录发现`www.zip`，打开发现flag路径fl000g.txt

#### Web7

>```
>版本控制很重要，但不要部署到生产环境更重要。
>```

git信息泄露，扫描目录发现`.git`文件，打开即可看到flag

#### Web8

>```
>版本控制很重要，但不要部署到生产环境更重要。
>```

svn信息泄露，扫描目录发现`.svn`文件，打开即可看到flag

SVN（subversion）源代码版本管理软件，造成SVN源代码漏洞的主要原因是管理员操作不规范。在使用SVN管理本地代码过程中，会自动生成一个名为.svn的隐藏文件夹，包含重要的源代码信息，开发管理员在发布代码时，不愿意使用"导出"功能，而是直接复制代码文件夹到WEB服务器上，导致.svn隐藏文件夹被暴露于外网环境。

#### Web9

>```
>发现网页有个错别字？赶紧在生产环境vim改下，不好，死机了
>```

vim缓存信息泄露，swp缓存信息泄露，/index.php.swp路径拼接。

以 index.php 为例：第一次产生的交换文件名为 `.index.php.swp`

再次意外退出后，将会产生名为 `.index.php.swo` 的交换文件

第三次产生的交换文件则为 `.index.php.swn`

#### Web10

>```
>cookie 只是一块饼干，不能存放任何隐私数据
>```

cookie信息泄露

#### Web11

>```
>域名其实也可以隐藏信息，比如flag.ctfshow.com 就隐藏了一条信息
>```

查询域名解析地址

```bash
nslookup -query=any flag.ctfshow.com
```

#### Web12

>```
>有时候网站上的公开信息，就是管理员常用密码
>```

根据提示查看网页，发现最下面有一个特别的number，猜想可能为某个密码，查看robots.txt文件

```bash
User-agent: *
Disallow: /admin/
```

发现文件夹/admin/访问是个登录后台，猜想账号：admin密码：372619038，登录拿到flag

#### Web13

>```
>技术文档里面不要出现敏感信息，部署到生产环境后及时修改默认密码
>```

在页面底部找到Document，内含登陆信息，在所给网址中登陆账号密码，得到flag

#### Web14

>```
>有时候源码里面就能不经意间泄露重要(editor)的信息,默认配置害死人
>```

根据提示，扫描目录，加/editor 发现是一个编辑器，在编辑器中，找到插入文件。 发现插入的文件 ，在文件空间中找文件插入，发现居然是服务器中的文件（非本地），于是浏览一下目录在var/www/html目录 中，存在一个nothinghere有一个文件 fl000g.txt 直接访问这个fl000g.txt 即可获得flag!

#### Web15

>```
>公开的信息比如邮箱，可能造成信息泄露，产生严重后果
>```

题目信息提示公开邮箱可能造成信息泄露，我们发现一个邮箱，尝试登陆后台，用户名admin，密码输入邮箱不正确，点击忘记密码，密保问题为所在城市，搜索邮箱中的qq号，发现位于西安，重置密码成功，登陆获得flag

#### Web16

>```
>对于测试用的探针，使用完毕后要及时删除，可能会造成信息泄露
>```

dirsearch扫描无果，查看Writeup是访问tz.php，绝了。

#### Web17

>```
>备份的sql文件会泄露敏感信息
>```

dirsearch扫描目录发现存在/backup.sql，访问拿到flag。

#### Web18

>```
>不要着急，休息，休息一会儿，玩101分给你flag
>```

这是一个javascript 的游戏，游戏的目的就是让要赢，从js代码中可知，当score>120时，且game_over这个参数为false时，即可赢，于是打开开发者模式中的console，直接赋值score=130，game_over=false 然后，执行游戏的run()即可得到 "你赢了，去幺幺零点皮爱吃皮看看"， 即，110.php 打开它，即得flag

#### Web19

>```
>密钥什么的，就不要放在前端了
>```

F12查看源码，可以看到账号密码。

#### Web20

>```
>mdb文件是早期asp+access构架的数据库文件，文件泄露相当于数据库被脱裤了。
>```

dirsearch扫描目录发现/db，继续扫描/db下的内容，发现数据库文件/db/db.mdb，查看flag。

#### 敏感信息泄露小结

- Stash
- Log
- DS_Store
- bak文件
- vim缓存
- 网站源码
- hg泄露
- SVN泄露
- phpinfo
- 目录遍历