# HBBASMClickTrack

通过ASM+Tranform插桩View.OnClickListener完成页面元素点击监听

支持注入三种方式实现View.OnClickListener协议:

*   lamda实现的

    >   ```
    >   findViewById(R.id.tv_lambda).setOnClickListener(v->{
    >       
    >   });
    >   ```

*   layout binding

    >   ```
    >   <TextView
    >       android:layout_width="wrap_content"
    >       android:layout_height="wrap_content"
    >       android:text="binding listener"
    >       app:layout_constraintBottom_toBottomOf="parent"
    >       app:layout_constraintLeft_toLeftOf="parent"
    >       app:layout_constraintRight_toRightOf="parent"
    >       app:layout_constraintTop_toTopOf="@id/tv_btn"
    >       android:onClick="toSecond"
    >       />
    >   ```

*   object

    >   ```
    >   findViewById(R.id.tv_btn).setOnClickListener(new View.OnClickListener(){
    >       @Override
    >       public void onClick(View view) {
    >           
    >       }
    >   });
    >   ```

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
        classpath 'com.hibobi.spmtrack:SPMClickTrack:1.0.0'

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
    implementation('com.hibobi.spmtrack:SPMTrackBase:1.0.0')
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

## Demo

```
public class SPMClickAspect implements SPMTrack.OnTrackListener{
    SPMClickAspect() {
        SPMTrack.sharedInstance().subscribe(this);
    }

    @Override
    public void onViewClick(View view) {
        Log.i("ASMTrack", "spm subscribe notify, view click:"+((TextView)view).getText());

    }

    @Override
    public void onTabClick(TabLayout.Tab tab) {
        Log.i("ASMTrack", "spm subscribe notify, tab on select:"+tab.getText());

    }
}
```