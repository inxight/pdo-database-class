# PDO-database-class

PHP PDO Wrapper which utilizes PDO and prepared statements

<hr>
### Installation

To utilize this class, first import PDODb.php into your project, and require it.
PDODb requires PHP 5.5+ to work.

```php
require_once ('PDODb.php');
```

### Installation with composer

It is also possible to install library via composer

```
composer require tommyknocker/pdo-database-class
```

### Initialization

initialization:

```php
$db = new PDODb(['type' => 'mysql',
                 'host' => 'host',
                 'username' => 'username',
                 'password' => 'password',
                 'dbname'=> 'databaseName',
                 'port' => 3306,
                 'prefix' => 'my_',
                 'charset' => 'utf8']);
```

클래스 파일 하단에 적용합니다.

### Insert Query

Simple example

```php
$data = ["login" => "admin",
         "firstName" => "John",
         "lastName" => 'Doe',
         'createdAt' => $db->now(),
];
$id = $db->insert_query('users', $data);
if($id)
    echo 'user was created. Id=' . $id;
```

입력시 날짜 기입방식이 변경되었습니다. now() > $db->now()

### Update Query

```php
$data = ['firstName' => 'Bobby',
	    'lastName' => 'Tables',
	    'editCount' => $db->inc(2),
	    // editCount = editCount + 2;
	    'active' => $db->not()
	    // active = !active;
];
$db->where('id', 1);
if ($db->update('users', $data)) {
    echo $db->getRowCount() . ' records were updated';
} else {
    echo 'update failed: ' . $db->getLastError();
}
```

```php
$users = $db->fetch_query('SELECT * FROM users WHERE id = admin');
한개만


$users = $db->select_query('SELECT * FROM users WHERE show = Y');
foreach ($users as $user) {
    print_r($user);
}
```

여러개 가져오기

$DB->close() 가 없습니다.
