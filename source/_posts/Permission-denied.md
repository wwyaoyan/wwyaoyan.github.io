---
title: Permission denied(publickey)
---
不知道什么原因,有一次,我本地的公司项目无法pull,也无法push项目了,![](http://i4.buimg.com/567571/44198f9ebab475a8.png)
但是ssh连接主机又是成功的。
![](http://i1.piimg.com/567571/e34d5692f17ed2e0.png)
后来知道是ssh的问题。但是重新配置了ssh key,并且更改了github上面ssh key还是不行,搞了很久,最后在一同事的提醒下,在公司git的项目里把里面的ssh key也更改了就ok了。下面是整个正确的操作流程。

## 检查是否已经有SSH Key

``` bash
$ cd ~/.ssh
```
如果说没有这个目录，就直接生成一个新的SSH

## 备份删除
如果上一步得出有.ssh文件,则备份删除这个文件

## 生成一个新的SSH

``` bash
$ ssh-keygen -t rsa -C "you email"
```
之后直接三次回车，不用填写东西。然后就生成一个目录.ssh ，里面有两个文件：id_rsa , id_rsa.pub

## 复制生成的公钥,将其放到你的github上

``` bash
$ vim ~/.ssh/id_rsa.pub
```
这个命令可以直接查看id_rsa.pub的内容,之后手动复制全部内容,或者直接在电脑上找到.ssh文件夹,然后复制里面id_rsa.pub的内容

## 在github上新建ssh key

打开你的github,点击右上角的头像,然后选择下面的"settings"
选择出现的"SSH and GPG keys",之后"New SSH key","title"可以随便填,然后将上一步中复制的内容粘贴到"key"的输入框里面。完成之后点击"Add SSH key"

## 在公司或你所要进行的项目所在的git上面也按上一步的操作,重新设置ssh key

上面的内容,在网上都有相应的文章进行阐述,并不难完成,而这最后一步却很重要,很容易被忽略,我一开始就是忽略了这一步才导致一直都不成功,也找不出原因。做完上述的操作,记得在公司或你所要进行的项目所在的git上面按照上一步的操作,也进行重新配置ssh key