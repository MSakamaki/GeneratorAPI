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

##### Properties:

| Name | Type | Description |
|:--|:--|:--|
| env | Object | 実行時の環境変数 |
| args | Object | 初期化時の引数 |
| resolved | String | generatorのパス |
| generatorName | String	 |  |
| description | String | ``-help``オプションで使用する。 |
| appname | String | アプリケーション名 |
| config | Storage	| ``.yo-rc``設定 ファイルマネージャ |
| src | Object | file utilインスタンスのスコープをsourceRoot(ソースコード)に設定 |
| dest | Object | file utilインスタンスのスコープをdestinationRoot(リリース先)に設定 |
| log | function | Output content through Interface Adapter |



### Classes: [Environment](http://yeoman.github.io/generator/Environment.html)
### Classes: [NamedBase](http://yeoman.github.io/generator/NamedBase.html)
### Classes: [RunContext](http://yeoman.github.io/generator/RunContext.html)
### Classes: [Storage](http://yeoman.github.io/generator/Storage.html)
### Classes: [TerminalAdapter](http://yeoman.github.io/generator/TerminalAdapter.html)
