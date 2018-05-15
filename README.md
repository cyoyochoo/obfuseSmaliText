## Android gradle plugin 3.0+ 多模块常量字符串混淆
forked from: https://github.com/Qrilee/obfuseSmaliText
#### 使用方法
* 将**hsaeObfuscateString_V2.0.jar**文件放在工程根目录，在根目录**build.gradle**文件中添加如下：
``` java 
allprojects {
    ...
    tasks.whenTaskAdded {task->
        if (task.name.contains('ReleaseJavaWithJavac')) {//Release版本开启混淆
            task.doLast {
                javaexec {
                    main = "-jar"
                    args = [
                            "../hsaeObfuscateString_V2.0.jar",
                            task.project.name,
                            task.outputs.files.last().path,
                            //指定要混淆的包名
                            "xxx.pkg",
                            //指定要混淆的包名
                            "xxx.pkg"
                    ]
                    jvmArgs '-Dfile.encoding=UTF-8'
                }
            }
        }
    }
}
```

