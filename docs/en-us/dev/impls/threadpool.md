# ThreadPool Extension

## Summary

Thread pool strategy extension for service provider. When server receives one request, it needs a thread from thread pool to execute business logic in service provider.

## Extension Interface

`org.apache.dubbo.common.threadpool.ThreadPool`

## Extension Configuration

```xml
<dubbo:protocol threadpool="xxx" />
<!-- default configuration, it will take effect when threadpool attribute is not specified in <dubbo:protocol> -->
<dubbo:provider threadpool="xxx" />
```

## Existing Extension

* `org.apache.dubbo.common.threadpool.FixedThreadPool`
* `org.apache.dubbo.common.threadpool.CachedThreadPool`

## Extension Guide

Directory layout:

```
src
 |-main
    |-java
        |-com
            |-xxx
                |-XxxThreadPool.java (ThreadPool implementation)
    |-resources
        |-META-INF
            |-dubbo
                |-org.apache.dubbo.common.threadpool.ThreadPool (plain text file with the content: xxx=com.xxx.XxxThreadPool)
```

XxxThreadPool.java：

```java
package com.xxx;
 
import org.apache.dubbo.common.threadpool.ThreadPool;
import java.util.concurrent.Executor;
 
public class XxxThreadPool implements ThreadPool {
    public Executor getExecutor() {
        // ...
    }
}
```

META-INF/dubbo/org.apache.dubbo.common.threadpool.ThreadPool：

```properties
xxx=com.xxx.XxxThreadPool
```

