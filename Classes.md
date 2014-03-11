# Classes

### Classes: [Base](http://yeoman.github.io/generator/Base.html)

#### new Base(args, options)

base クラスはすべてのgeneratorへの共通APIを提供します。
オプションとしてarguments, hooks, file, prompt, log, API, などが定義されています。
actions/pixinsのprototype中に見ることができます。

すべてのgeneratorはこのクラスを拡張する必要があります。

| Method | argment | infomation |
|:--|:--|:--|


##### Parameters:

| Name | Type | Description |
|:--|:--|:--|
| args | String or Array	 |  |
| options | Object	 |  |

##### Properties:

| Name | Type | Description |
|:--|:--|:--|
| env | Object | the current Environment being run |
| args | Object | Provide arguments at initialization |
| resolved | String | the path to the current generator |
| generatorName | String	 |
| description | String | Used in --help output |
| appname | String | The application name |
| config | Storage	| .yo-rc config file manager |
| src | Object | File util instance scoped to sourceRoot |
| dest | Object | File util instance scoped to destinationRoot |
| log | function | Output content through Interface Adapter |



### Classes: [Environment](http://yeoman.github.io/generator/Environment.html)
### Classes: [NamedBase](http://yeoman.github.io/generator/NamedBase.html)
### Classes: [RunContext](http://yeoman.github.io/generator/RunContext.html)
### Classes: [Storage](http://yeoman.github.io/generator/Storage.html)
### Classes: [TerminalAdapter](http://yeoman.github.io/generator/TerminalAdapter.html)
