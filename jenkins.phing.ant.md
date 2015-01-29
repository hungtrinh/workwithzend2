<!-- MarkdownTOC -->

- [Install jenkins](#install-jenkins)
- [Install plugins](#install-plugins)
- [References cited](#references-cited)

<!-- /MarkdownTOC -->

# Install jenkins
```sh
sudo -s
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list
apt-get update
apt-get install jenkins
```
# Install plugins
```sh
cd
wget http://localhost:8080/jnlpJars/jenkins-cli.jar
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin checkstyle
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin clover
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin dry
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin htmlpublisher
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin jdepend
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin plot
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin pmd
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin violations
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin xunit
java -jar jenkins-cli.jar -s http://localhost:8080 install-plugin build-pipeline-plugin
java -jar jenkins-cli.jar -s http://localhost:8080 safe-restart
```

# References cited
http://jenkins-php.org/
http://pwong-tipsandtricks.blogspot.com/2014/12/install-jenkins-and-pluginstools-for.html