Logging Interceptor
===================

An [OkHttp interceptor][1] which logs HTTP request and response data.

```java
HttpLoggingInterceptor logging = new HttpLoggingInterceptor();
logging.setLevel(Level.BASIC);
OkHttpClient client = new OkHttpClient.Builder()
  .addInterceptor(logging)
  .build();
```

You can change the log level at any time by calling `setLevel()`.

To log to a custom location, pass a `Logger` instance to the constructor.
```java
HttpLoggingInterceptor logging = new HttpLoggingInterceptor(new Logger() {
  @Override public void log(String message) {
    Timber.tag("OkHttp").d(message);
  }
});
```

**Warning**: The logs generated by this interceptor when using the `HEADERS` or `BODY` levels have
the potential to leak sensitive information such as "Authorization" or "Cookie" headers and the
contents of request and response bodies. This data should only be logged in a controlled way or in
a non-production environment.

You can redact headers that may contain sensitive information by calling `redactHeader()`.
```java
logging.redactHeader("Authorization");
logging.redactHeader("Cookie");
```

Download
--------

```kotlin
implementation("com.squareup.okhttp3:logging-interceptor:4.1.0")
```



 [1]: ../INTERCEPTORS.md