# env-openjdk-gradle
Using as investigation for a Java development environment

## Why
Looking at how Docker could simplify Java development, build and deployment.

This Docker file creates image giving you a development environment based on [Ubuntu 14.04 (trusty)][ubuntu] to build [OpenJDK 8][openjdk] projects using [Gradle 2.8][gradle]

## Usage
I'm assuming you know how to use Docker, Java and Gradle... and have Docker installed!

(If you're new to docker the site is very helpful [Docker user guide][docker-user-guide])

Using my [simple-spark-api][simple-spark-api] as an example...

First get the base image...
```
docker pull channie/env-openjdk-gradle
```

Adding a `Dockerfile` containing the following to the Java project root next to the `src` folder and `gradle.build` file

```
# The image source
FROM channie/env-openjdk-gradle
# Tell everyone who is maintaining this file
MAINTAINER Your Name <yourname@someemail.com>
WORKDIR /code
ADD build.gradle /code/build.gradle
ADD src /code/src
RUN ["gradle","build"]
EXPOSE 4567
CMD ["gradle", "runJar"]
```
From the `Dockerfile` location, run

```
docker build -t yourname/yourprojectname:version .
```
You've just built an image containing the project!
Now run it in a container...
```
docker run -dp 10023:4567 yourname/yourprojectname:version
```
Open a browser of your choice and navigate to

http://your-docker-machine-ip:10023/hello

If alls good you should see a hello message :)

## Coming soon
• Different java example

• Smaller image size

## Tag History


#### [trusty-openjdk8-gradle2.8][trusty-openjdk8-gradle2.8]
  * Built on [Ubuntu 14.04 Trusty Docker official image][docker-ubuntu]
  * Contains OpenJDK 8 (1.8.0_45-internal)
  * Contains Gradle 2.8



[docker-user-guide]: https://docs.docker.com/userguide/
[ubuntu]: http://releases.ubuntu.com/
[openjdk]: http://openjdk.java.net/install/
[gradle]: http://gradle.org/gradle-download/
[simple-spark-api]: https://github.com/lendmeapound/simple-spark-api
[trusty-openjdk8-gradle2.8]:https://github.com/lendmeapound/docker-files/tree/trusty-openjdk8-gradle2.8
[docker-ubuntu]:https://hub.docker.com/_/ubuntu/
