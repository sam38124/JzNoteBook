# SqliteConnector

That is a sample class to show how to connect sqlite by java or kotlin!!

```kotlin
class SqLiteConnector(var tableName:String) {
    var conn: Connection
    var stmt: Statement
    init {
        val frout="chatRout"
        val file= File(frout)
        if(!file.exists()){
            file.mkdir()
        }
        val dbRout=File("chatRout/${tableName}.db")
        if(!dbRout.exists()){
            dbRout.createNewFile()
        }
        val strin="jdbc:sqlite:${dbRout.absolutePath}"
        Class.forName("org.sqlite.JDBC");
        conn = DriverManager.getConnection(strin)
        stmt = conn.createStatement()
    }
    fun close() {
        conn.close()
        stmt.close()
    }
}

fun String.sqLiteUpdate( tableName: String){
    val a= SqLiteConnector(tableName)
    a.stmt.executeUpdate(this)
    a.close()
}

fun String.sqLiteQuery(tableName: String,callback: callback){
    val a= SqLiteConnector(tableName)
    val rs=a.stmt.executeQuery(this)
    while (rs.next()){
        callback.callback(rs)
    }
    a.close()
}


```
