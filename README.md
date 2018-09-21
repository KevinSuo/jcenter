# 发布Android Library到jCenter
步骤如下：
### bintray/jcenter 部分
1. 到 https://bintray.com/signup/oss 注册个人账号

2. 在 bintray 创建 maven 资源库

>  登陆 bintray后点击 “Add New Repository”

>  maven库的名字要记住 随后需要用到

3. 使用gpg生成密钥
>  gpg --gen-key
### Android Studio部分
1. 在根目录下的build.gradle文件添加如下代码
```
dependencies {
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.4'
        classpath 'com.github.dcendents:android-maven-plugin:1.2'
    }
```
2. 在根目录下的local.properties文件添加如下代码
```
bintray.user=用户名
bintray.apikey=apiKey
bintray.gpg.password=gpg生成的密钥的密码
```
3. 在需要发布的library下的build.gradle中配置
```
ext {
  bintrayRepo = 'maven' // 远程仓库名 
  bintrayName = 'kstabpager' // 包名 全部小写 可包含数字 - _ .
  libraryName = 'KsTabPager'
  
  // implementation 'com.kevinsuo:kstabpager:0.0.2'
  publishedGroupId = 'com.kevinsuo' // 组名
  artifact = 'kstabpager' //当前组件名
  libraryVersion = '0.0.2' // 版本号 每次发布都需要变化
  
  siteUrl = 'https://github.com/KevinSuo/KsTabPager'
  gitUrl = 'https://github.com/KevinSuo/KsTabPager.git'
  libraryDescription = 'A TabPager Library for Android' // 库描述
}

// 文件底部添加
if(rootProject.file('local.properties').exists()) {
  apply from: 'https://raw.githubusercontent.com/KevinSuo/jcenter/master/jcenter_maven_publish.gradle'
}

```

### 发布
```
./gradlew install 
./gradlew bintrayUpload

```

> 需要注意的是 这样只是发库发布到了 bintray上，并没有同步到jcenter,发布成功后需要到bintray上找到发布的库，并在同一页找到“ADD to JCenter"点击后发送同步申请，
> 内容可为空
