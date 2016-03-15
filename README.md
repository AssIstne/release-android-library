release-android-library
=======================
用作将本地Android-Library包装成maven工程, 这是因为[bintray](https://bintray.com/)上传库到Jcenter要求:
> Before you can include your package in JCenter, the following requirements must be met:

> 1. The package must be in a Maven repository and must contain Maven sources.

> 2. The path of the files (entered in the Upload Files form of the Version page) must conform to Maven standards (the Group ID and Artifact ID combination must be unique, etc.; for more information about Maven standards, consult the appropriate Maven documentation)

> 3. Every version within the package that includes files must also include a valid POM file.

因此需要这个脚本生成合适的包(.zip)直接上传到bintray并发布至Jcenter.参考该[blog](https://medium.com/@tigr/how-to-publish-your-android-studio-library-to-jcenter-5384172c4739#.cxq364us2)

Remote script to create a maven compatible release of an android library (aar). This release comes in a zip or exploded form and is only created locally inside your own build folder. You can these use these files to release to JCenter or Maven Central.

Matching blog post here: [blog.blundell-apps.com/locally-release-an-android-library-for-jcenter-or-maven-central-inclusion/](http://blog.blundell-apps.com/locally-release-an-android-library-for-jcenter-or-maven-central-inclusion/)

####adding to your library
```
apply plugin: 'com.android.library'

ext {
    PUBLISH_GROUP_ID = 'com.blundell'
    PUBLISH_ARTIFACT_ID = 'example-library-name'
    PUBLISH_VERSION = '1.0.0'
}

android {
    // configs, flavors etc
}

dependencies {
    // dependencies
}

// Copy the file locally and use
apply from: 'android-release-aar.gradle'
// or use the remote copy to keep update with latest changes
apply from: 'https://raw.githubusercontent.com/blundell/release-android-library/master/android-release-aar.gradle'
```


####useage

`./gradlew clean build generateRelease`

####example output


```
 :engine:zipRelease
 :engine:generateRelease
 Release 1.0.0 can be found at /Users/Blundell/Developer/git_repo/ExampleAndroidLibrary/build/release/1.0.0/
 Release 1.0.0 zipped can be found /Users/Blundell/Developer/git_repo/ExampleAndroidLibrary/build/release-1.0.0.zip

 BUILD SUCCESSFUL
 
 Total time: 23.609 secs
```
