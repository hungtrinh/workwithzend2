# Install zf2 tool

ZFTool is an utility module for maintaining modular Zend Framework 2 applications. It runs from the command line and can be installed as ZF2 module or as PHAR.
[zftool on github]


## Features

* Class-map generator
* Listing of loaded modules
* Create a new project (install the ZF2 skeleton application)
* Create a new module
* Create a new controller
* Create a new action in a controller
* Application diagnostics

## Installation on ubuntu
```sh
$ cd ~/Downloads
$ wget http://packages.zendframework.com/zftool.phar
$ chmod +x zftool.phar
$ sudo mv zftool.phar /usr/local/bin/zftool
```

## Usage
### Check version of zftool
```sh
$ zftool version
```
### Create zf2tuto project
```sh
$ mkdir ~/www
$ cd ~/www
$ zftool create project zf2tuto
$ cd zf2tuto
$ php composer.phar install
```

### Verify app run
```sh
$ cd ~/www/zf2tuto/public
$ php -S 0:8888
```
Open web browser with url: http://localhost:8888/

### Fix zftool issue when work with zf2tuto
[Issue description  and solution here]

```sh
$ cd ~/www/zf2tuto
$ php composer.phar require zendframework/zftool:dev-master
```
### Create module album

```sh
$ cd ~/www/zf2tuto
$ zftool create module album
```
Check module Album added to project
```sh
$ ls ~/www/zf2tuto/modules/
Album Application
$ cat config/application.config.php | grep Album
    'Album'
```
### Test Driven Development 

Please see [Unit Testing a Zend Framework 2 application]
```sh
$ mkdir -p ~/www/zf2tuto/module/Album/test/AlbumTest/Controller
$ mkdir -p ~/www/zf2tuto/module/Album/test/AlbumTest/Model
```

Make phpunit.xml
```sh
$ echo '<?xml version="1.0" encoding="UTF-8"?><phpunit bootstrap="Bootstrap.php" colors="true"><testsuites><testsuite name="zf2tuto"><directory>./AlbumTest</directory></testsuite></testsuites></phpunit>' | xmllint --format - | tee ~/www/zf2tuto/module/Album/test/phpunit.xml
```

Verify phpunit.xml content
```sh
$ cat ~/www/zf2tuto/module/Album/test/phpunit.xml
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit bootstrap="Bootstrap.php" colors="true">
  <testsuites>
    <testsuite name="zf2tuto">
      <directory>./AlbumTest</directory>
    </testsuite>
  </testsuites>
</phpunit>
```

Install portable phpunit version (the PHAR):
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ wget https://phar.phpunit.de/phpunit.phar
$ chmod +x phpunit.phar
$ mv phpunit.phar phpunit
$ phpunit --version
PHPUnit x.y.z by Sebastian Bergmann.
```

[zftool on github]: https://github.com/zendframework/ZFTool
[Issue description  and solution here]: https://github.com/zendframework/ZFTool/issues/51#issuecomment-25453131
[Unit Testing a Zend Framework 2 application]: http://framework.zend.com/manual/current/en/tutorials/unittesting.html#setting-up-the-tests-directory
