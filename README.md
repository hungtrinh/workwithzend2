<!-- MarkdownTOC -->

- [Install zf2 tool](#install-zf2-tool)
    - [Features](#features)
    - [Installation on ubuntu](#installation-on-ubuntu)
    - [Check version of zftool](#check-version-of-zftool)
- [Create zf2tuto project](#create-zf2tuto-project)
    - [Verify app run](#verify-app-run)
    - [Fix zftool issue when work with zf2tuto](#fix-zftool-issue-when-work-with-zf2tuto)
    - [Create module album](#create-module-album)
    - [Test driven development (TDD)](#test-driven-development-tdd)
        - [Prepaire directory structure](#prepaire-directory-structure)
        - [Install portable phpunit version (the PHAR):](#install-portable-phpunit-version-the-phar)
        - [Prepaire phpunit.xml config file](#prepaire-phpunitxml-config-file)
            - [Make phpunit.xml](#make-phpunitxml)
            - [Verify phpunit.xml content](#verify-phpunitxml-content)
        - [Prepaire Boostrap.php](#prepaire-boostrapphp)
            - [make file zf2tuto/module/Album/test/Boostrap.php](#make-file-zf2tutomodulealbumtestboostrapphp)
        - [Verify phpunit.xml and Bootstrap.php are working](#verify-phpunitxml-and-bootstrapphp-are-working)
    - [Make album list page route](#make-album-list-page-route)
        - [Make test route **/album**](#make-test-route-album)
        - [Run test to see failed status](#run-test-to-see-failed-status)
        - [Fill real code to pass test route **/album**](#fill-real-code-to-pass-test-route-album)
        - [Run test again to see test route **/album** success](#run-test-again-to-see-test-route-album-success)
    - [Create an album](#create-an-album)
        - [Make test route **/album/add**](#make-test-route-albumadd)
        - [Verify fail with test matched route **/album/add**](#verify-fail-with-test-matched-route-albumadd)
        - [Fill real code to pass test **/album/add**](#fill-real-code-to-pass-test-albumadd)
        - [Verify passed test matched route **/album/add**](#verify-passed-test-matched-route-albumadd)
    - [Edit an album route](#edit-an-album-route)
        - [Make test route  to access edit album with id 1 **/album/edit/1**](#make-test-route--to-access-edit-album-with-id-1-albumedit1)
        - [Verify fail with test matched route **/album/edit/1**](#verify-fail-with-test-matched-route-albumedit1)
        - [Fill real code to pass test **/album/edit/1**](#fill-real-code-to-pass-test-albumedit1)
        - [Verify passed test matched route **/album/edit/1**](#verify-passed-test-matched-route-albumedit1)
    - [Modeling Album](#modeling-album)
        - [Again Test First, Test Album initial state](#again-test-first-test-album-initial-state)
            - [Make test initial Album Model](#make-test-initial-album-model)
            - [Run phpunit](#run-phpunit)
            - [Fill code to pass first test](#fill-code-to-pass-first-test)
            - [Verify pass test initial album](#verify-pass-test-initial-album)
        - [Test Entity Album full fill data](#test-entity-album-full-fill-data)
            - [Again, write test exchange properties correctly](#again-write-test-exchange-properties-correctly)
            - [Again, run test to see failed status](#again-run-test-to-see-failed-status)
            - [Again, fill code to pass test](#again-fill-code-to-pass-test)
            - [Again, test passed](#again-test-passed)
    - [ Mapper entity to persistent](#-mapper-entity-to-persistent)
        - [Data mapper interface](#data-mapper-interface)
        - [Code Test first](#code-test-first)
        - [Verify failing status](#verify-failing-status)
        - [Full fill code to pass test](#full-fill-code-to-pass-test)

<!-- /MarkdownTOC -->


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

## Check version of zftool
```sh
$ zftool version
```
# Create zf2tuto project
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

## Verify app run
```sh
$ cd ~/www/zf2tuto/public
$ php -S 0:8888
```
Open web browser with url: http://localhost:8888/

## Fix zftool issue when work with zf2tuto
[Issue description  and solution here]

```sh
$ cd ~/www/zf2tuto
$ php composer.phar require zendframework/zftool:dev-master
```
## Create module album

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
or using zftool to verify
```sh
$ cd ~/www/zf2tuto && zftool modules list
Modules installed:
Application
Album
```
## Test driven development (TDD)
Apply TDD ot zf2tuto project. Please see [Unit Testing a Zend Framework 2 application]

### Prepaire directory structure

```sh
$ cd ~/www/zf2tuto
$ mkdir -p module/Album/test/AlbumTest/{Controller,Model}
```

### Install portable phpunit version (the PHAR):
Download and make phpunit runable inside zf2tutor/module/Album/test directory

```sh
$ cd ~/www/zf2tuto/module/Album/test
$ wget https://phar.phpunit.de/phpunit.phar
$ chmod +x phpunit.phar
$ php phpunit.phar --version
PHPUnit x.y.z by Sebastian Bergmann.
```

### Prepaire phpunit.xml config file

#### Make phpunit.xml
```sh
$ echo '<?xml version="1.0" encoding="UTF-8"?><phpunit bootstrap="Bootstrap.php" colors="true"><testsuites><testsuite name="zf2tuto"><directory>./AlbumTest</directory></testsuite></testsuites></phpunit>' | xmllint --format - | tee ~/www/zf2tuto/module/Album/test/phpunit.xml
```

#### Verify phpunit.xml content
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

### Prepaire Boostrap.php 
To autoload library (zend framework 2, other vendor), load current module resource
#### make file zf2tuto/module/Album/test/Boostrap.php
fill cotent below see [zend 2 unit test boostrap file](http://framework.zend.com/manual/current/en/tutorials/unittesting.html#id2)
```php
<?php

namespace AlbumTest;

use Zend\Loader\AutoloaderFactory;
use Zend\Mvc\Service\ServiceManagerConfig;
use Zend\ServiceManager\ServiceManager;
use RuntimeException;

error_reporting(E_ALL | E_STRICT);
chdir(__DIR__);

/**
 * Test bootstrap, for setting up autoloading
 */
class Bootstrap
{
    protected static $serviceManager;

    public static function init()
    {
        $zf2ModulePaths = array(dirname(dirname(__DIR__)));
        if (($path = static::findParentPath('vendor'))) {
            $zf2ModulePaths[] = $path;
        }
        if (($path = static::findParentPath('module')) !== $zf2ModulePaths[0]) {
            $zf2ModulePaths[] = $path;
        }

        static::initAutoloader();

        // use ModuleManager to load this module and it's dependencies
        $config = array(
            'module_listener_options' => array(
                'module_paths' => $zf2ModulePaths,
            ),
            'modules' => array(
                'Album'
            )
        );

        $serviceManager = new ServiceManager(new ServiceManagerConfig());
        $serviceManager->setService('ApplicationConfig', $config);
        $serviceManager->get('ModuleManager')->loadModules();
        static::$serviceManager = $serviceManager;
    }

    public static function chroot()
    {
        $rootPath = dirname(static::findParentPath('module'));
        chdir($rootPath);
    }

    public static function getServiceManager()
    {
        return static::$serviceManager;
    }

    protected static function initAutoloader()
    {
        $vendorPath = static::findParentPath('vendor');

        $zf2Path = getenv('ZF2_PATH');
        if (!$zf2Path) {
            if (defined('ZF2_PATH')) {
                $zf2Path = ZF2_PATH;
            } elseif (is_dir($vendorPath . '/ZF2/library')) {
                $zf2Path = $vendorPath . '/ZF2/library';
            } elseif (is_dir($vendorPath . '/zendframework/zendframework/library')) {
                $zf2Path = $vendorPath . '/zendframework/zendframework/library';
            }
        }

        if (!$zf2Path) {
            throw new RuntimeException(
                'Unable to load ZF2. Run `php composer.phar install` or'
                . ' define a ZF2_PATH environment variable.'
            );
        }

        if (file_exists($vendorPath . '/autoload.php')) {
            include $vendorPath . '/autoload.php';
        }

        include $zf2Path . '/Zend/Loader/AutoloaderFactory.php';
        AutoloaderFactory::factory(array(
            'Zend\Loader\StandardAutoloader' => array(
                'autoregister_zf' => true,
                'namespaces' => array(
                    __NAMESPACE__ => __DIR__ . '/' . __NAMESPACE__,
                ),
            ),
        ));
    }

    protected static function findParentPath($path)
    {
        $dir = __DIR__;
        $previousDir = '.';
        while (!is_dir($dir . '/' . $path)) {
            $dir = dirname($dir);
            if ($previousDir === $dir) {
                return false;
            }
            $previousDir = $dir;
        }
        return $dir . '/' . $path;
    }
}

Bootstrap::init();
Bootstrap::chroot();
```

### Verify phpunit.xml and Bootstrap.php are working
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar
PHPUnit 4.4.1 by Sebastian Bergmann.
Configuration read from zf2tuto/module/Album/test/phpunit.xml
Time: 755 ms, Memory: 3.75Mb

```

## Make album list page route
we access /album to retrieve list album
### Make test route **/album** 
make file zf2tuto/module/Album/test/AlbumTest/Controller/AlbumControlleTest.php with the following content

```php
<?php

namespace AlbumTest\Controller;

use Zend\Test\PHPUnit\Controller\AbstractHttpControllerTestCase;

class AlbumControllerTest extends AbstractHttpControllerTestCase
{
    public function setUp()
    {
        $this->setApplicationConfig(
            // include '/var/www/zf2tuto/config/application.config.php'
            include __DIR__ . '/../../../../../config/application.config.php'
        );
        parent::setUp();
    }

    public function testCanAccessListAlbum()
    {
        $this->dispatch('/album');

        $this->assertResponseStatusCode(200);
        $this->assertModuleName('Album');
        $this->assertControllerName('Album\Controller\Album');
        $this->assertControllerClass('AlbumController');
        $this->assertActionName('index');
        $this->assertMatchedRouteName('album');
    }
}
```

### Run test to see failed status
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar
...
Time: 2.07 seconds, Memory: 8.25Mb

There was 1 failure:

1) AlbumTest\Controller\AlbumControllerTest::testCanAccessListAlbum
Failed asserting response code "200", actual status code is "404"
...
```
### Fill real code to pass test route **/album**
make file zf2tuto/module/Album/src/Album/Controller/AlbumController.php with the following content
```php
<?php
namespace Album\Controller;
use Zend\Mvc\Controller\AbstractActionController;

class AlbumController extends AbstractActionController
{
    public function indexAction()
    {
        return false; // no viewRender
    }
}
```

Add following content to zf2tuto/modules/Album/config/module.config.php
```php
<?php
return array(
    'controllers' => array(
        'invokables' => array(
            'Album\Controller\Album' => 'Album\Controller\AlbumController'
        ),//invokables
    ),//controller

    'router' => array(
        'routes' => array(
            'album' => array(
                'type' => 'segment',
                'options' => array(
                    'route' => '/album[/][:action][/:id]',
                    'constraints' => array(
                        'action' => '[a-zA-Z][a-zA-Z0-9_-]*',
                        'id' => '[0-9]+',
                    ),//constraints 
                    'defaults' => array(
                        'controller' => 'Album\Controller\Album',
                        'action' => 'index',
                    ),//defaults
                ),//options
            ),//album
        ),//routes
    ),//router
);
```
### Run test again to see test route **/album** success
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar --testdox
...
AlbumTest\Controller\AlbumController
 [x] Can access list album
...
```

## Create an album
add to zf2tuto/module/Album/test/AlbumTest/Controller/AlbumControlleTest.php with the following content 
### Make test route **/album/add**
```php
<?php

namespace AlbumTest\Controller;

use Zend\Test\PHPUnit\Controller\AbstractHttpControllerTestCase;

class AlbumControllerTest extends AbstractHttpControllerTestCase
{
    /* setUp(), testCanAccessListAlbum() code here */
    public function testCanAccessAddAlbum()
    {
        $this->dispatch('/album/add');

        $this->assertModuleName('Album');
        $this->assertControllerName('Album\Controller\Album');
        $this->assertControllerClass('AlbumController');
        $this->assertActionName('add');
        $this->assertMatchedRouteName('album');
    }
}
```
### Verify fail with test matched route **/album/add**

```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar
...
There was 1 failure:

1) AlbumTest\Controller\AlbumControllerTest::testCanAccessAddAlbum
Failed asserting action name "add", actual action name is "not-found"
...
```
### Fill real code to pass test **/album/add**
append following content to file zf2tuto/module/Album/src/AlbumTest/Controller/AlbumControllerTest.php
```php

class AlbumControllerTest extends AbstractActionController
{
    /* old indexAction() method code HERE */
    public function addAction()
    {
        return false;
    }
}
```
### Verify passed test matched route **/album/add**
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar --testdox
...
AlbumTest\Controller\AlbumController
 [x] Can access list album
 [x] Can access add album
...
```
## Edit an album route
To edit an album : access /album/edit/:id
### Make test route  to access edit album with id 1 **/album/edit/1**
Append following content to file zf2tuto/module/Album/test/Album/Controller/AlbumControllerTest.php
```php

class AlbumControllerTest extends AbstractHttpControllerTestCase
{
    /* 
    testCanAccessListAlbum()
    testCanAccessAddAlbum() code HERE 
    */
    public function testCanAccessEditAlbum()
    {
        $this->dispatch('/album/edit/1');

        $this->assertModuleName('Album');
        $this->assertControllerName('Album\\Controller\\Album');
        $this->assertControllerClass('AlbumController');
        $this->assertActionName('edit');
        $this->assertMatchedRouteName('album');
    }
}
```
### Verify fail with test matched route **/album/edit/1**
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar
...
There was 1 failure:

1) AlbumTest\Controller\AlbumControllerTest::testCanAccessEditAlbum
Failed asserting action name "edit", actual action name is "not-found"
...
```
### Fill real code to pass test **/album/edit/1**
Append following code to zf2tuto/module/Album/src/Album/Controller/AlbumController.php
```php
...
class AlbumController extends AbstractActionController
{
    /*
    indexAction()
    addAction()
    editAction()
    code HERE
    */
    public function editAction()
    {
        return false;
    }
}
```
### Verify passed test matched route **/album/edit/1**
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar --testdox
...
AlbumTest\Controller\AlbumController
 [x] Can access list album
 [x] Can access add album
 [x] Can access edit album
...
```

## Modeling Album

* Now we make album model, using Plain older php object(POPO).
* In this example (Album look like anemic domain model).
* Alway keep in mind [You Arent Gonna Need It (YAGNI)](http://c2.com/cgi/wiki?YouArentGonnaNeedIt) - add something if you need do that

What we need? 
we need some object keep track album id, artist, album title => we have **Album entity**.
So **Album entity** look like this

![Album entity class diagram](http://yuml.me/8ebd8131 "Album class diagram")
### Again Test First, Test Album initial state
#### Make test initial Album Model
You can avoid this test case (with anemic model, trivial logic: avoid unit test to safe your time :D).
* Create folder zf2tuto/module/Album/test/AlbumTest/Entity
* Create file zf2tuto/module/Album/test/AlbumTest/Entity/AlbumTest.php
```sh
$ cd ~/www/zf2tuto
$ mkdir module/Album/test/AlbumTest/Entity
$ touch module/Album/test/AlbumTest/Entity/AlbumTest.php
```
fill following content to zf2tuto/module/Album/test/AlbumTest/Entity/AlbumTest.php
```php
<?php

namespace AlbumTest\Entity;

use Album\Entity\Album;
use PHPUnit_Framework_TestCase;

class Album extends PHPUnit_Framework_TestCase
{
    public function testInitialState()
    {
        $album = new Album();
        $this->assertNull($album->getId());
        $this->assertNull($album->getTitle());
        $this->assertNull($album->getArtist());
    }
}
```
#### Run phpunit
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar
...
PHP Fatal error:  Class 'Album\Entity\Album' not found 
...
```

#### Fill code to pass first test
* Create folder zf2tuto/module/Album/src/Album/Entity
* Create file zf2tuto/module/Album/src/Album/Entity/Album.php
```sh
$ cd ~/www/zf2tuto
$ mkdir module/Album/src/Album/Entity
$ touch module/Album/src/Album/Entity/Album.php
```
fill following content to file zf2tuto/module/Album/src/Album/Entity/Album.php
```php
<?php 
namespace Album\Entity;

class Album
{
    public function getId()
    {
        return null;
    }

    public function getTitle()
    {
        return null;
    }

    public function getArtist()
    {
        return null;
    }
}
```
#### Verify pass test initial album
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar --testdox
...
AlbumTest\Controller\AlbumController
 [x] Can access list album
 [x] Can access add album
 [x] Can access edit album
 
AlbumTest\Entity\Album
 [x] Initial state is null
...
```
### Test Entity Album full fill data
#### Again, write test exchange properties correctly
Append following content to zf2tuto/module/Album/test/AlbumTest/Entity/AlbumTest.php
```php
<?php
...
class AlbumTest extends PHPUnit_Framework_TestCase
{
    /**/
    public function testExchangeArraySetsPropertiesCorrectly()
    {
        $exchangeData = array(
            'id' => 1,
            'title' => 'first time',
            'artist' => 'you'
        );

        $album = new Album($exchangeData);
        $this->assertEquals(1,$album->getId());
        $this->assertEquals('first time', $album->getTitle());
        $this->assertEquals('you', $album->getArtist());
    }
    /**/
}
....
```
#### Again, run test to see failed status
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar 
...
There was 1 failure:

1) AlbumTest\Entity\AlbumTest::testExchangeArraySetsPropertiesCorrectly
Failed asserting that null matches expected 1.
...
```
#### Again, fill code to pass test
fill following content to zf2tuto/module/Album/src/Album/Entity/Album.php
```php
<?php 
namespace Album\Entity;

class Album
{
    /**
     * @var string
     */
    private $title;

    /**
     * @var string
     */
    private $artist;

    /**
     * @var int
     */
    private $id;

    /**
     * Make album from array
     * @param array [title,id,artist]
     */
    public function __construct($data=array()) {
        if (!$data) {
            return;
        }
        $this->exchangeArray($data);
    }

    /**
     * exchange data from array to this object
     * 
     * @param  [type] $data [description]
     * @return [type]       [description]
     */
    public function exchangeArray($data)
    {
        if (isset($data['title'])) {
            $this->setTitle($data['title']);
        }
        if (isset($data['artist'])) {
            $this->setArtist($data['artist']);
        }
        if (isset($data['id'])) {
            $this->setId ($data['id']);
        }
    }

    /**
     * Gets the value of title.
     *
     * @return string
     */
    public function getTitle()
    {
        return $this->title;
    }

    /**
     * Sets the value of title.
     *
     * @param string $title the title
     *
     * @return self
     */
    public function setTitle($title)
    {
        $this->title = $title;

        return $this;
    }


    /**
     * Gets the value of artist.
     *
     * @return string
     */
    public function getArtist()
    {
        return $this->artist;
    }

    /**
     * Sets the value of artist.
     *
     * @param string $artist the artist
     *
     * @return self
     */
    public function setArtist($artist)
    {
        $this->artist = $artist;

        return $this;
    }

    /**
     * Gets the value of id.
     *
     * @return int
     */
    public function getId()
    {
        return $this->id;
    }

    /**
     * Sets the value of id.
     *
     * @param int $id the id
     *
     * @return self
     */
    public function setId($id)
    {
        $this->id = $id;

        return $this;
    }
}
```
#### Again, test passed
```sh
$ cd ~/www/zf2tuto/module/Album/test
$ php phpunit.phar --testdox
...
AlbumTest\Controller\AlbumController
 [x] Can access list album
 [x] Can access add album
 [x] Can access edit album
 
AlbumTest\Entity\Album
 [x] Initial state is null
 [x] Exchange array sets properties correctly
...
```

##  Mapper entity to persistent 
### Data mapper interface 
![Album mapper interface class diagram](http://yuml.me/c4696820 "Album mapper interface class diagram")
### Code Test first
```php
<?php

namespace AlbumTest\Mapper;

use Album\Entity\Album;
use Album\Mapper\AlbumTable;
use Zend\Db\ResultSet\ResultSet;
use PHPUnit_Framework_TestCase;

class AlbumTableTest extends PHPUnit_Framework_TestCase
{
    public function testWhenInsertNewAlbumSuccessThenAlbumInsertedHasAnIdIsNumberic()
    {
        $mockAlbumTableGatewate = $this->getMock(
            'Zend\Db\TableGateway\TableGateway',
            $methods = array('insert'),
            $arguments = array(),
            $mockClassName = '',
            $callOriginalConstructor = FALSE,
            $callOriginalClone = TRUE,
            $callAutoload = TRUE
        );

        $albumData = array(
            'title' => 'first time',
            'artist' => 'you'
        );

        $album = new Album($albumData);
        $albumMapper = new AlbumTable($mockAlbumTableGatewate);

        $mockAlbumTableGatewate->expects($this->once())
            ->method('insert')
            ->with($albumData)
            ->will($this->returnValue(1));

        $albumMapper->insert($album);
        $this->assertEquals(1,$album->getId());
    }

    public function testWhenUpdateExistingAlbumWithAlbumAlreadyHaveAndIdThenSuccess()
    {
        $albumData = array(
            'id' => 123,
            'title' => 'first time',
            'artist' => 'you'
        );
        $album = new Album($albumData);

        $resultSet = new ResultSet();
        $resultSet->setArrayObjectPrototype(new Album);
        $resultSet->initialize(array($album));

        $mockAlbumTableGatewate = $this->getMock(
            'Zend\Db\TableGateway\TableGateway',
            $methods = array('select', 'update'),
            $arguments = array(),
            $mockClassName = '',
            $callOriginalConstructor = FALSE,
            $callOriginalClone = TRUE,
            $callAutoload = TRUE
        );

        $mockAlbumTableGatewate->expects($this->once())
            ->method('select')
            ->with(array('id'=>123))
            ->will($this->returnValue($resultSet));

        $mockAlbumTableGatewate->expects($this->once())
            ->method('update')
            ->with(array('title'=> 'first time', 'artist' => 'you'), array('id'=> 123));

        $album = new Album($albumData);
        $albumMapper = new AlbumTable($mockAlbumTableGatewate);
        $albumMapper->update($album);
    }

    /**
     * @expectedException \Exception
     * @expectedExceptionMessage Album not found
     */
    public function testWhenUpdateAnAlbumNonExistentInDbThenThrowException()
    {
        $albumData = array(
            'id' => 123,
            'title' => 'first time',
            'artist' => 'you'
        );
        $album = new Album($albumData);

        $resultSet = new ResultSet();
        $resultSet->setArrayObjectPrototype(new Album);
        $resultSet->initialize(array());

        $mockAlbumTableGatewate = $this->getMock(
            'Zend\Db\TableGateway\TableGateway',
            $methods = array('select'),
            $arguments = array(),
            $mockClassName = '',
            $callOriginalConstructor = FALSE,
            $callOriginalClone = TRUE,
            $callAutoload = TRUE
        );

        $mockAlbumTableGatewate->expects($this->once())
            ->method('select')
            ->will($this->returnValue($resultSet));

        $album = new Album($albumData);
        $albumMapper = new AlbumTable($mockAlbumTableGatewate);
        $albumMapper->update($album);
    }
}
```
### Verify failing status
### Full fill code to pass test
```php
<?php

namespace Album\Mapper;

use Zend\Db\TableGateway\TableGateway;
use Album\Entity\Album;

class AlbumTable
{
    private $albumTable;

    public function __construct(TableGateway $albumTable)
    {
        $this->albumTable = $albumTable;
    }

    public function insert(Album $album)
    {
        $id = $this->albumTable->insert(array(
            'artist' => $album->getArtist(),
            'title' => $album->getTitle()
        ));
        $album->setId($id);
    }

    public function update(Album $album)
    {
        $id = $album->getId();
        $albumRowSet = $this->albumTable->select(array('id'=>$id));

        if (0===$albumRowSet->count()) {
            throw new \Exception('Album not found');
        }

        $this->albumTable->update(
            array(
                'artist' => $album->getArtist(),
                'title' => $album->getTitle()
            ),
            array('id' => $id)
        );
    }
}
```

[zftool on github]: https://github.com/zendframework/ZFTool
[Issue description  and solution here]: https://github.com/zendframework/ZFTool/issues/51#issuecomment-25453131
[Unit Testing a Zend Framework 2 application]: http://framework.zend.com/manual/current/en/tutorials/unittesting.html#setting-up-the-tests-directory
