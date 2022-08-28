https://labo.kon-ruri.co.jp/composer-macos-install/
***
[Homebrewインストール](/メモ/Homebrewインストール.md)をしておく

```
brew install composer
```

`composer install`や`composer update`をしても、PHPのバージョンと合わないと言われる。

[composer.lockとcomposer.jsonの違い](/メモ/composer.lockとcomposer.json.md)


エラー文↓
```
Root composer.json requires php ^7.1.3 but your php version (8.1.9) does not satisfy that requirement.
```

適当にcomposer.jsonを書き換えたがうまくいかない。

```
curl -s "https://laravel.build/sample" | bash
```
で Laravelプロジェクトを仮で作って、そのcomposer,jsonをコピペしたら、`composer update`通った。


