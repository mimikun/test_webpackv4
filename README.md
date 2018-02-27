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

書き終わったあと何もせずnpm run buildしたらこんなものが出た。

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

ドキュメント探したらまだないらしい？ので適当に実行してみます。
