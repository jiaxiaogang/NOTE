| 账户 >> |
| --- |

|  |  |  |
| --- | --- | --- |
| 1 | ssh登录linux | ssh root@180.76.113.98 |

***

| 文件 >> |
| --- |

|  |  |  |
| --- | --- | --- |
| 1 | 查看目录 | ls -a |
| 2 | 删除文件 | rm fileName.md -f |
| 3 | 删除目录 | rm folderName -r -f |
| 4 | 更名 | mv fileOrFolderA fileOrFolderB |
| 5 | 快速查找文件 | locate fileName |
| 6 | 查找 | where is mysql |
| 7 | 创建文件夹 | mkdir xxx |
| 8 | 复制 | cp -r xxx targetFolder |

***

| 程序 >> |
| --- |

|  | 功能 | 命令 | 目录 |
| --- | --- | --- | --- |
| 1 | 安装java | yum install java |  |
| 2 | 下载 | wget http://xxx.xxx.com/xxx.file |  |
| 3 | mac->linux上传目录 | jia:~ jia$ scp -r /Users/jia/Desktop/Folder root@111.111.111.111:/root/Folder |  |
| 4 | mac->linux上传文件 | scp -r /Users/jia/Desktop/MacFile.md root@111.111.111.111:/root/LinuxFile.md |  |
| 5 | mac->linux下载文件 | scp -r root@180.76.113.98:/root/serviceFileName.md /Users/jia/Desktop/downloadFileName.md |  |
| 6 | 安装tomcat | `wget x.gz` `tar -zxv -f x.x.gz` `tomcat/bin/startup.sh` | 正确 |
| 7 | 安装solo | `将solo.war放到tomcat9/webapps下会自动生成solo文件夹` `cd solo/WEB-INF/classes` `vim latke.properties` `将localhost改成180.76.113.98` | 访问180.76.113.98:8080/solo(注:latke.properties中端口号需与tomcat相同) |
| 8 | 安装git | yum -y install git |  |
| 9 | yum卸载 | yum remove mysql |  |
| 10 | 安装httpd | `yum -y install httpd*` `httd -v` |  |
| 11 | 安装mysql | `yum -y install mysql//客户端` `mysql -V` `yum -y install mysql-server  mysql-devel//服务端` |  |
| 12 | 安装php | `yum -y install php*` `php -v` `/etc/phpMyAdmin/config.inc.php` `vim /etc/httpd/conf.d/phpmyadmin.conf//此处略去一万字` |  |
| 13 | 安装mariadb | `yum install mariadb-server mariadb ` | http://www.runoob.com/mysql/mysql-install.html |
| 14 | 安装tale | `下载http://static.biezhi.me/tale-least.zip` `传到linux解压` `java -jar tale-least.jar` `http://180.76.113.98:9000` |  |

***

| 压缩 >> |
| --- |

|  |  |  |
| --- | --- | --- |
| 1 | 解压war | jar -xvf fileName.war |
| 2 | 解压zip | unzip fileName.war |
| 3 | 解压gz | tar -zxv -f xxx.tar.gz |

***

| 运行 >> |
| --- |

|  |  |  |
| --- | --- | --- |
| 1 | 运行war | java -jar fileName.war |
| 2 | 后台运行war | java -jar gitbucket.war & |
| 3 | 挂起运行war | nohup java -jar gitbucket.war |
| 4 | 杀进程 | kill %psId |
| 5 | 前台->后台暂停状态 | Ctrl+z |
| 6 | 后台暂停->运行 | bg %jobnum |

***

| 系统状态 >> |
| --- |

|  |  |  |
| --- | --- | --- |
| 1 | 查看进程 | ps |
| 2 | 查看后台任务 | jobs |
| 3 | 任务管理器 | top |

***

| 码农 >> |
| --- |

|  |  |  |
| --- | --- | --- |
| 1 | 访问gitbucket | http://180.76.113.98:8080/gitbucket |
| 2 | tomcat改端口 | `cd tomcat/conf` `vim server.xml` `找到port8080改成80` |
| 3 | tomcat改默认目录 | 在server.xml中`/Host>`上一行插入`<Context path="" docBase="../../myWeb" debug="0" reloadable="true" crossContext="true" />` |
