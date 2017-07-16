※ _sass/css は、直接編集しないでいい。

### css/main.scss
カラーや大きさを変数で定義できる

### _sass/_base.scss
body, h1, h2
などの基本設定をする。main.scssで定義した変数が使える。

### _sass/_layout.scss
ヘッダー、フッターなどの設定

※sass後のビルドは不要。Jekyllが勝手にトランスパイルしてくれてる？