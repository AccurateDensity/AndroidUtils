                ***Android studio 打可运行jira包说明***

java mode构建

![image-20250504134737404](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250504134737404.png)

构建完成后要打包一个可运行的jira包需要对gradle.build进行配置

```
plugins {
    id 'java-library'
}
jar {
    duplicatesStrategy = DuplicatesStrategy.EXCLUDE
    archiveFileName = 'density.jar'
    manifest {
        attributes 'Main-Class': "com.kotlin.runjava.MyClass"
    }

    from {
        configurations.runtimeClasspath.collect { it.isDirectory() ? it : zipTree(it) }
    }
}
java {
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
}
```

然后使用这里进行打包。

![image-20250504134914131](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250504134914131.png)



jar包运行：

java -jar MyJar.jar arg0 arg1



java -cp MyJar.jar com.xxx.xxx.MyMainClass arg0 arg1