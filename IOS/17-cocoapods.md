`CreateTime 2017.03.16`

```
1. cd 项目目录
2. vim Podfile
3. 输入
  platform :ios,'7.0'
  target 'SMG_Language' do
  pod 'AFNetworking','~>3.1.0'
  end
4. esc
5. :wq
6. 检查项目SMG_Language.xcodeproj同目录有个Podfile文件
7. pod install//假如失败,重新pod setup






cocoapods安装升级
http://www.jianshu.com/p/2ef8a38416c4
cocoapods常见问题
http://blog.csdn.net/linwenbang/article/details/46481501




------------------------------------------备忘------------------------------------------
安装pod setup成功的备忘:
localhost:SMG_Language jia$ pod setup
Setting up CocoaPods master repo
  $ /usr/bin/git clone https://github.com/CocoaPods/Specs.git master --progress
  Cloning into 'master'...
  remote: Counting objects: 1138732, done.        
  remote: Compressing objects: 100% (426/426), done.        
  remote: Total 1138732 (delta 188), reused 0 (delta 0), pack-reused 1138281        
  Receiving objects: 100% (1138732/1138732), 384.04 MiB | 3.89 MiB/s, done.
  Resolving deltas: 100% (537282/537282), done.
  Checking out files: 100% (142688/142688), done.
CocoaPods 1.2.1.beta.1 is available.
To update use: `sudo gem install cocoapods --pre`
[!] This is a test version we'd love you to try.
For more information, see https://blog.cocoapods.org and the CHANGELOG for this version at https://github.com/CocoaPods/CocoaPods/releases/tag/1.2.1.beta.1
Setup completed

安装AFNetworking
localhost:SMG_Language jia$ pod install
Analyzing dependencies
Downloading dependencies
Installing AFNetworking (3.1.0)
Generating Pods project
Integrating client project
[!] Please close any current Xcode sessions and use `SMG_Language.xcworkspace` for this project from now on.
Sending stats
Pod installation complete! There is 1 dependency from the Podfile and 1 total pod installed.
localhost:SMG_Language jia$ 






















注:


pod repo remove master


pod repo add master https://gitcafe.com/akuandev/Specs.git

pod setup

 ping github.com/CocoaPods/Specs.git

ping git.oschina/akuandev/Specs.git

ping gitcafe.com/akuandev/Specs.git




$ ruby -v

rvm list

rvm -v


sudo gem update --system


gem update

gem -v

gem sources -l

gem sources



cd ~/.cocoapods

 pod repo list

sudo xcode-select --switch/Applications/Xcodeapp

sudo gem install -n /usr/local/bin cocoapods

gem sources -a https://gems.ruby-china.org/

rvm use 2.2.2 --default

rvm list known

gem rvm update

rvm install 2.2.2


fuby -v

```

***

| 180228重装备忘 >> |  |
| --- | --- |
| 1 | sudo gem update --system |
| 2 | sudo gem install -n /usr/local/bin cocoapods |


| 180929解决pod update太慢问题 >> |  |  |
| --- | --- | --- |
| 1 | cd ~/.cocoapods/repos |  |
| 2 | pod repo remove master | 删master,可以直接到finder删 |
| 3 | git clone https://git.coding.net/hging/Specs.git master | 用国内库更新快 |
| 4 | source 'https://git.coding.net/hging/Specs.git' | Podfile文件加一行描述 |
| 5 | pod install --verbose --no-repo-update | 用后辍命令执行install |
| 6 | pod update --verbose --no-repo-update | 或update |

| 180929解决pod update慢问题方法2 >> |  |
| --- | --- |
| 1 | pod repo remove master |
| 2 | pod repo add master https://git.oschina.net/6david9/Specs.git |
| 3 | pod repo update |
| 4 | Podfile头部指定: source 'https://git.oschina.net/6david9/Specs.git' |
| 5 | pod update  --verbose --no-repo-update |

| 20200709重装备忘 | 花括号,表示占位符,替换为正确内容即可; |
| --- | --- |
| 1. 安装gem | sudo gem update --system |
| 2. 查看源 | gem sources -l |
| 3. 删旧源 | gem sources --remove {占位:2中显示的源,一般是https://rubygems.org/} |
| 4. 换新源 | gem sources -a https://gems.ruby-china.com/ |
| 5. 安装pod | sudo gem install -n /usr/local/bin cocoapods |
| 6. 使用 | 到项目目录下,执行pod update |
