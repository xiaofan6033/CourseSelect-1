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
### 本地测试：
### Travis CI 线上自动测试：
### 7.线上部署：
### 8.进行项目时遇到的问题及解决方法：

## 说明

目前使用的库和数据库：

* 使用[Bootstrap](http://getbootstrap.com/)作为前端库
* 使用[Rails_admin Gem](https://github.com/sferik/rails_admin)作为后台管理
* 使用[Postgresql](http://postgresapp.com/)作为数据库

使用前需要安装Bundler，Gem，Ruby，Rails等依赖环境。

请根据本地系统下载安装[postgresql](https://devcenter.heroku.com/articles/heroku-postgresql#local-setup)数据库，并运行`psql -h localhost`检查安装情况。


## 在本地机部署方法

在终端（MacOS或Linux）中执行以下代码。

注意：在执行下面代码之前，请确认数据库系统（PostgreSQL)已经在本地安装好，用命令 postgres -D /usr/local/var/postgres/ 启动数据库系统，并且用命令：createdb courseselect_development 创建选课系统应用数据库。在bundle install 时，一定是链接外网，若
是MacOS, 还要执行命令：sudo xcodebuild -license， 输入agree授权Apple xcodebuild 软件进行编译。

```
$ git clone https://github.com/PENGZhaoqing/CourseSelect
$ cd CourseSelect
$ bundle install
$ rake db:migrate
$ rake db:seed
$ rails s 
```

## 安装正常后的使用方法

在浏览器中输入`localhost:3000`访问应用系统主页

1.学生登陆：

账号：`student1@test.com`

密码：`password`

2.老师登陆：

账号：`teacher1@test.com`

密码：`password`


3.管理员登陆：

账号：`admin@test.com`

密码：`password`

账号中数字都可以替换成2,3...等等


## 在 Heroku 云端部署方法

项目可直接在Heroku上免费部署

1.fork此项目到自己Github账号下

2.创建Heroku账号以及Heroku app

3.将Heroku app与自己Github下的fork的项目进行连接

4.下载配置[Heroku CLI](https://devcenter.heroku.com/articles/heroku-command-line)命令行工具

5.运行`heroku login`在终端登陆，检查与heroku app的远程连接情况`git config --list | grep heroku`，若未检查到相应的app，请看[这里](http://stackoverflow.com/questions/5129598/how-to-link-a-folder-with-an-existing-heroku-app)

6.运行部署，详情[请戳这里](https://devcenter.heroku.com/articles/getting-started-with-rails4#rails-asset-pipeline)


## 在本地测试方法

本项目包含了部分的测试（integration/fixture/model test），测试文件位于/test目录下。
在一键运行所有测试使用`rake test`命令之前，一定检测是否用命令 postgres -D /usr/local/var/postgres/ 启动数据库系统，并且执行过命令：createdb courseselect_test 创建选课系统应用测试数据库。

```
PENG-MacBook-Pro:IMS_sample PENG-mac$ rake test
Run options: --seed 15794

# Running:
.........

Finished in 1.202169s, 7.4865 runs/s, 16.6366 assertions/s.

9 runs, 20 assertions, 0 failures, 0 errors, 0 skips
```

### 模型测试

以用户模型为例, 位于`test/models/user_test.rb`, 首先生成一个`@user`对象，然后`assert`用户是否有效，这里的调用`valid`方法会去检查你的模型中的相关的`validates`语句是否正确，若`@user.valid?`为false, 那么此`assert`会报错，代表`"should be valid"`这条测试没有通过, 单独运行此测试文件使用`rake test test/models/user_test.rb`


```
class UserTest < ActiveSupport::TestCase
  # test "the truth" do
  #   assert true
  # end

  def setup
    @user = User.new(name: "Example User", email: "user@example.com", password: "password", password_confirmation: "password")
  end

  test "should be valid" do
    assert  @user.valid?
  end

  ...

end
```

### 视图和控制器测试

以用户登录为例，位于`test/integration/user_login_test.rb`，首先同样生成一个@user模型，这个@user的用户名和密码可以在`test/fixtures/users.yml`中指定, 然后我们用get方法到达登录页面（sessions_login_path），然后使用post方法提交这个@user的账号密码来登录，如果登录成功，当前应该会跳转至homes控制器下的index方法进行处理，`assert_redirected_to`能判断这个跳转过程是否发生，然后调用`follow_redirect！`来紧跟当前的跳转，用`assert_template`来判读跳转后的视图文件是否为`homes/index`, 最后在这个视图文件下做一些测试，比如判断这个视图下连接为root_path的个数等等（根据当前登录的角色不同，当前的页面链接会不同，比如admin用户就会有控制面板的链接rails_admin_path，而普通用户没有，因此可以根据链接的个数来判断当前登录用户的角色）

```
class UserLoginTest < ActionDispatch::IntegrationTest

  def setup
    @user = users(:peng)
  end

  test "login with valid information" do
    get sessions_login_path
    post sessions_login_path(params: {session: {email: @user.email, password: 'password'}})
    assert_redirected_to controller: :homes, action: :index
    follow_redirect!
    assert_template 'homes/index'
    assert_select "a[href=?]", root_path, count: 2
    assert_select "a[href=?]", rails_admin_path, count: 0
  end
end
```

### 测试涵盖率检测

我们可以使用[simplecov](https://github.com/colszowka/simplecov/)库来检测我们编写的测试对于我们的项目是否完整，步骤如下：

1. 在Gemfile文件中导入simplecov库：`gem 'simplecov', :require => false, :group => :test`，然后`bundle install`安装
2. 在test/test_helper.rb的最前面加入simplecov的启动代码（这里默认使用rails自带的test框架，simplecov也支持其他测试框架如rspec，那么启动代码导入的位置请参考simplecov的官方文档）

  ```
  # 注意这里必须在 require rails/test_help 之前加入，否则不会生效
  require 'simplecov'
  SimpleCov.start 'rails'

  ENV['RAILS_ENV'] ||= 'test'
  require File.expand_path('../../config/environment', __FILE__)
  require 'rails/test_help'

  class ActiveSupport::TestCase
    # Setup all fixtures in test/fixtures/*.yml for all tests in alphabetical order.
    fixtures :all

    # Add more helper methods to be used by all tests here...
  end
  ```

3. 运行`rake test`,成功后会根目录的coverage下生成一个index.html文件，用浏览器打开能看到结果如下：

  <img src="/lib/screenshot5.png" width="700">  

  <img src="/lib/screenshot6.png" width="700">  


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


