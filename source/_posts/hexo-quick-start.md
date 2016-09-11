

***
## 快速安装hexo，并部署到github.io,这里针对是3.*版本
***
* 1 确保本地已经有nodejs和git bash
* 2 执行 ，npm install hexo --global 或者 npm i hexo -g\
* 3 hexo init \<your-blog-name> 初始化一个blog项目的根文件夹，然后进去
```javascript
  hexo init my-blog
  cd my-blog
```
* 4 替换掉默认的样式landscape 为 next，这一步可以省略，用默认的样式也ok
```javascript
 git clone https://github.com/iissnan/hexo-theme-next themes/next
```
* 5 本地跑起来博客项目
 ```javascript
 hexo server
```
* 6 在自己的github 仓库里新建一个仓库名 \<your-name>.github.io，注意这里必须这样命名
* 7 打开项目里的_config.yml文件，修改deploy配置为如下内容
```javascript
deploy:
  type: git
  repository: git@github.com:<your_repository_name_url>
  branch: master
```
* 8 在本地blog的根文件夹下安装git部署器，确保本地的博客文件能够部署到你的远端git仓库 
```javascript
npm i hexo-deployer-git --save
```
* 9 本地生成ssh的id_rsa.pub文件，然后在远端git上添加d_rsa.pub里的内容即ssh-key
```
ssh-keygen -t rsa -C <you_mail> //一路回车，创建好pub文件
cat ~/..ssh/id_rsa.pub //把内容添加到git的ssh-keys管理里
eval `ssh-agent -s` //启动ssh代理，注意这里必须是反斜号
ssh-add ~/.ssh/id_ras.pub
ssh -T git@github.com //测试ssh通不通，也可以是-vT 参数，打印详细信息
hexo g -d //生成静态文件，并部署到github.io, 这个命令是 hexo g && hexo d 的合体
```