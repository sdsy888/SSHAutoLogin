# SSHAutoLogin
一个SSH登录服务器的shell脚本，每次使用ssh登录服务器都要自己输入密码，而且容易输入错误，使用自动登录来节省无谓工作。

## 添加配置
# 如果只有一个服务器，直接删除其中一行即可
在ssh_login文件中，修改以下配置
```shell
    CONFIGS=(
    "服务器名称 端口号 IP地址 登录用户名 登录密码"
    "服务器名称 端口号 IP地址 登录用户名 登录密码"
)
```
比如可以修改成：
```shell
    CONFIGS=(
    "服务器名称 22 220.181.57.217 root baidu.com"
    "新浪服务器 22 66.102.251.33 root sina.com"
)
```
或者在脚本同目录下新建一个文件server_config,按照以上格式写入文件，每个配置单独一行如下：
```
服务器名称 22 220.181.57.217 root baidu.com
新浪服务器 22 66.102.251.33 root sina.com
```
## 使用
1).给ssh_login文件执行的权限,并执行ssh_login
```shell
  chmod u+x ssh_login
  ./ssh_login
```
2).可以将ssh_login 拷贝至 /usr/local ,之后便可以在终端中全局使用ssh_login
```shell
  sudo chmod u+x ssh_login.sh
  sudo chmod 777 ssh_login.sh
  sudo cp ssh_login /usr/local/
  ssh_login.sh
```
3).命令使用

`ssh_login list` - 查看所有服务器配置

`ssh_login 1` - 登录第一个配置的服务器


## 提示
使用本脚本前，请确认已安装expect

1) Linux 下 安装expect
```shell
 yum install expect
```
2）Ubuntu 下 安装expect
```
sudo apt-get install expect
```
3) Mac 下 安装expect
```shell
 brew install homebrew/dupes/expect
```

## 特殊说明
如果密码中含有以下特殊字符，请按照一下规则转义：
- \ 需转义为 \\\\\
- } 需转义为 \\}
- [ 需转义为 \\[
- $ 需转义为 \\\\\\$
- \` 需转义为 \\`
- " 需转义为 \\\\\\"

```
如密码为'-OU[]98' 在CONFIG配置中写成'-OU\[]98'
否则，提示要手动输入密码
```
