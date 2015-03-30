Gradle Watch Plugin 0.2.0-SNAPSHOT [![Build Status](https://travis-ci.org/bluepapa32/gradle-watch-plugin.png?branch=develop)](https://travis-ci.org/bluepapa32/gradle-watch-plugin)
=========================

Run predefined tasks whenever watched file patterns are added, changed or deleted.


Requirements
------------

- Oracle JDK7+
- Gradle 1.9+


Usage
-----

To use the Watch plugin, include in your build script:

~~~
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.bluepapa32:gradle-watch-plugin:0.2.0-SNAPSHOT'
    }
}   

apply plugin: 'watch'
~~~

Then [configure](#configuration) at least one [`WatchTarget`](https://github.com/bluepapa32/gradle-watch-plugin/blob/master/src/main/java/com/bluepapa32/gradle/plugins/watch/WatchTarget.java).

Tasks
-----

The Watch plugin adds the following tasks to the project.

Table 1. Watch plugin - tasks

|Task name       |Depends on|Type     |Description                                                                       |
|:--------------:|:--------:|:-------:|----------------------------------------------------------------------------------|
|watch           |-         |WatchTask|Run predefined tasks whenever watched file patterns are added, changed or deleted.|


<a name="configuration"></a>Configuration
-------------

In order for the Watch plugin to be useful, at least one [`WatchTarget`](https://github.com/bluepapa32/gradle-watch-plugin/blob/master/src/main/java/com/bluepapa32/gradle/plugins/watch/WatchTarget.java) must be configured using arbitrary named domain objects.

The watch target encapsulate which files or directories to watch and which tasks to execute when something has changed. For that, the watch target expose methods `files(`[`FileCollection`](http://gradle.org/docs/current/javadoc/org/gradle/api/file/FileCollection.html)`)` and `tasks(String...)`.  

~~~
watch {

    java {
        files files('src/main/java')
        tasks 'compileJava'
    }

    resources {
        files fileTree(dir: 'src/main/resources',
                       include: '**/*.properties')
        tasks 'processResources'
    }

    hoge {
        files files('foo/bar', 'foo/boo/hoo.txt')
        tasks 'hogehoge', 'hugohugo'
    }
}
~~~

