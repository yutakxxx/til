HTMLフォームの作成はformタグの中に記述する  
index.php
```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <title>フォーム学習</title>
</head>
<body>
  <main>
    <h2>Practice</h2>
      <form action="submit.php" method="get">
        <label for="my_name">お名前：</label>
        <input type="text" id="my_name" name="my_name" maxlength="255" value="">
        <input type="submit" value="送信する">
      </form>
  </main>
</body>
</html>
```
作成したフォームで送信ボタンを押すと、formタグのaction属性に指定されているsubmit.phpにデータ送信される  
submit.php
```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <title>フォーム学習</title>
</head>
<body>
  <main>
    <h2>Practice</h2>
    お名前：<?php echo htmlspecialchars($_REQEST['my_name'], ENT_QUOTES); ?>
  </main>
</body>
</html>
```

* `$_REQEST['my_name']`はフォームの値を受け取るためのグローバル変数と呼ばれるもの  
連想配列の形になっており、index.phpのinputタグで記述したname属性を指定して取り出すことができる

* `htmlspecialchars()`はHTMLタグなどがそのまま出力されないようにするために必要となる  
二つ目のパラメータには基本的に`ENT_QUOTES`を指定する  