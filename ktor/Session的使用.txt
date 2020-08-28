

# <font color="#314A56">Ktor Session的使用</font><br /> 
### 1.設定要儲存的類型!

``` kotlin 
class Cookie(val name: String, val value: Int)
```

### 2.於HttpClient中添加
``` kotlin 
  val client = HttpClient(Apache) {
        install(Sessions){
            cookie<Cookie>("test")
        }
    }
```
### 3.資料取得
#### (類行為Any不是泛型需自行轉義!!)
``` kotlin 
// 在caller中呼叫
  get("/getCookie"){
            call.sessions.get("test") as Cookie
        }
```
### 4.資料儲存
``` kotlin 
//在caller中呼叫
  get("/setCookie"){
            call.sessions.set("test",Cookie("value","value"))
        }
```