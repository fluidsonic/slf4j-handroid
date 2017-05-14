[![Build Status](https://travis-ci.org/mvysny/slf4j-handroid.svg?branch=master)](https://travis-ci.org/mvysny/slf4j-handroid)

# slf4j-android fixed

Tired of slf4j-android not logging your debug messages? Tired of android logger hiding your UnknownHostException or other exceptions not appearing? Use this instead of the built-in slf4j-android logger.

Features

* Shows DEBUG messages during the development: http://jira.qos.ch/browse/SLF4J-314
* Does not hide any exceptions, even exceptions hidden by buggy Android Studio 1.5. Fixes https://code.google.com/p/android/issues/detail?id=195164 https://code.google.com/p/android/issues/detail?id=194446 http://stackoverflow.com/questions/28897239/log-e-does-not-print-the-stack-trace-of-unknownhostexception
* Supports Crashlytics; when Crashlytics jar is included in your project then slf4-handroid will
  automatically log using `Crashlytics.log()` and `Crashlytics.logException()` instead of using plain Android logger.

## Using with your project

slf4j-handroid is now at jcenter, so all you have to do is to add this to your project dependencies:
```groovy
dependencies {
  compile 'sk.baka.slf4j:slf4j-handroid:1.7.25'
}
```

If this won't work, add the jcenter repo:
```groovy
repositories {
    jcenter()
}
```

Then, just update the `HandroidLoggerAdapter.DEBUG` field to appropriate value. Good practice is to log debug during development,
while not logging debug messages during production. You can achieve this by adding a constructor to your android.app.Application and:

```
HandroidLoggerAdapter.DEBUG = BuildConfig.DEBUG;
```

Then, replace all calls to Android built-in `Log` class by slf4j logging, for example:

```java
public class YourClass {
  private static final Logger log = LoggerFactory.getLogger(YourClass.class);
  public void foo() {
    log.error("Something failed", new RuntimeException("something"));
  }
}
```
