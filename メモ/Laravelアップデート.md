### [Laravel 8.x アップグレードガイド](https://readouble.com/laravel/8.x/ja/upgrade.html)


https://yoo-s.com/topic/detail/869


- composer.jsonの編集
⇨ composer update

- シーダーファイルに
```
namespace Database\Seeders;
```
を追加
database/seedsディレクトリの名前をdatabase/seedersに変更

- `composer require laravel/legacy-factories`の実行
  - Laravelのモデルファクトリ機能は、クラスをサポートするよう完全に書き直されており、Laravel7.xスタイルのファクトリとは互換性がありません。ただし、アップグレードプロセスを簡単にするため、新しいlaravel/legacy-factoriesパッケージが作成され、Laravel 8.xで既存のファクトリを続けて使用できます。このパッケージはComposerでインストールできます。

- ルーティングを
```php
Route::get('/users', [UserController::class, 'index']);
```
の形に

```
php artisan -V
Laravel Framework 9.26.1
```

完了

### [Laravel 9.x アップグレードガイド](https://readouble.com/laravel/9.x/ja/upgrade.html)
```
Class "Fideloper\Proxy\TrustProxies" not found
```
というエラー画面

Laravel8プロジェクトをLaravel9にアップグレードする際、既存のアプリケーションコードを全く新しいLaravel9アプリケーションスケルトンへインポートする場合、アプリケーションの「信用できるプロキシ」ミドルウェアを更新する必要がある場合があります。

`app/Http/Middleware/TrustProxies.php`ファイル中の、`use Fideloper\Proxy\TrustProxies as Middleware`を`use Illuminate\Http\Middleware\TrustProxies as Middleware`へ変更してください。

次に、`app/Http/Middleware/TrustProxies.php`中の$headersプロパティ定義を更新します。

```
// 変更前
protected $headers = Request::HEADER_X_FORWARDED_ALL;

// 変更後
protected $headers =
    Request::HEADER_X_FORWARDED_FOR |
    Request::HEADER_X_FORWARDED_HOST |
    Request::HEADER_X_FORWARDED_PORT |
    Request::HEADER_X_FORWARDED_PROTO |
    Request::HEADER_X_FORWARDED_AWS_ELB;
```
最後に、アプリケーションからfideloper/proxyComposerの依存パッケージを削除します。

```
composer remove fideloper/proxy
```