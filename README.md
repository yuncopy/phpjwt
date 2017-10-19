### 免责声明
决不应将此代码用于生产就绪的应用程序，也不应在生产服务器上执行。没有安全检查和/或确认被执行。此代码仅用于教育目的，具有展示基本功能的范围。性能、效率、安全性或重用性不是优先事项。
### 安装
运行'composer install'来安装所有库依赖项。
请用所需的签名密钥和MySQL数据库凭据创建一个配置文件。你可以使用文件`config/config.php.dist`作为模板。
另外在数据库中创建以下表：
```
SET FOREIGN_KEY_CHECKS=0;

-- ----------------------------
-- Table structure for users
-- ----------------------------
DROP TABLE IF EXISTS `users`;
CREATE TABLE `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(255) NOT NULL,
  `password` varchar(255) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `username` (`username`)
) ENGINE=MyISAM AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of users
-- ----------------------------
INSERT INTO `users` VALUES ('1', 'root', '$2y$10$AUCMRch7kz47u4zbOSGkyetJjTKJOxxSfEEU2cEMX41grX639rizm');

```
“id”和“用户名”字段应该非常直接。的`密码`场产生使用[ ` password_hash() ` ]（http://php.net/manual/en/function.password-hash.php）功能的PHP
`echo password_hash('qwer@123',PASSWORD_DEFAULT);`

- 原始代码案例：https://github.com/tecnom1k3/sp-simple-jwt
- 执行流程：http://blog.csdn.net/liuwenbiao1203/article/details/52351772
- 参数说明：http://www.cnblogs.com/zjutzz/p/5790180.html
`注意 ：
"iat" => time(),                #非必须。issued at。 token创建时间，unix时间戳格式
"nbf" => time()+10,             # 非必须。not before。如果当前时间在nbf里的时间之前，则Token不被接受；创建时间十秒后才会被接受，否则报错Cannot handle token prior to 2017-10-19T05:31:08+0000
"exp" => time()+10+60,           #非必须。expire 指定token的生命周期。unix时间戳格式
`