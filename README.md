# Sherlock
Sherlock is a shorthand for "Network Sherlock Holmes" a simple lib that you can plug into your http client to capture everything around network requests, which then provides you or your QA team member with enough info about requests.

## Why not use a proxy?
- Sherlock is not to replace your normal proxy like. Charles Proxy for example, however the right question would be .. how many times did something go wrong while QAing your app then you realized that it's too late as you were not proxying?
## How to use it?
it's a very simple and straight forward for v.0.X only OKHttp is supported.
1. Add the dependency to your gradle.

```groovy
allprojects {
    repositories {
	maven { url 'https://jitpack.io' }
    }
}
```
```groovy
dependencies {
    debugImplementation 'com.github.shehabic.sherlock:sherlock:v0.11.0'
    releaseImplementation 'com.github.shehabic.sherlock:sherlock-no-op:v0.11.0'
    
    // the next part is important (until there is a better solution)
    implementation "android.arch.persistence.room:runtime:$architecture_version"
    // if your project uses kotlin:
    kapt "android.arch.persistence.room:compiler:$architecture_version"
    // or if your project doesn't use kotlin:
    annotationProcessor "android.arch.persistence.room:compiler:$architecture_version"
}
```
2. on app startup initialize sherlock by ``` NetworkSherlock.getInstance().init(appContext) ```
3. then attach Sherlock's okhttp intercepter to your OKHttpClient as follows:

**Kotlin**
```kotlin
val client: OkHttpClient = OkHttpClient.Builder().addInterceptor(SherlockOkHttpInterceptor()).build()
```
**Java**
```java
OkHttpClient client = new OkHttpClient.Builder().addInterceptor(new SherlockOkHttpInterceptor()).build()
```

## Advanced options
Show/Hide anchor - Show/Hide network activity indicator
**Kotlin**
```kotlin
NetworkSherlock
  .getInstance(NetworkSherlock.Config(showAnchor = true, showNetworkActivity = true))
  .init(this)
```
## Pause/Resume Recording
```kotlin
NetworkSherlock.getInstance().pauseRecording()
NetworkSherlock.getInstance().resumeRecording()
``` 
## Check the demo app which is using many feature of Sherlock's lib

![](https://github.com/shehabic/Sherlock/blob/master/screenshots/sherlock_preview.gif?raw=true)

## Roadmap
### Enahnce Export Format
  - Export whole sessions in a machine readable format
  - Export request in cURL format
  - Export standard http-request format
  - Export Charles-Proxy files for sessions 
