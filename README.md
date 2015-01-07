Buildpack for Gradle
====================

This is a [buildpack](https://www.cloudcontrol.com/dev-center/Platform%20Documentation#buildpacks-and-the-procfile) for
applications being built with Gradle. It supports Gradle wrappers and custom build tasks.

Usage
-----

During build process your application will be detected as a Gradle one
based on presence of `build.gradle` or `settings.gradle` file.

~~~bash
$ cctrlapp APP_NAME create java
$ cctrlapp APP_NAME/DEP_NAME push
-----> Receiving push
-----> Installing OpenJDK 1.7(openjdk7.jdk7u60-b03.tar.gz)... done
-----> Installing gradle-1.11..... done
-----> Building Gradle app...
       WARNING: The Gradle buildpack is currently in Beta.
-----> executing gradle stage
...
-----> Building image
-----> Uploading image (44.3 MB)
~~~

Gradle wrappers
---------------

In order to use custom Gradle wrapper add it to your application root directory with executable permissions.

Custom tasks
------------

By default buildpack executes `stage` gradle task. In order to use different and multiple tasks
list them in `.buildpack/tasks` file in the root directory of your application:

~~~bash
$ mkdir .buildpack
$ echo "clean build stage" > .buildpack/tasks
~~~

Add file to repository and push again:

~~~bash
$ cctrlapp APP_NAME/DEP_NAME push
-----> Receiving push
-----> Installing OpenJDK 1.7(openjdk7.jdk7u60-b03.tar.gz)... done
-----> Building Gradle app...
       WARNING: The Gradle buildpack is currently in Beta.
-----> executing gradle clean build stage
...
-----> Building image
-----> Uploading image (44.3 MB)
~~~

Hacking
-------

If any further modifications are required, fork this buildpack, apply required modifications and create your application with [`custom`](https://www.cloudcontrol.com/dev-center/Guides/Third-Party%20Buildpacks/Third-Party%20Buildpacks) type specifying your buildpack url:

~~~bash
$ $ cctrlapp APP_NAME create custom --buildpack BUILDPACK_URL
~~~
