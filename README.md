# HBBASMClickTrack

通过ASM+Tranform插桩View.OnClickListener完成页面元素点击监听



# 使用说明



## 工程配置

修改工程级build.gradle， 添加maven及plugin依赖

```
buildscript {
    
    repositories {
        google()
        jcenter()
        // 添加maven依赖
        maven { 
            url "https://raw.githubusercontent.com/hbbchenzhiqian/HBBASMClickTrack/master" 
        }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:4.0.2'
        // 增加plugin依赖
        classpath 'com.hibobi.spmtrack:SPMClickTrack:0.0.1'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        
		// 添加maven依赖
		maven {
            url "https://raw.githubusercontent.com/hbbchenzhiqian/HBBASMClickTrack/master" 
        }
    }
}
```

修改项目级build.gradle，应用plugin并添加依赖com.hibobi.spmtrack:SPMTrackBase:0.0.1

```
apply plugin: 'com.android.application'
// 应用plugin
apply plugin: 'spmclicktrack'

android {
    compileSdkVersion 31
    defaultConfig {
        applicationId "com.gavin.asmdemo"
        minSdkVersion 15
        targetSdkVersion 31
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    //....
    implementation('com.hibobi.spmtrack:SPMTrackBase:0.0.1')
}

```



## API

### 订阅追踪事件

```
SPMTrack.sharedInstance().subscribe(this);
```

### 取消订阅

```
SPMTrack.sharedInstance().unsubscribe(this);
```