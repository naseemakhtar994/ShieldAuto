[<img src="media/autoshield.png" width="400" />]() [<img src="media/name.png" width="200" />]()

# Disclaimer
 - This project is meant for a proof of concept, to check if it is feasible to have a single magic solution for Proguard configurations
 - Currently its a 0.0.X version. Please don't use it in a real environment. Its terrible.
 - Basically googled and copied the first result for each proguard. The point I wanted to convey was that a single source, when crowdsourced enough, could bring value. (And also that most of google’s first result when used without knowledge is valueless)
 - My imagination of a real case usage in the future would be something like this:
 ```gradle
 shieldConfig {  //inside build.config
    libraries {
        ...
        picasso {
            enableDownloader true
            useOkhttp3 true
            ...
        }
    }
}
 ```

# ShieldAuto
[![CI status](https://img.shields.io/badge/start%20with-why%3F-brightgreen.svg?style=flat)](https://github.com/wotomas/ShieldAuto) ![Download](https://api.bintray.com/packages/wotomas/maven/ShieldAuto/images/download.svg)

We were tired of searching for proguard configs for every library that needed to be included in release APK. By using [ShieldAuto](https://github.com/wotomas/ShieldAuto/) developers don't have to worry about checking proguard config file to check if setup is correct for each imported libraries.

[ShieldAuto](https://github.com/wotomas/ShieldAuto/) checks your dependencies extension defined in the build.gradle file to check for matching proguard and to generate a simple proguard config file. In short, [ShieldAuto](https://github.com/wotomas/ShieldAuto/) is a Java based Gradle plugin to manage proguard config for release build.
 
This is still a premature version and any helps are welcome. Test cases, refactoring, optimization, bug fixes and adding any libraries are welcome. Current State diagram is as following: 

# State Diagram
[<img src="media/state_diagram.png" width="800" />]()

# How to use?
```gradle
// modify project level build.gradle
buildscript {
    repositories {
        ... 
        maven {
            url  "https://dl.bintray.com/wotomas/maven"
        }
    }
    dependencies {
        ...
        classpath 'info.kimjihyok:ShieldAuto:0.0.4'
    }
}
```

```gradle
// add ShieldAuto plugin below application plugin 'com.android.application' plugin
apply plugin: 'info.kimjihyok.ShieldAuto'

android {
    ...  
    buildTypes {
        release {
            // apply sheidlAuto.auto() to proguardFiles configuration
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro', shieldAuto.auto()
        }
    }
```

# Note
Currently ShieldAuto is able to check for libraries imported only through *compile* configuration (which is deprecated and should be replaced with *implementation*, but direct access is not allowed right now). I would love for additional help with this issue. 

# Supported Libraries
* [BottomBar](https://github.com/roughike/BottomBar/)
* [Butterknife](http://jakewharton.github.io/butterknife/)
* [Calligraphy](https://github.com/chrisjenx/Calligraphy/)
* [Crashlytics](http://try.crashlytics.com/sdk-android/)
* [Flurry](https://github.com/flurry/flurry-android-sdk/)
* [Fresco](https://github.com/facebook/fresco/)
* [Glide](https://github.com/bumptech/glide/)
* [Gson](https://code.google.com/p/google-gson/)
* [Square OkHttp](http://square.github.io/okhttp/)
* [Square Picasso](https://github.com/square/picasso)
* [Square Retrofit](http://square.github.io/retrofit/)
* [RxJava](https://github.com/ReactiveX/RxJava/wiki/The-RxJava-Android-Module)
* [Stetho](https://github.com/facebook/stetho/)

Request for additional libraries could be submitted through issues. Pull requests are always welcome.

# License
Copyright (C) 2018 Kim Jihyok

See the file [License](https://github.com/wotomas/ShieldAuto/blob/master/LICENSE)

# Development and Contribution
We are open for any contributions. Please use the issue tickets for communication before sending pull requests.

# Thanks to
<div>Icons made by <a href="https://www.flaticon.com/authors/maxim-basinski" title="Maxim Basinski">Maxim Basinski</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>
