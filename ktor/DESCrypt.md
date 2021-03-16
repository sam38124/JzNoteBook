# How to encrypt password and stored in database and decrypt password?

### Sample Code

```kotlin
//单例
object DESCrypt{
    //des加密
    fun encrypt(input:String,password:String): ByteArray {
        //1.创建cipher
        val c = Cipher.getInstance("DES")
        //2.初始化cipher(参数1:加密/解密模式)
        val kf = SecretKeyFactory.getInstance("DES")
        val keySpec = DESKeySpec(password.toByteArray())

        val key: Key? = kf.generateSecret(keySpec)
        c.init(Cipher.ENCRYPT_MODE, key)
        //3.加密/解密
        val encrypt = c.doFinal(input.toByteArray())
        return encrypt
    }
    //des解密
    fun decrypt(input:ByteArray,password:String): ByteArray {
        //1.创建cipher
        val c = Cipher.getInstance("DES")
        //2.初始化cipher(参数1:加密/解密模式)
        val kf = SecretKeyFactory.getInstance("DES")
        val keySpec = DESKeySpec(password.toByteArray())

        val key: Key? = kf.generateSecret(keySpec)
        c.init(Cipher.DECRYPT_MODE, key)
        //3.加密/解密
        val encrypt = c.doFinal(input)
        return encrypt
    }
}
````