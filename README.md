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
    unset($arr_query);
    $arr_query = array(
        "bt_type" => $_POST['bt_type'],
        "bt_title" => $_POST['bt_title'],
        "bt_link1" => $_POST['bt_link1'],
        "bt_link2" => $_POST['bt_link2'],
        "bt_target1" => $_POST['bt_target1'],
        "bt_target2" => $_POST['bt_target2'],
        "bt_rank" => $_POST['bt_rank'],
        "bt_show" => $_POST['bt_show'],
        "bt_wdate" => $DB->now(),
    );

    $DB->insert_query('banner_t', $arr_query);
    $_last_idx = $DB->insert_id();
```

입력시 날짜 기입방식이 변경되었습니다. now() > $db->now()

### Update Query

```php
    unset($arr_query);
    $arr_query = array(
        "bt_type" => $_POST['bt_type'],
        "bt_title" => $_POST['bt_title'],
        "bt_link1" => $_POST['bt_link1'],
        "bt_link2" => $_POST['bt_link2'],
        "bt_target1" => $_POST['bt_target1'],
        "bt_target2" => $_POST['bt_target2'],
        "bt_rank" => $_POST['bt_rank'],
        "bt_show" => $_POST['bt_show'],
        "bt_wdate" => $DB->now(),
    );

    $DB->where('idx', $_POST['bt_idx']);

    $DB->update_query('banner_t', $arr_query);
```

```php
$query = "
    select *, a1.idx as bt_idx from banner_t a1
    where a1.idx = '".$_GET['bt_idx']."'
";
$row = $DB->fetch_query($query);
```

한개만

```php
unset($list);
$sql_query = $query.$where_query." order by a1.idx desc limit ".$n_from.", ".$n_limit;
$list = $DB->select_query($sql_query);

if ($list) {
    foreach ($list as $row) {
```

여러개 가져오기

$DB->close() 가 없습니다.
