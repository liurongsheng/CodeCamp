# 搭建 git服务器及权限管理 

## 使用最新源码方式安装 git
```
//安装git依赖
yum install -y curl-devel expat-devel gettext-devel openssl-devel zlib-devel
cd /user/local
mkdir git
cd git
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.18.0.tar.gz
tar -xvf git-2.18.0.tar.gz
cd git-2.18.0
make prefix=/usr/local all
sudo make prefix=/usr/local install
git --version
//git version 2.18.0
```
## 添加git的管理的账号和密码
```
useradd git
passwd git //两次输入密码
```

## 使用gitolite管理权限
可以使用gitolite 或者 gitosis，两者都差不多，一个是Perl开发，一个是Python开发。

### 安装gitolite依赖
yum install -y 'perl(Data::Dumper)'

### 安装gitolite
```
su git
mkdir -p ~/bin //在git用户home目录下建立bin目录
git clone git://github.com/sitaramc/gitolite //下载gitolite管理软件
cd gitolite
./install -to ~/bin
//把本机上的id_rsa.pub公钥复制到git的用户目录
~/bin/gitolite setup -pk ~/id_rsa.pub 
//设置完成后可以看到repositories目录下已经有了两个git仓库了
[git@localhost ~]$ ls /home/git
bin  gitolite  id_rsa.pub  projects.list  repositories
[git@localhost ~]$ cd repositories/
[git@localhost repositories]$ ls
gitolite-admin.git  testing.git
[git@localhost repositories]$ 
gitolite-admin.git    # 管理配置权限的仓库
testing.git           # 测试仓库
```
### 管理员本地管理配置
git clone git@192.168.80.123:gitolite-admin

修改gitolite-admin下的conf文件
```
@work = workName1 workName2 //项目名
@work_team = adminliu user1 user2 //团队用户 
@admin = adminliu //管理者

repo gitolite-admin //配置管理员权限
    RW+     =   @admin

repo testing
    RW+     =   @all
    
repo @work    //配置项目权限
    RW      = @work_team
    RW      = @admin  
```

### 添加用户更新配置
如果添加用户把新用户的pubkey放置到keydir目录下，修改config配置

做好配置后，由管理员把修改push到服务器端，会自动处理。
```
git add conf
git add keydir
git commit -m "added user1 user1"
git push
```