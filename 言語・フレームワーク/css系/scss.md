### 導入
- 導入するにはrubyが必要
- `ruby -v`で入ってるか確認
- `sudo gem install sass`でsassを導入。

### 反映
- scss/main.scssをcss/main.cssに反映させたい場合
- `sass scss/main.scss:css/main.css`
- インデントがない書き方で表示する場合、
- `sass --style expanded scss/main.scss:css/main.css`

#### 自動で反映させたい場合
- scssのファイルごとcssに自動反映するには
- `sass --style expanded --watch scss:css`


### 書き方
#### 変数
- 数値
```scss
$basicFontSize: 14px;

p {
  font-size: $baseFontSize;
  .sub {
    font-size: $baseFontSize - 2px;
  }
}
```
- 文字列
```scss
$imgDir: "../img/";

p {
  background: url($imgDir + "bg.png");
  // または
  background: url("#{$imgDir}bg.png");
}
```

- 色
  - `lighten()`や`darken()`という関数も使うことができる。
```scss
$brandColor: rgba(255,0,0,0.9);
p {
  color: lighten($brandColor, 30%);
}
```

#### 条件分岐
- `@if @else`
- `== != < > <= ?>=`
```scss
$debugMode: true;

#main {
  @if $debugMode == true {
    color: red;
  } @else {
    color: green;
  }
  p {
    @if $x > 20 { color: yellow; }
  }
}
```

### 繰り返し処理
- `@for`
```scss
@for $i from 10 through 12 {
  .fs#{$i} {font-size: #{$i}px; }
}
// .fs10 {
//   font-size: 10px;
// }

// .fs11 {
//   font-size: 11px;
// }

// .fs12 {
//   font-size: 12px;
// }
```
- while
```scss
$i: 10;
@while $i <= 12 {
  .fs#{$i} {font-size: #{$i}px; }
  $i: $i + 1;
}
// 上と同じ
```

#### リスト
- 似たようなデータをまとめて管理
```scss
$animals: cat, dog, tiger;

@each $animal in $animals {
  .#{$animal}-icon { background: url("#{$animal}.png"); }
}

// 以下も同じ
@each $animal in cat, dog, tiger {
  .#{$animal}-icon { background: url("#{$animal}.png"); }
}
```

#### 関数
```scss
$totalWidth: 940px;
$columnCount: 5;

@function getColumnWidth($width, $count) {
  // $columnWidthを計算
  $padding: 10px;
  $columnWidth: floor(($width - ($padding * ($count - 1))) / $count);
  // @debug $columnWidth;
  @return $columnWidth;
}

.grid {
  float: left;
  width: getColumnWidth($totalWidth, $columnCount);
}
```

#### ファイルを分割する
```
- main.scss
- _functions.scss
- _settings.scss
```
のようなファイル構成にして、main.scssで以下のように呼び出す
```scss
@import "settings";
@import "functions";
```

#### mixin
複数の設定をまとめて管理できる。
引数を持たせたり、初期値を与えることもできる。
```scss
@mixin round($radius:4px) {
  border-radius: $radius;
}

.label {
  font-size: 12px;
  @include round(10px);
}
```

#### extend
```scss
.msg {
  font-size: 12px;
  font-weight: bold;
  padding: 2px 4px;
  color: white;
}

.errorMsg {
  @extend .msg;
  background: red;
}

.warningMsg {
  @extend .msg;
  background: orange;
}
```
継承。mixinでも出来るが、明示的に継承を意味づける時に使うと良い。