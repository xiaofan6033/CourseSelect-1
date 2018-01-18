# CourseSelect [![Build Status](https://travis-ci.org/PENGZhaoqing/CourseSelect.svg?branch=master)](https://travis-ci.org/PENGZhaoqing/CourseSelect)
### 1.项目介绍：
([项目演示链接网址](https://courseselect.herokuapp.com/ ))
本项目是高级软件工程课程大作业，是在已有的一个在线选课系统上进行的二次开发，完善改进该系统的功能。包含对已有项目的分析，二次开发，测试，部署等部分
### 2.开发环境和关键技术：
* 使用rails作为开发框架
* 使用PostgreSQL作为数据库，用于存放users，courses，grades三张数据表
* 使用heroku进行线上部署
* 使用github来存放代码，对代码进行管理
* 使用atom对项目进行编辑，使编程更加方便便捷
### 3.原有功能：
* 多角色登陆（学生，老师，管理员）
* 学生动态选课，退课
* 老师动态增加，删除课程
* 老师对课程下的学生添加、修改成绩
* 权限控制：老师和学生只能看到自己相关课程信息
### 4.新增功能：
* 绑定邮箱：在注册后，用户登录时要激活邮箱验证
* 解决选课冲突：主要是通过上课时间冲突来提示学生选课冲突
* 学分统计：实现查看已获得成绩的课程的学分统计情况，查看目前选课的学分统计情况，查看用户对应学位的学分要求
* 课程评估：学生在选修课程并获得学分后，可以根据自身情况对该课程从五个方面进行评价，为后面选课的学生提供参考
* 导出excel课表：学生选课后，可以导出个人课表
### 5.项目截图：
<img src="/lib/screenshot1.png" width="700">  
<img src="/lib/screenshot2.png" width="700">
<img src="/lib/screenshot3.png" width="700">   
<img src="/lib/screenshot4.png" width="700">
### 6.测试：
### 6.1本地测试：
   本项目包含了部分的测试（integration/fixture/model test），测试文件位于/test目录下。在一键运行所有测试使用`rake test`命令之前，一定检测是否用命令 postgres -D /usr/local/var/postgres/ 启动数据库系统，并且执行过命令：createdb courseselect_test 创建选课系统应用测试数据库。在项目原有c测试的基础上增加了如下测试：
  对model的测试. 由于原有系统已有对user的model test，因此需新增对course的model test即对course各个属性进行有效性验证以及长度进行验证。主要的测试用例如下：（CourseSelect/test/models/course_test.rb） 
  
  在develop.rb中配置本地的server在浏览器中键入地址：分别预览html格式和text格式的邮件。





### 6.2Travis CI 线上自动测试：
### 7.部署：
### 7.1本地部署：
在终端（MacOS或Linux）中执行以下代码。
注意：在执行下面代码之前，请确认数据库系统（PostgreSQL)已经在本地安装好，用命令 postgres -D /usr/local/var/postgres/ 启动数据库系统，并且用命令：createdb courseselect_development 创建选课系统应用数据库。在bundle install 时，一定是链接外网，若是MacOS, 还要执行命令：sudo xcodebuild -license， 输入agree授权Apple xcodebuild 软件进行编译。
$ git clone https://github.com/PENGZhaoqing/CourseSelect
$cd CourseSelect
$ bundle install
$ rake db:migrate
$ rake db:seed
$ rails s
### 7.2线上部署：
### 8.进行项目时遇到的问题及解决方法



# 在 Heroku 云端部署方法

项目可直接在Heroku上免费部署

1.fork此项目到自己Github账号下

2.创建Heroku账号以及Heroku app

3.将Heroku app与自己Github下的fork的项目进行连接

4.下载配置[Heroku CLI](https://devcenter.heroku.com/articles/heroku-command-line)命令行工具

5.运行`heroku login`在终端登陆，检查与heroku app的远程连接情况`git config --list | grep heroku`，若未检查到相应的app，请看[这里](http://stackoverflow.com/questions/5129598/how-to-link-a-folder-with-an-existing-heroku-app)

6.运行部署，详情[请戳这里](https://devcenter.heroku.com/articles/getting-started-with-rails4#rails-asset-pipeline）
## Travis CI 线上自动测试

上述为本地测试，我们可以使用Travis CI来实现自动测试，首先申请一个Travis CI的账号，然后与自己的github连接起来，接着在自己项目根目录中增加一个新的文件`.travis.yml`如下，这个文件中指定了测试需要的ruby版本，数据库等配置以及一些测试前的脚本操作，当你的github发生更新后，Travis CI会自动触发测试（需要你在Travis CI中自己设置自动/手动触发），然后读取你的`.travis.yml`文件配置进行测试，其实也就是把本地测试拉到服务器上进行，测试成功后会在你的github项目给一个buliding pass的标签（见CourseSelect题目旁边），代表当前的代码是通过测试的

```
language: ruby

rvm:
  - 2.2

env:
  - DB=pgsql

services:
  - postgresql

script:
  - RAILS_ENV=test bundle exec rake db:migrate --trace
  - bundle exec rake db:test:prepare
  - bundle exec rake

before_script:
  - cp config/database.yml.travis config/database.yml
  - psql -c 'create database courseselect_test;' -U postgres
```

## How to Contribute

先fork此项目，在分支修改后，pull request到主分支

提问请到issues里创建，欢迎contributor！

如果觉得好，给项目点颗星吧～


