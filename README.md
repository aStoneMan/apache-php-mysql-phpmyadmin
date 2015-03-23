# apache-php-mysql-phpmyadmin
how to build a exploitation environment for php   <br> 
1.安装apache    <br>
2.把D:\mynerv\apache\bin加入到Path中（就可以通过控制台控制apache了	//netstat -an   是用来查看端口的使用情况的   
							   //netstat -anb	查看用每个端口的程序   
3.可以配置虚拟目录	在httpd.conf中注销DocumentRoot	如果不去掉都可以访问   <br>
   <br>
#   <br>
		<IfModule dir_module> 
		   DirectoryIndex index.html			//在这个后面加上虚拟目录   <br>
		</IfModule>   <br>
   <br>
#配置虚拟目录   <br>
		<IfModule dir_module>   <br>
			#direcotory 相当于是欢迎页面
			DirectoryIndex index.html index.htm index.php
			#你的站点别名
			Alias /apache "E:/myweb"
			<Directory E:/myweb>
			#这是访问权限设置
			Order allow,deny
			Allow from all
			</Directory>
		</IfModule>


4.可以配置虚拟主机

在httpd.conf中注销DocumentRoot
找到Include conf/extra/httpd-vhosts.conf  启用它
打开httpd-vhosts.conf 做配置

在最后加上

		#配置我们自己的虚拟主机

		<VirtualHost 127.0.0.1:80>
			DocumentRoot "e:/myweb1"
			DirectoryIndex index.html index.htm index.php
			<Directory />
			Options FollowSymLinks
			AllowOverride None
			Order allow,deny
			Allow from all
			</Directory>
		</VirtualHost>


5.配置PHP
	

	解压即可
		#让apache载入php处理模块
		LoadModule php5_module D:\mynerv\php-5.4.37\php5apache2_2.dll
		PHPIniDir "D:\mynerv\php-5.4.37"
		AddType application/x-httpd-php .php .phtml


把php安装目录下的php.ini-development
改名为php.ini
修改php.ini
搜索extension_dir
启用extension_dir = "ext" 修改为extension_dir = "D:\mynerv\php-5.4.37\ext"

在D:\mynerv\apache\htdocs下写一个测试文件
 		<?php 
			phpinfo();
 		?>
即可测试是否成功

6.安装MySQL

在Manual Setting选择并增加数值

在Manual Selected Defaut Charcater Set改成UTF-8

在please set the security options 设置mysql数据库的用户密码
就结束了

在php.ini
激活			;extension=php_mysql.dll
			;extension=php_mysqli.dll

测试MySQL是否可用
1.写一段php代码测试

		<?php 
			$conn==mysql_connect("localhost","root","admin");
			if($conn){
				echo "ok";
			}else{
				echo "fail";
			}
		 ?>
