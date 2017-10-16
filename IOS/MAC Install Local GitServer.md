## gitosis步骤:(放弃)```
注:mac自带git和phyon参考: http://www.cnblogs.com/weijingyun/p/4716858.html	1.	git --version	2.	python --version	3.	git clone https://www.github.com/tv42/gitosis.gitCloning into 'gitosis'...remote: Counting objects: 661, done.remote: Total 661 (delta 0), reused 0 (delta 0), pack-reused 661Receiving objects: 100% (661/661), 118.13 KiB | 12.00 KiB/s, done.Resolving deltas: 100% (430/430), done. 	1.	cd /Users/jia/gitosis  	1.	sudo python setup.py install 	1.	cd~ 	1.	ssh-keygen -t rsaGenerating public/private rsa key pair.Enter file in which to save the key (/Users/jia/.ssh/id_rsa): Enter passphrase (empty for no passphrase): Enter same passphrase again: Your identification has been saved in /Users/jia/.ssh/id_rsa.Your public key has been saved in /Users/jia/.ssh/id_rsa.pub.The key fingerprint is:SHA256:ICnhZA09KjO+GASLRbf4GLnWtvd/eQ8a4e8hBE/+M7s jia@localhostThe key's randomart image is:+---[RSA 2048]----+| .*+.            ||.+.=+o           ||oo*.+..   . .    ||*..B . .   =     ||o++ +   S   =    ||.o . .     o o   ||... . .     +.*  ||..   . .    o=.* ||        .....oEo.|+----[SHA256]-----+ 	1.	cd /Users/jia/.ssh  	1.	lsgithub_rsa github_rsa.pub id_rsa id_rsa.pub known_hosts 	1.	放弃;
```



## gitblit步骤:(成功)> 参考: http://blog.csdn.net/pony_maggie/article/details/508801421.	下载

	```	a.	首选 http://gitblit.com/ 	b.	备选 		i.	http://mac.softpedia.com/dyn-postdownload.php/b5759a62cb81ab1b5bdbe64048d77f0c/58f7274a/21655/0/1?tsf=0		ii.	http://akamai.bintray.com/15/155cf8af49c76fbe6ea73383462c468fa8d69bad?__gda__=exp=1492592617~hmac=25a33212c3825c0242eebe0f8fbe3a746b30d85ec4e3db8bbc72ca69c47cf621&response-content-disposition=attachment%3Bfilename%3D%22gitblit-1.6.2.tar.gz%22&response-content-type=application%2Foctet-stream&requestInfo=U2FsdGVkX18qTwH5n-lYZI_DgnE1HLwWdfOYG369bLD6nwt-l7xqRTRjtWsHU5kw5FrMYVS-gikf0J1S5byJ7Lavcooo-T9ZwGjfM05YIQT6vc4oazsJ1tH9_B9s5itTtttueyk7haNG9NhNSUzpYpv_99n2QL9E2r0H0O1ChtoNrvuyiJxLWol_Ipy4bGddiZJN4C35LkyH_sIglH9Hzet-58JdmRxpcJE7cjimJ1U
	```
	2.	创建git根文件夹/Users/jia/Desktop/gitblit/repositoryFolder3.	打开defaults.properties

	![](assets/1.png)
	4.	配置路径:

	```	#git.repositoriesFolder = ${baseFolder}/git	git.repositoriesFolder = /Users/jia/Desktop/gitblit/repositoryFolder	```
5.	配置端口

	```	#server.httpPort = 0	server.httpPort = 7070
	```
 	6.	运行:

	```	localhost:gitosis jia$ cd /Users/jia/Desktop/gitblit/gitblit-1.8.0 	localhost:gitblit-1.8.0 jia$ ./gitblit.sh
	```
7.	访问Web后台:
	<http://localhost:7070> user:admin pwd:admin 8.	用mac的github客户端打开项目	![](img/2.png)




## github和gitblit指向到同一项目文件夹;	1.	在gitblit创建projectParent;	2.	在github创建projectSon;	3.	将projectSon放到projectParent文件夹下;然后移projectSon下的.git文件夹到别处去;	4.	将projectSon提交同步到projectParent项目;	5.	将projectSon下的.git移回来;	6.	完成;
 
