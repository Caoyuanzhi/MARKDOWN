
##### 参考
https://www.cnblogs.com/yuanchaoyong/p/9976895.html

#### step:
##### 1.个人在github上面创建了仓库，通过本地的git拉取远程仓库到本地报错信息如下：

这是因为Git使用SSH连接，而SSH第一次连接需要验证GitHub服务器的Key。确认GitHub的Key的指纹信息是否真的来自GitHub的服务器。解决办法。其实就是在本地生成key配置到github服务器。这样子接收过来就gitHub服务器了。


##### 2.使用命令： ls -al ~/.ssh

##### 3.使用命令： ssh-keygen -t rsa -C "github用户名"，按三次回车

##### 4.查看生成的key：cat ~/.ssh/id_rsa.pub

##### 5.登陆github,点击头像-settings-new SSH,复制新生成的SSH配置到服务器，记住拷贝是4步骤下面的秘钥信息以ssh-rsa开始邮箱结束的。

