<!-- MarkdownTOC -->

- [Environment](#environment)
- [Install jenkins](#install-jenkins)
    - [Manual install](#manual-install)
    - [Install plugins](#install-plugins)
    - [Shortcut install](#shortcut-install)
- [Install ant](#install-ant)
    - [Manual install](#manual-install-1)
    - [Verify install success](#verify-install-success)
    - [Install all plugins needed](#install-all-plugins-needed)
- [References cited](#references-cited)

<!-- /MarkdownTOC -->
# Environment
* Ubuntu 12.04+ 64bit
* Openjdk 6
# Install jenkins
## Manual install
```sh
$ sudo -s
$ wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
$ echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list
$ apt-get update
$ apt-get install jenkins
```
## Install plugins
```sh
$ cd
$ wget http://localhost:8080/jnlpJars/jenkins-cli.jar
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin checkstyle
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin clover
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin dry
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin htmlpublisher
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin jdepend
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin plot
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin pmd
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin violations
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin xunit
$ java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin build-pipeline-plugin
$ java -jar jenkins-cli.jar -s http://localhost:8080 safe-restart
```
## Shortcut install
```sh
$ cd && wget http://localhost:8080/jnlpJars/jenkins-cli.jar && java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin checkstyle clover dry htmlpublisher jdepend plot pmd violations xunit build-pipeline-plugin && java -jar jenkins-cli.jar -s http://localhost:8080 safe-restart
```
# Install ant
## Manual install
```sh
$ sudo apt-get install -y openjdk-6-jdk
$ mkdir ~/Downloads && cd ~/Downloads
$ wget http://mirrors.viethosting.vn/apache//ant/binaries/apache-ant-1.9.4-bin.tar.gz
$ tar -xzf apache-ant-1.9.4-bin.tar.gz
$ sudo mv apache-ant-1.9.4 /usr/local

```
## Verify install success
```sh
$ /usr/local/apache-ant-1.9.4/bin/ant -version
Apache Ant(TM) version 1.9.4 compiled on April 29 2014
```
## Install all plugins needed
FTP, SSH, ...
```sh
$ cd /usr/local/apache-ant-1.9.4
$ bin/ant -f fetch.xml -Ddest=system
Buildfile: /usr/local/apache-ant-1.9.4/fetch.xml

pick-dest:
     [echo] Downloading to /usr/local/apache-ant-1.9.4/lib
...
```
# References cited
* http://jenkins-php.org/
* http://pwong-tipsandtricks.blogspot.com/2014/12/install-jenkins-and-pluginstools-for.html


