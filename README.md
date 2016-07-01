# android-library-gradle-publish
android library gradle publish 快速度将项目上传到JCenter上

##介绍
本项目包含一些Gradle脚本及属性文件

##项目配置
第一步：在你的root build.gradle文件添加
```
classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.2'
```
第二步：在你的library module 中的build.gradle文件后面添加
```
apply from: 'https://raw.githubusercontent.com/LiangMaYong/android-library-gradle-publish/master/library.gradle'
apply from: 'https://raw.githubusercontent.com/LiangMaYong/android-library-gradle-publish/master/bintray.gradle'
apply from: 'https://raw.githubusercontent.com/LiangMaYong/android-library-gradle-publish/master/install.gradle'
```
第三步：在项目gradle.properties中配置
```
BINTRAY_USER=*********
BINTRAY_APIKEY=*******************************
BINTRAY_GPG_PASSWORD=

PROJ_GROUP=com.github.liangmayong
#项目名称
PROJ_NAME=BintrayDemo
#项目版本
PROJ_VERSION=1.0.0

PROJ_WEBSITEURL=https://github.com/liangmayong/bintray-demo
PROJ_VCSURL=git@github.com:liangmayong/bintray-demo.git

#项目介绍
PROJ_DESCRIPTION= this is android library bintray-demo
#项目artifactId
PROJ_ARTIFACTID=bintray-demo

#开发者信息
DEVELOPER_ID=linagmayong
DEVELOPER_NAME=Liang Ma Yong
DEVELOPER_EMAIL=ibeam@qq.com
```
##编译和上传
执行 gradlew install 验证编译
```
gradlew install
```

执行 gradlew bintrayUpload 将库发布到 bintray.com
```
gradlew bintrayUpload
```

##使用格式
上面的例子最终在Android Studio中的引用形式为：
```
repositories {
    maven {
        url 'https://dl.bintray.com/{BINTRAY_USER}/maven/'
    }
}

......

dependencies {
    compile 'com.github.liangmayong:bintray-demo:1.0.0'
}
```
可以发现，它的格式是 PROJ_GROUP:PROJ_ARTIFACTID:PROJ_VERSION组成。


##常见问题
保持你的library module的名字同artifactId一样，否则会报错
```
Could not upload to 'https://*****.pom': HTTP/1.1 400 Bad Request [message:Unable to upload files: Maven group, artifact or version defined in the pom file do not match the file path '****.pom']
```

请注意链接到jcenter是一个只需做一次的操作。如果你对你的package做了任何修改，比如上传了一个新版本的binary，删除了旧版本的binary等等，这些改变也会影响到jcenter。不过毕竟你自己的仓库和jcenter在不同的地方，所以需要等待2－3分钟让jcenter同步这些修改。

同时注意，如果你决定删除整个package，放在jcenter仓库上的library不会被删除。它们会像僵尸一样的存在，没有人再能删除它了。因此我建议，如果你想删除整个package，请在移除package之前先在网页上删除每一个版本。




