# test_webpackv4
Webpack 4.0を使ってみる

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

