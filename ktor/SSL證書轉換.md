项目中因为使用环境和语言不通，需要将证书进行转换，下面我们就展示一下如何将server.crt和server.key转换为.jks证书。

各种证书格式参考《SSL 证书格式普及，PEM、CER、JKS、PKCS12》

第一步
1, 根据server.crt和server.key生成pkcs12证书
生成过程输入的密码就是keypass
openssl pkcs12 -export -in server.crt -inkey server.key -out mycert.p12 -name abc -CAfile myCA.crt
这时我输入：a123456 （因此c123456就是我的keypass）， name就是别名， 我的别名是abc


第二步
2, 将上一步的mycert.p12证书转换为jks证书
deststorepass就是将来的storepass
keytool -importkeystore -v -srckeystore mycert.p12 -srcstoretype pkcs12 -srcstorepass a123456 -destkeystore Aserver.keystore -deststoretype jks -deststorepass b123456

我上一步中的keypass是a123456，同时设置storepass 为b123456
————————————————
版权声明：本文为CSDN博主「russle」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/russle/article/details/99694465