---
title: Android-Studio使用阿里云镜像解决依赖下载慢的问题
date: 2019-12-12 23:12:07
toc: true
categories: Android
tags: Android Studio
---

## 使用阿里云的镜像替换默认的镜像

国内由于众所周知的原因导致Android Studio依赖下载过慢，使用阿里云的镜像能够有效解决这个问题
<!--more-->

``` groovy
buildscript {

    repositories {
        maven{ url 'http://maven.aliyun.com/nexus/content/groups/public/'}
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.2'


        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        maven{ url 'http://maven.aliyun.com/nexus/content/groups/public/'}
        google()
        jcenter()
    }
}
task clean(type: Delete) {
    delete rootProject.buildDir
}
```

