# Google Cloud 檔案上傳

### gradle

```kotlin 
implementation platform('com.google.cloud:libraries-bom:18.0.0')
compile 'com.google.cloud:google-cloud-storage'
```
### Sample Code

```kotlin 
  val credentials: GoogleCredentials = GoogleCredentials.fromStream(FileInputStream("/Users/jianzhi.wang/Desktop/iosKey/tsportCloudStorage.json"))
        .createScoped(Lists.newArrayList("https://www.googleapis.com/auth/cloud-platform"))
    val storage = StorageOptions.newBuilder().setCredentials(credentials).build().getService()
    val bucketName = "tsport"
    val blobId = BlobId.of(bucketName, "file")
    val blobInfo = BlobInfo.newBuilder(blobId).build()
    storage.create(blobInfo, "Binary data".toByteArray())
    ///Make public url
    storage.createAcl(blobId, Acl.of(Acl.User.ofAllUsers(), Acl.Role.READER))
    println("url=https://storage.googleapis.com/tsport/file")
  
```