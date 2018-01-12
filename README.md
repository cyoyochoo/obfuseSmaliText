## Android gradle plugin 3.0+ 多模块常量字符串混淆
#### 使用方法
* 将**hsaeObfuscateString_V1.0.jar**文件放在工程根目录，在根目录**build.gradle**文件中添加如下：
``` java 
allprojects {
    ...
    tasks.whenTaskAdded {task->
        if (task.name.contains('JavaWithJavac')) {
            task.doLast {
                javaexec {
                    main = "-jar"
                    args = [
                            "../hsaeObfuscateString_V1.0.jar",
                            task.project.name,
                            task.outputs.files.last().path
                    ]
                    jvmArgs '-Dfile.encoding=UTF-8'
                }
            }
        }
    }
}
```

