# gitlab

## centOS7.2下的GitLab安装
前提：需要在服务器安装了git之后，才安装gitlab
PS：7.2版本下这是一个深坑之路

### <i class="menu-item-icon fa fa-fw zzq_cion" style="background: #624116;border-radius: 50%;height: 16px;width: 16px;"> </i> GitLab

GitLab是一个独立现代化的开发者协作平台，当然也是基于git
如果你想像gitHub那样，有一个属于自己的git代码托管，或者是你自己公司需要有一个自己的代码管理工具，gitLab是一个不错的选择。

[这是官网（中文）](https://www.gitlab.com.cn/)

### <i class="menu-item-icon fa fa-fw zzq_cion" style="background: #624116;border-radius: 50%;height: 16px;width: 16px;"> </i> GitLaba安装
[参考文献一(简书)](http://www.jianshu.com/p/7a0d6917e009?mType=Group)
[参考文献二（gitla官网）](https://www.gitlab.com.cn/)

#### 安装国内镜像
~~~
1，创建gitlab-ce.repo文件
cd /
vim /etc/yum.repos.d/gitlab-ce.repo
2.配置gitlab-ce.repo文件内容
[gitlab-ce]
name=gitlab-ce
baseurl=http://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el6
repo_gpgcheck=0
gpgcheck=0
enabled=1
gpgkey=https://packages.gitlab.com/gpg.key
~~~
####  安装配置pstfix和gitlab－ce
~~~
1：安装postfix邮件依赖
sudo yum install curl openssh-server openssh-clients postfix cronie
2：这里centos7.2有坑
对于centos6以上要处理防火墙！
sudo systemctl enable sshd
sudo systemctl start sshd

安装postfix
sudo yum install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
sudo firewall-cmd --permanent --add-service=http
注意：这里可能出翔：FirewallD is not running
说明你的FirewallD没有启动，需要启动
执行systemctl start firewalld 
或者sudo systemctl reload firewalld

3：启动 postfix 邮件服务
sudo service postfix start
4：检查 postfix
sudo chkconfig postfix on
5: 安装 GitLab 社区版
sudo yum install gitlab-ce
6:初始化 GitLab
sudo gitlab-ctl reconfigure

~~~

#### 修改 hosts文件
1:添加访问的 host，修改/etc/gitlab/gitlab.rb的external_url
~~~
vim /etc/gitlab/gitlab.rb
修改  external_url 'http://154.1.111'
~~~
2:vi /etc/hosts，添加 host 映射
~~~
vi /etc/hosts
~~~
3:修改/etc/gitlab/gitlab.rb，都要运行以下命令，让配置生效
~~~
sudo gitlab-ctl reconfigure
~~~

如果出现这个：（等一会他的自动配置）
- execute the ruby block reload gitlab-monitor svlogd configuration
然后你就可以在浏览器中输入你配置的网址了
至此你的gitLab算是配置好了

登录首页后默认的
~~~
用户名: root
密码: 5iveL!fell
~~~
~~~
设置密码为：new1....4
~~~
#### 