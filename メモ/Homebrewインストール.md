https://chigusa-web.com/blog/homebrew/

[公式サイト](https://brew.sh/index_ja)にアクセス

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

を実行

```
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/xxx/.zprofile
```
（xxxはユーザー名）
と
```
eval "$(/opt/homebrew/bin/brew shellenv)"
```
を実行してパスを通す

```
brew --version
```
で確認