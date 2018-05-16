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
                                //指定要混淆的包名或类名
                                "com.xxx", //混淆com.xxx包名下所有字符串
                                "com.yyy.MainActivity", //混淆com.yyy.MainActivity类中所有字符串
                                ...
                        ]
                        jvmArgs '-Dfile.encoding=UTF-8'
                    }
                }
            }
        }
    }
    ```
* 指定不混淆字符串的类
  * 添加 **_com.hsae.yoyochoo.annotation.StringIgnore_** 注解即可
  ``` java
    @StringIgnore
    public class Ignore {
        ...
    }
    ```
  * 使用 **_com.hsae.yoyochoo.annotation.StringIgnore_** 注解 需要依赖 **_StringIgnore.jar_**
  ``` java
    implementation files('libs/StringIgnore.jar')
  ```
  
  ## 更新日志
  #### V2.0
  * 新增指定**包名**或**类**中字符串混淆
  * 新增指定类下字符串不混淆（注解标识）
  #### V1.0
  * 新增多模块支持