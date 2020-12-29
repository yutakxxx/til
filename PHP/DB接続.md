# PDO
PHPからDBを操作するにはPDO（PHP Data Objects）を使用する  
```php
try {
  $db = new PDO('mysql:dbname=mydb;host=127.0.0.1;charset=utf8','root','root');
} catch (PDOException $e) {
  echo 'DB接続エラー： ' . $e->getMessage();
}
```
<br>

execメソッドはDBのクエリをそのまま入力できる  
返り値は挿入した件数なので、最後に挿入した件数を挿入してみる
```php
$count = $db->exec('INSERT INTO my_items SET maker_id=1, item_name="もも", price=210, keyword="缶詰,甘い,ピンク"');
echo $count . '件のデータを挿入しました';
```
<br>

SELECT構文はexecメソッドでは受け取ることができないのでqueryメソッドを使用する
```php
$records = $db->query('SELECT * FROM my_items');
while ($record = $records->fetch()) {
  echo $record['item_name'] . "\n";
}
```
$recordsはレコードセットというオブジェクトのインスタンスとなる  
そのインスタンスに用意されているfetchというメソッドを使いデータを一行ずつ取り出す
fetchはデータを行ずつ取り出し、取り出す行がなくなるとfalseを返すため while構文の中に入れて判定を行っている
<br>
<br>

# DBに値を保存
DBに値を保存する際に、以下のように入力された値をそのままDBに保存してしまうと、悪意のあるSQLを埋め込まれる危険性がる
```php
try {
  $db = new PDO('mysql:dbname=mydb;host=127.0.0.1;chartset=utf8', 'root', 'root');

  // この書き方はセキュリティ上よろしくない
  $db->exec('INSERT INTO memos SET memo="' . $_POST['memo'] . '", created_at=NOW()');
} catch (PDOException $e) {
  echo 'DB接続エラー：' . $e->getMessage();
}
```
そのため、フォームなどから渡された値を安全にSQLに格納するには`prepare()`を使用する
```php
try {
  $db = new PDO('mysql:dbname=mydb;host=127.0.0.1;chartset=utf8', 'root', 'root');

  // SQLを事前に準備
  $statement = $db->prepare('INSERT INTO memos SET memo=?, created_at=NOW()');
  // executメソッドに入る値を配列で渡す
  $statement->execute(array($_POST['memo']));
} catch (PDOException $e) {
  echo 'DB接続エラー：' . $e->getMessage();
}
```
`execute()`に渡した値の型は自動で判別される  
また、`prepare()`を使った書き方には下記のような方法もある
```php
try {
  $db = new PDO('mysql:dbname=mydb;host=127.0.0.1;chartset=utf8', 'root', 'root');

  // SQLを事前に準備
  $statement = $db->prepare('INSERT INTO memos SET memo=?, created_at=NOW()');
  // 第一引数に何番目の？に入るか指定し、第二引数に値を格納する
  $statement->bindParam(1, $_POST['memo']);
  // executeで保存処理を実行
  $statement->execute();
} catch (PDOException $e) {
  echo 'DB接続エラー：' . $e->getMessage();
}
```