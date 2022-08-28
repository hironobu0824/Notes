[公式ドキュメント](https://readouble.com/laravel/8.x/ja/sail.html)

### 既存アプリへのSailインストール
- sailをインストール
```
composer require laravel/sail --dev
```
- Sailのdocker-compose.ymlファイルをアプリケーションのルートへリソース公開
```
php artisan sail:install
```
- 立ち上げる
```
./vendor/bin/sail up
```
***
```
alias sail="./vendor/bin/sail"
```
を設定すれば
```
sail up
```
で起動できる
```
sail up -d
```
でバックグラウンドで起動
```
sail down
```
で終了