


# <font color="#314A56">Ktor Https設定</font><br /> 
### 1.打開終端機將取得的SSL憑證轉換成JKS

``` kotlin 
keytool 
-importkeystore 
-srckeystore /Users/jianzhi.wang/Desktop/bento2.pfx 
-destkeystore /Users/jianzhi.wang/Desktop/bento3.jks  
-srcstoretype PKCS12 -deststoretype JKS
```

### 2.終端機取得返回的key alias
``` kotlin 
Entry for alias te-524e9976-bcd8-4685-aa5b-359fea7a3dea successfully imported.
```
### 3.在application進行設定
``` kotlin 
 ktor {
    deployment {
        port = 80
        sslPort = 443
        port = ${?PORT}
    }
    application {
        modules = [com.orange.dataserver.MainKt.module]
    }

    security {
        ssl {
            keyStore = bento3.jks
            keyAlias = te-524e9976-bcd8-4685-aa5b-359fea7a3dea
            keyStorePassword = orangetpms
            privateKeyPassword = orangetpms
        }
    }
}
```
### 3.完成
