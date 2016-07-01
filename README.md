# android-library-gradle-publish
android library gradle publish 快速度将项目上传到JCenter上

##介绍
本项目包含一些Gradle脚本及属性文件

##规范说明
保持你的library module的名字同artifactId一样，否则会报错
```
Could not upload to 'https://*****.pom': HTTP/1.1 400 Bad Request [message:Unable to upload files: Maven group, artifact or version defined in the pom file do not match the file path '****.pom']
```
##项目配置
第一步：在你的library module 中的build.gradle文件后面添加
```
apply from: 'https://raw.githubusercontent.com/LiangMaYong/android-library-gradle-publish/master/library.gradle'
apply from: 'https://raw.githubusercontent.com/LiangMaYong/android-library-gradle-publish/master/bintray.gradle'
apply from: 'https://raw.githubusercontent.com/LiangMaYong/android-library-gradle-publish/master/install.gradle'
```
第二步：在项目gradle.properties中配置
```
BINTRAY_USER=*********
BINTRAY_APIKEY=*******************************
BINTRAY_GPG_PASSWORD=

PROJ_GROUP=com.github.liangmayong
PROJ_VERSION=1.0.0
PROJ_NAME=BintrayDemo
PROJ_WEBSITEURL=https://github.com/liangmayong/bintray-demo
PROJ_VCSURL=git@github.com:liangmayong/bintray-demo.git
PROJ_DESCRIPTION=this is android library bintray-demo
PROJ_ARTIFACTID=bintray-demo

DEVELOPER_ID=linagmayong
DEVELOPER_NAME=Liang Ma Yong
DEVELOPER_EMAIL=ibeam@qq.com
```
在Terminal中输入命令
```
gradlew install
```
如果出现 BUILD SUCCESSFUL,说明成功了一半了，下一步就是上传了，在在Terminal中输入命令
```
gradlew bintrayUpload
```
如果出现 BUILD SUCCESSFUL，说明上传到bintray.com成功了，登录bintray.com，提交到JCenter等待审核就可以了

##使用格式
上面的例子最终在Android Studio中的引用形式为：
```
dependencies {
    compile 'com.github.liangmayong:bintray-demo:1.0.0'
}
```
可以发现，它的格式是 PROJ_GROUP:PROJ_ARTIFACTID:PROJ_VERSION组成。





