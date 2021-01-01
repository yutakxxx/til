# コントローラ規約
* 「fuel/app/classes/controller」以下に配置する
* ファイル名はコントローラ名とし、全て小文字で記載する
* クラス名には「Controller_」という接頭辞をつける
* クラス名の単語の最初は大文字でその他は小文字とする
* クラス名の中の「_」はフォルダ区切りになる
* Controllerクラスを継承する
fuel/app/classes/controller/test.php
```php
<?php
class Controller_Test extends Controller
{
  ...
}
```
<br>

「fuel/app/classes/controller」以下でフォルダ別にさらに分けて表示する場合、クラス名の区切りは以下のようになる  
fuel/app/classes/controller/example/test
```php
class Controller_Example_Test extends Controller
{
  ...
}
```
<br>
<br>

# FuelPHPのURL構造
```
http://example.jp/コントローラ/メソッド[/パラメータ1[/パラメータ2[/...]]]
```
<br>
<br>

# メソッド
ブラウザから実行されるメソッドは接頭辞に`action`をつける必要がある  


