# Classes

### Classes: [Base](http://yeoman.github.io/generator/Base.html)

#### new Base(args, options)

base クラスはすべてのgeneratorへの共通APIを提供します。

オプションとしてarguments, hooks, file, prompt, log, API, などが定義されています。

actions/pixinsのprototype中に見ることができます。

すべてのgeneratorはこのクラスを拡張する必要があります。


##### Parameters:

| Name | Type | Description |
|:--|:--|:--|
| args | String or Array	 |  |
| options | Object	 |  |

##### Properties

| Name | Type | Description |
|:--|:--|:--|
| env | Object | 実行時の環境変数 |
| args | Object | 初期化時の引数 |
| resolved | String | generatorのパス |
| generatorName | String	 |  |
| description | String | ``-help``オプションで使用する。 |
| appname | String | アプリケーション名 |
| config | Storage	| [.yo-rc.json](http://yeoman.github.io/generator/Storage.html)ファイルマネージャ |
| src | Object | file utilインスタンスのスコープをsourceRoot(ソースコード)に設定 |
| dest | Object | file utilインスタンスのスコープをdestinationRoot(リリース先)に設定 |
| log | function | [adapter](https://github.com/yeoman/generator/blob/master/lib/env/adapter.js)を経由し、ログの内容を標準出力する。 |


##### Members

 + **extend**
	+ [class-extend](https://github.com/SBoudrias/class-extend) の機能を使用している。
	+ 新しいgenaratorを作る場合この機能で拡張します。
	+ また、親のprototypeメソッドにスーパーオブジェクトを追加します。

 + prompt
 	+ [adapter](https://github.com/MSakamaki/generator/blob/master/lib/env/adapter.js)重要
 	+ [Inquirer](https://github.com/SBoudrias/Inquirer.js)でコンソールを管理してたりする。
	+ 何が使えるかは[ドキュメント](https://github.com/SBoudrias/Inquirer.js#prompts-type)参照


### Classes: [Environment](http://yeoman.github.io/generator/Environment.html)
### Classes: [NamedBase](http://yeoman.github.io/generator/NamedBase.html)
### Classes: [RunContext](http://yeoman.github.io/generator/RunContext.html)
### Classes: [Storage](http://yeoman.github.io/generator/Storage.html)
### Classes: [TerminalAdapter](http://yeoman.github.io/generator/TerminalAdapter.html)
