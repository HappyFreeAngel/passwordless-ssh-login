Role Name
=========

ssh 免密码登陆模块

前提条件
------------
Linux 系统，执行的用户必须具备root权限,能创建用户


Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------
   user_host_list=?
   username=? centos,
   password=? yourpassword, #这个密码是加密形式的，不能用明码
   auto_generate_etc_host_list=? False
   sudo_privilege? True 显示传入

Dependencies
------------
Linux 系统必须有ssh-keygen 命令

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

先定义spark-hosts变量
spark-hosts:
  - name: "spark-node1.cityworks.cn"
  - name: "spark-node2.cityworks.cn"
  - name: "spark-node3.cityworks.cn"
  - name: "spark-node4.cityworks.cn"   
  - name: "spark-node5.cityworks.cn"
  

## 实例1
```
- name: "安装不同主机间用户之间root免密码登陆 passwordless-ssh-login 这个不是必须的,只是为了方便用户使用."
  include_role:
     name: passwordless-ssh-login
  vars:
    user_host_list: "{{spark_host_list}}"
    username: "root"
    password: "{{root_salt_password}}"
    sudo_privilege: True
    auto_generate_etc_host_list: False
```  
      
## 实例2
```
- name: "安装不同主机间用户{{spark_username}}之间免密码登陆 passwordless-ssh-login"
  include_role:
     name: passwordless-ssh-login
  vars:
    user_host_list: "{{spark_host_list}}"
    username: "{{spark_username}}"
    password: "{{spark_salt_password}}"
    sudo_privilege: True
    auto_generate_etc_host_list: True
  become_user: root
      
```

License
-------

BSD
源代码下载地址
https://github.com/HappyFreeAngel/passwordless-ssh-login.git

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
# passwordless-ssh-login
源代码下载地址
https://github.com/HappyFreeAngel/passwordless-ssh-login.git
