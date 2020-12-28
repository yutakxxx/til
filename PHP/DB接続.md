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