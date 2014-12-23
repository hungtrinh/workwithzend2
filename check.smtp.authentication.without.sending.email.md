# How to check SMTP authentication without sending email?

Depend:
* php 5.2+
* Zend Framework 1

```PHP
set_include_path(implode(PATH_SEPARATOR, array(
    '/Users/apple/www/zend_compact/library', //point to Zend lib directory
    get_include_path()
)));

ini_set('display_errors',1);
ini_set('display_startup_errors',1);
error_reporting(-1);

require_once 'Zend/Loader/Autoloader.php';
$loader = Zend_Loader_Autoloader::getInstance();

$host = 'smtp.gmail.com';
$port = 465;
$config = array(
    'auth' => 'login',
    'ssl' => 'ssl',
        'username' => 'yourgmail.com',
        'password' => 'testmail'
);

class SmtpAuthentication extends Zend_Mail_Protocol_Smtp_Auth_Login {
    protected $_authMessage = null;

    public function getAuthenMessage() {
        return $this->_authMessage;
    }

    public function isAuthenSuccess() {
        try {
            $this->connect();
            $this->helo();
            return $this->_auth;
        }
        catch(Zend_Mail_Protocol_Exception $e) {
            $this->_authMessage = $e->getMessage();
        }
        return false;
    }
};

$smtp = new SmtpAuthentication($host, $port, $config);

var_dump($smtp->isAuthenSuccess()); // succes or failed
var_dump($smtp->getAuthenMessage()); // cause
```
