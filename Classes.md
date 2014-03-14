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


#### Members

 + **extend**
	+ [class-extend](https://github.com/SBoudrias/class-extend) の機能を使用している。
	+ 新しいgenaratorを作る場合この機能で拡張します。
	+ また、親のprototypeメソッドにスーパーオブジェクトを追加します。

 + prompt
 	+ [adapter](https://github.com/MSakamaki/generator/blob/master/lib/env/adapter.js)重要
 	+ [Inquirer](https://github.com/SBoudrias/Inquirer.js)でコンソールを管理してたりする。
	+ 何が使えるかは[ドキュメント](https://github.com/SBoudrias/Inquirer.js#prompts-type)参照

#### Methods

##### argument(name, config)

クラスに引数を追加できるようにする。

    Adds an argument to the class and creates an attribute getter for it.

    Arguments are different from options in several aspects. The first one is how they are parsed from the command line, arguments are retrieved from position.

    Besides, arguments are used inside your code as a property (this.argument), while options are all kept in a hash (this.options).
    Options:

        desc Description for the argument
        required Boolean whether it is required
        optional Boolean whether it is optional
        type String, Number, Array, or Object
        defaults Default value for this argument
        banner String to show on usage notes

    Parameters:
    Name 	Type 	Description
    name 	String 	
    config 	Object 	

##### composeWith(namespace, options, settings) → {this}

    Compose this generator with another one.
    Parameters:
    Name 	Type 	Argument 	Description
    namespace 	String 		

    The generator namespace to compose with
    options 	Object 		

    The options passed to the Generator
    settings 	Object 	<optional>
    	

    Settings hash on the composition relation
    Properties
    Name 	Type 	Argument 	Default 	Description
    local 	string 	<optional>
    		

    Path to a locally stored generator
    link 	String 	<optional>
    	"weak" 	

    If "strong", the composition will occured even when the composition is initialized by the end user


##### defaultFor(name)

    Return the default value for the option name.

    Also performs a lookup in CLI options and the this.fallbacks property.
    Parameters:
    Name 	Type 	Description
    name 	String 	

##### destinationRoot(rootPath) → {String}

    Change the generator destination root directory. This path is used to find storage, when using this.dest and this.src and for multiple file actions (like this.write and this.copy)

    Parameters:
    Name 	Type 	Description
    rootPath 	String 	

    new destination root path


##### determineAppname()

    Determines the name of the application.

    First checks for name in bower.json. Then checks for name in package.json. Finally defaults to the name of the current directory.


##### getCollisionFilter()

    Return a file Env validation filter checking for collision


##### hookFor(name, config)

    Registers a hook to invoke when this generator runs.

    A generator with a namespace based on the value supplied by the user to the given option named name. An option is created when this method is invoked and you can set a hash to customize it.

    Must be called prior to the generator run (shouldn't be called within a generator "step" - top-level methods).
    Options:

        as The context value to use when runing the hooked generator
        args The array of positional arguments to init and run the generator with
        options An object containing a nested options property with the hash of options

              to use to init and run the generator with


##### option(name, config)

    Adds an option to the set of generator expected options, only used to generate generator usage. By default, generators get all the cli option parsed by nopt as a this.options Hash object.
    Options:

        desc Description for the option
        type Either Boolean, String or Number
        default Default value
        banner String to show on usage notes
        hide Boolean whether to hide from help

    Parameters:
    Name 	Type 	Description
    name 	String 	
    config 	Object 	

##### rootGeneratorName()

    Determine the root generator name (the one who's extending Base).


##### run(args, cb)

    Runs the generator, executing top-level methods in the order they were defined.

    Special named method like constructor and initialize are skipped (CoffeeScript and Backbone like inheritence), or any method prefixed by a _.

    You can also supply the arguments for the method to be invoked, if none is given, the same values used to initialize the invoker are used to initialize the invoked.
    Parameters:
    Name 	Type 	Argument 	Description
    args 	String | Array 	<optional>
    	    cb 	function 	<optional>
    	


##### runHooks(cb)

    Goes through all registered hooks, invoking them in series.
    Parameters:
    Name 	Type 	Description    cb 	function 	


##### sourceRoot(rootPath) → {String}

    Change the generator source root directory. This path is used by this.dest and this.src and multiples file actions like (this.read and this.copy)
    Parameters:
    Name 	Type 	Description
    rootPath 	String 	    new source root path
 

### Classes: [Environment](http://yeoman.github.io/generator/Environment.html)
### Classes: [NamedBase](http://yeoman.github.io/generator/NamedBase.html)
### Classes: [RunContext](http://yeoman.github.io/generator/RunContext.html)
### Classes: [Storage](http://yeoman.github.io/generator/Storage.html)
### Classes: [TerminalAdapter](http://yeoman.github.io/generator/TerminalAdapter.html)
