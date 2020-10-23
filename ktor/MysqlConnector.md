# MysqlConnector

That is a sample class to show how to connect Mysql by java or kotlin!!

```kotlin

class MysqlConnect(var root:String= "jdbc:mysql://sample:3306?autoReconnect=false&allowPublicKeyRetrieval=true&useSSL=false&serverTimezone=UTC") {
    var conn: Connection
    var stmt: Statement
    init {
        Class.forName("com.mysql.jdbc.Driver")
        conn = DriverManager.getConnection(root, PublicBeans.dataUSER, PublicBeans.dataPASS)
        stmt = conn.createStatement()
    }
    fun close() {
        conn.close()
        stmt.close()
    }
}

interface callback {
    fun callback(rs: ResultSet)
}

fun String.mySqlQuery(callback: callback){
    val a= MysqlConnect()
    val rs=a.stmt.executeQuery(this)
    while (rs.next()){
        callback.callback(rs)
    }
    a.close()
}

```
