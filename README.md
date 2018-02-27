# test_webpackv4
Webpack 4.0を使ってみる

ここに書かれてある情報は(2018/02/27)現在のものとなります。

### モジュールインストール

```
npm i -D electron
npm i -D react react-dom
npm i -D babel-core babel-preset-react babel-preset-env
npm i -D webpack babel-loader
```

babel-preset-es2015からbabel-preset-envにしました。

それから、webpack4からはwebpackコマンドは別パッケージになったのでそれも入れます。

```
$ webpack
The CLI moved into a separate package: webpack-cli.
Please install 'webpack-cli' in addition to webpack itself to use the CLI.
-> When using npm: npm install webpack-cli -D
-> When using yarn: yarn add webpack-cli -D

```

翻訳:

```
CLIはwebpack-cliという別のパッケージに移動しました。
CLIを使用するにはwebpack自体に加えて 'webpack-cli'をインストールしてください。
-npmを使用する場合：npm install webpack-cli -D
-yarnを使用する場合：yarn add webpack-cli -D
```

なので入れましょう。

```
npm i -D webpack-cli
```

書き終わったあと何もせずnpm run buildしたらエラーが出ました。

```
➜  test_webpackv4 git:(master) npm run build
Hash: 51ad6ef45850cddb8c4d
Version: webpack 4.0.1
Time: 82ms
Built at: 2018-2-27 19:50:00
 1 asset
Entrypoint main = main.js
   [0] ./src/index.js 251 bytes {0} [built] [failed] [1 error]

WARNING in configuration
The 'mode' option has not been set. Set 'mode' option to 'development' or 'production' to enable defaults for this environment.

ERROR in ./src/index.js
Module parse failed: Unexpected token (6:12)
You may need an appropriate loader to handle this file type.
| export default class App extends Component {
|   render () {
|     return (<div>
|       <h1>Hello</h1>
|     </div>)
```

翻訳:

```
設定時の警告
'mode'オプションは設定されていません。 この環境のデフォルトを有効にするには、 'mode'オプションを 'development'または 'production'に設定します。

./src/index.jsのERROR
モジュールの解析に失敗しました：予期しないトークン（6:12）
このファイルタイプを処理するには、適切なローダーが必要な場合があります。
```

ここを見て実行してみます。
まずは、webpack4の目玉と言われるconfigファイルを書かない方法で行こうと思います。

https://qiita.com/shisama/items/730e7a2e6a3090a63a38


### 1. `--module-bind` オプションだけ付けて実行

```
webpack --module-bind 'js=babel-loader' --module-bind 'jsx=babel-loader'
```

結果:

```
➜  test_webpackv4 git:(master) webpack --module-bind 'js=babel-loader' --module-bind 'jsx=babel-loader'

Hash: dc950f6ced7eac1b3d69
Version: webpack 4.0.1
Time: 888ms
Built at: 2018-2-27 20:07:03
 1 asset
Entrypoint main = main.js
   [0] ./src/index.js 934 bytes {0} [built] [failed] [1 error]

WARNING in configuration
The 'mode' option has not been set. Set 'mode' option to 'development' or 'production' to enable defaults for this environment.

ERROR in ./src/index.js
Module build failed: SyntaxError: Unexpected token (6:12)

  4 | export default class App extends Component {
  5 |   render () {
> 6 |     return (<div>
    |             ^
  7 |       <h1>Hello</h1>
  8 |     </div>)
  9 |   }

➜  test_webpackv4 git:(master) ✗
```

翻訳:

```
設定時の警告
'mode'オプションは設定されていません。 この環境のデフォルトを有効にするには、 'mode'オプションを 'development'または 'production'に設定します。

./src/index.jsのERROR
モジュールビルドに失敗しました：SyntaxError：予期しないトークン（6:12）
```

Module parse failed: Unexpected token (6:12) のエラーは消えましたが、modeオプション未設定のエラーは残っています。


### 2. 1. のオプションに加え、`--mode production`オプションを付けて実行

```
webpack --module-bind 'js=babel-loader' --module-bind 'jsx=babel-loader' --mode production
```

結果:

```
➜  test_webpackv4 git:(master) ✗ webpack --module-bind 'js=babel-loader' --module-bind 'jsx=babel-loader' --mode production
Hash: 47c238ad5361544ab60b
Version: webpack 4.0.1
Time: 248ms
Built at: 2018-2-27 20:12:37
 1 asset
Entrypoint main = main.js
   [0] ./src/index.js 934 bytes {0} [built] [failed] [1 error]

ERROR in ./src/index.js
Module build failed: SyntaxError: Unexpected token (6:12)

  4 | export default class App extends Component {
  5 |   render () {
> 6 |     return (<div>
    |             ^
  7 |       <h1>Hello</h1>
  8 |     </div>)
  9 |   }

```

翻訳:

```
./src/index.jsのERROR
モジュールビルドに失敗しました：SyntaxError：予期しないトークン（6:12）
```

WARNING in configuration のエラーは消えましたが、Module build failed のエラーはまだ残っています。

ここについては調べ方が悪いのか、調べても出てきませんでした。babel-preset-envを使いたかった感じです。

ここを見て作業してみます。

https://www.valentinog.com/blog/webpack-4-tutorial/

### 1. .babelrc の作成
このような内容で作成します。

```
{
  "presets": ["env", "react"]
}
```

### 2. npm run build してみる

多分大丈夫だと思うのでビルドしてみます。

