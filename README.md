### 安装 Ansbile

```
~]# yum install git python-pip -y
# pip安装ansible(国内如果安装太慢可以直接用pip阿里云加速)
~]# pip install pip --upgrade -i https://mirrors.aliyun.com/pypi/simple/
~]# pip install ansible==2.6.18 netaddr==0.7.19 -i https://mirrors.aliyun.com/pypi/simple/
```

### 配置主机互信

```
~]# ssh-keygen  -t rsa -p
~]# ssh-copy-id $IPs #$IPs为所有节点地址包括自身，按照提示输入yes 和root密码
```

```
~]# yum install -y sshpass
```

```
~]# cat ssh_copy.sh
#!/bin/bash
#
IP="172.31.0.7
172.31.0.8
172.31.0.9
172.31.0.10
172.31.0.14"

for node in ${IP};do
  sshpass -p wangjie11@ ssh-copy-id  ${node}  -o StrictHostKeyChecking=no
  if [ $? -eq 0 ];then
    echo -e "\033[46;31m ${node} 秘钥copy成功 \033[0m"
  else
     echo -e "\033[43;31m ${node} 秘钥copy失败 \033[0m"
  fi
done
```
```
~]# bash ssh_copy.sh
```
