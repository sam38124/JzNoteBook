# How to sign in facebook with android

### 1.In gradle
```kotlin
 implementation 'com.facebook.android:facebook-login:5.15.3'
```
### 2.In Manifest
@string/facebook_app_id is your Application Id what you register on facebook!!
``` kotlin
  <meta-data
            android:name="com.facebook.sdk.ApplicationId"
            android:value="@string/facebook_app_id" />

        <activity
            android:name="com.facebook.FacebookActivity"
            android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
            android:label="T-sport" />
        <activity
            android:name="com.facebook.CustomTabActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />

                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />

                <data android:scheme="@string/fb_login_protocol_scheme" />
            </intent-filter>
        </activity>

```
### 3.Set Initialize

``` kotlin
FacebookSdk.sdkInitialize(applicationContext)
```
### 4.In fragement

``` kotlin
//First step
private var callbackManager: CallbackManager=CallbackManager.Factory.create()
//Second step
  LoginManager.getInstance().registerCallback(callbackManager,
            object : FacebookCallback<LoginResult> {
                override fun onSuccess(loginResult: LoginResult) {
                    val profile = Profile.getCurrentProfile()
                    var photo="https://graph.facebook.com/v3.3/${profile.id}/picture?height=300&width=300&migration_overrides=%7Boctober_2012%3Atrue%7D"
                    val id = "fb"+profile.id
                    val name = profile.name
                    Log.e("fb登入","登入成功")
                    handler.post { JzActivity.getControlInstance().toast("登入成功") }
                }

                override fun onCancel() {
                    Log.e("fb登入","取消登入")
                    handler.post { JzActivity.getControlInstance().toast("取消登入") }
                }

                override fun onError(exception: FacebookException) {
                    Log.e("fb登入","登入失敗->${exception.message}")
                    handler.post { JzActivity.getControlInstance().toast("登入失敗"+exception.message) }

                }
            })
//Third step
 override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        callbackManager.onActivityResult(requestCode, resultCode, data)
    }
//Fourth step
LoginManager.getInstance().logInWithReadPermissions(this, Arrays.asList("public_profile"))

```