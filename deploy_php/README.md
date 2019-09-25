发布和回滚 PHP 代码
==================

# 说明：

发布和回滚主要是依据两个变量： 版本号(release_version) 和 项目名字（job_name）。
发布如果结合Jenkins， 则这里的 job_name 则可以直接引用 Jenkins 自带的变量 JOB_NAME 。

# 发布：

## 发布代码的三种使用方式

### 直接使用当前发布服务器的时间作为版本号,不手动指定版本号
`ansible-playbook -e "job_name=wordpress release_version=$(date +%Y%m%d%H%M%S)" /etc/ansible/deploy.yml`

### 结合 Jenkins，使用 git tag 作为版本号
`ansible-playbook -e "job_name=wordpress release_version=${tag}" /etc/ansible/deploy.yml`

### 发布代码的同时，也设置保留多少个历史版本,其他的老版本将被删除
`ansible-playbook -e "job_name=wordpress release_version=$(date +%Y%m%d%H%M%S) keep_releases=3" /etc/ansible/deploy.yml`

# 回滚：

## 回滚代码的三种方式：

### 不选择版本号，直接回滚到上一次稳定版本
`ansible-playbook -e "job_name=wordpress" /etc/ansible/rollback.yml`

### 如果使用时间作为版本号，根据线上已经存在的历史版本，通过指定版本号，回滚到这个指定的版本
`ansible-playbook -e "job_name=wordpress release_version=20190925144115" /etc/ansible/rollback.yml`

### 如果使用 git tag 作为版本号，根据线上已经存在的历史版本，通过指定版本号，回滚到这个指定的版本
`ansible-playbook -e "job_name=wordpress release_version=v1.0.1" /etc/ansible/rollback.yml`

# 我的博客:

更多IT运维相关内容详情欢迎访问我的博客： [我的ROOT](http://wdroot.com)
