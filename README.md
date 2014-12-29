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
Or shortcut
```sh
$ cd ~/Downloads \
&& wget http://packages.zendframework.com/zftool.phar \
&& chmod +x zftool.phar \
&& sudo mv zftool.phar /usr/local/bin/zftool
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
Or shortcut
```sh
$ mkdir ~/www /
&& cd ~/www /
&& zftool create project zf2tuto /
&& cd zf2tuto /
&& php composer.phar install
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
### create module album

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
[zftool on github]: https://github.com/zendframework/ZFTool
[Issue description  and solution here]: https://github.com/zendframework/ZFTool/issues/51#issuecomment-25453131
