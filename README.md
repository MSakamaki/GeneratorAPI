
# yeoman-generator ハンズオン

 + 目次
	1. generator-generator
		+ 雛形を作る
		+ yo コマンドに認識させる（パスを通す）。
	1. yo my generator
		+ ファイルのコピーをする
		+ 選択肢を作ってみる
		+ 選択肢の結果でモジュールをインストールする
			+ bower
			+ npm
		+ 設定を保存してみる
	1. yo my subgenerator 
		+ subgeneratorを作ってみる
		+ 設定を引き継いでsubgeneratorを動かしてみる。


## generator-generator

まず、node, yeoman シリーズが入っていることが前提条件です。

まず、以下のコマンドでgenerator-generatorをインストールします。

```sh
npm i -g generator-generator
```

### 雛形を作る

まずは、generatorフォルダを作ります。

```sh
mkdir generator-sample
```

``sample``の部分は好きな名前で構いません、ジェネレータの名前になります。

以下のコマンドでgeneratorの雛形が作成されます。

```sh
yo generator
```

最初に作成者名を聞かれるので適当に答えます。

2番目にジェネレータの名前を聞かれます。

デフォルトでは``generator-sample``の``sample``部分が名前になります。

すると、以下のようなフォルダが作成されます。

```sh

./generator-sample
├── README.md
├── app
│   ├── index.js
│   └── templates
│       ├── _bower.json
│       ├── _package.json
│       ├── editorconfig
│       └── jshintrc
├── node_modules
├── package.json
└── test
    ├── test-creation.js
    └── test-load.js
```

### yo コマンドに認識させる。

 yoコマンドは以下のステップでgeneratorを認識しています。

 1. パスが通っているフォルダを総なめする。
 1. ``generator-``で開始されるフォルダを探す
 1. ``generator-``フォルダ内のapp/index.jsを実行する。

そのため、パスが通っている場所に先程作成した```generator-sample```のパスを通せば認識されます。

Mac,Linuxの場合はシンボリックリンク ``ln -s [generator-sampleフォルダ絶対パス] generator-sample``でシンボリックリンクを作成します。

Windowsの場合はgenerator-sampleフォルダにパスを通すか、パスが通っているフォルダにgenerator-をコピーして下さい。

## yo my generator

### generatorの実行

では早速generatorを実行してみましょう

新たにフォルダを作成し、そのフォルダの中で以下のコマンドを実行して下さい。

```sh
yo sample
```

パスが通って入れば、問題なくジェネレータが起動します。

適当に質問に答え、実行が完了すると以下のようなフォルダで新規にプロジェクトが作成されます。

```sh
.
├── app
│   └── templates
├── bower.json
└── package.json
```

### 選択肢を作ってみる

先程ジェネレーターを作成していると、質問が来ていたと思います。

generator内の``app/index.js``の以下の部分が、その質問を作成している部分です。

```javascript

var prompts = [{
	type: 'confirm',
	name: 'someOption',
	message: 'Would you like to enable this option?',
	default: true
}];
```

ここに選択肢を追加してみましょう。

APIは[ここのサイト](https://github.com/SBoudrias/Inquirer.js#prompts-type)を参考にしてください。

次の例は以下のような質問を追加しています。

```sh

var prompts = [{
  type: 'confirm',
  name: 'coffee',
  message: 'coffee scriptは使いますか？',
  default: false
},  
{   
  type: 'input',
  name: 'yourname',
  message: 'あなたの名前は？',
  default: "someuser"
},  
{   
  type: 'checkbox',
  name: 'bower',
  message: 'JavaScriptライブラリは何を使いますか？',
  choices: [{
    value: 'bootstrap',
    name: 'twitter-bootstrap',
    checked: false
  },{ 
    value: 'angularjs',
    name: 'angular.js',
    checked: false
  }]  
 },  
 {   
  type: 'list',
  name: 'cimodule',
  message: 'CIツールは何を使いますか？',
  choices: [{
    value: 'gulp',
    name: 'gulp.js',
    checked: false
  },{
    value: 'grunt',
    name: 'Grunt',
    checked: false
  }]
}];
```

選択肢を追加したのち、generatorの変数に選択肢の結果を格納させます。

```javascript

    this.prompt(prompts, function (props) {
      var haslib = function (lib) { return props.bower.indexOf(lib) !== -1; };
      var hasci = function (lib) { return props.cimodule.indexOf(lib) !== -1; };
      this.include = this.include || {};

      this.coffee = props.coffee;
      this.yourname = props.yourname;
      this.include.angular = haslib('angularjs');
      this.include.bootstrap = haslib('bootstrap');

      this.include.gulp = hasci('gulp');
      this.include.grunt = hasci('grunt');

      this.config.set('coffeescript', this.coffee);

      done();
    }.bind(this));
```

### 選択肢の結果でもジュールをインストールする

選択肢で選んだ回答にあわせ、生成されるテンプレートを切り替えなければいけません。

bower、grunt/gulpを選択肢に合わせてインストールするように改変してみましょう。

#### bower

``app/templates/_bower.json``を開いて、以下のように編集します。

 + 編集前

```javascript
{
  "name": "package",
  "version": "0.0.0",
  "dependencies": {}
}
```

+ 編集後

```javascript
{
  "name": "package",
  "version": "0.0.0",
  "dependencies": {<% if (include.angular) { %> 
    "angular": ">=1.2.14",<% } if (include.bootstrap) {%> 
    "bootstrap": ">=3.1.1",<% } %>
    "jquery": ">=2.1.0"
  }
}
```

#### grunt/gulp

CIツールに合わせ、grunt/gulpを選択出来るようにします。

 + 編集前

```javascript
{
  "name": "package",
  "version": "0.0.0",
  "dependencies": {}
}
```

 + 編集後

```javascript
{
  "name": "package",
  "version": "0.0.0",
  "dependencies": {<% if (include.grunt) { %> 
    "grunt": ">=0.4.4",<% } if (include.gulp) {%> 
    "gulp": ">=3.5.5",<% } %>
    "jshint-stylish": ">=0.1.5"
  }
}
```

ここまで編集したら、新しいフォルダを作るか、前のテンプレートを削除するかして、もう一度ジェネレートしてみましょう。

選択肢により、bowerやgrunt/gulpがインストールされれば成功です。

## yo my gsubgenerator

### subgeneratorを作ってみる

generatorにはsubgeneratorと言う考えがあります。

代表的な例は以下です。

 + [generator-angular](https://github.com/yeoman/generator-angular)

このgeneratorは、テンプレート生成後に、同じフォルダ内で ``yo angular:route``のように実行すると、

``route``フォルダ内のindex.jsが実行されます。

``route/index.js``では内部でviewとcontrollerを生成し、それを紐付けるrouterの追加を行ってくれます。

このように、プロジェクト生成後もルールに則った規則である程度の機能追加、改変を行うようにすることができます。

作成方法は``generator-generator``を使う場合、以下のコマンドを実行します。

```sh
yo generator:subgenerator subgen
```

サブジェネレータ名（今回は仮にsubg）を決めると、以下のようなフォルダ構成になります。

```sh
.
├── README.md
├── app
│   ├── index.js
│   └── templates
│       ├── _bower.json
│       ├── _package.json
│       ├── editorconfig
│       └── jshintrc
├── node_modules
├── package.json
├── subgen
│   ├── index.js
│   └── templates
│       └── somefile.js
└── test
    ├── test-creation.js
    └── test-load.js
```

作成されたのち、もう一度``yo generator``を実行、その後``yo generator:subgen``と実行してみましょう。

フォルダに``somefile.js``がコピーされれば成功です。

### 設定を引き継いでsubgeneratorを動かしてみる

今回、最初の選択肢にcoffe scriptの選択肢を入れました。

その最初の設定に紐subgeneratorを起動させるため、generatorの設定を保持、取得する機能を導入してみましょう。

generatorの設定の保持/取得は以下の機能を使います。

 + [generatorAPI/Storage](http://yeoman.github.io/generator/Storage.html)

設定を保存する場合は``this.config.set();``を使用します。

以下のように記述することで、generator生成時に設定されたcoffee scriptのフラグが``.yo-rc``ファイルに保存されるようになります。

``javascript

this.prompt(prompts, function (props) {
  var haslib = function (lib) { return props.bower.indexOf(lib) !== -1; };
  var hasci = function (lib) { return props.cimodule.indexOf(lib) !== -1; };
  this.include = this.include || {};

  this.coffee = props.coffee;
  this.yourname = props.yourname;
  this.include.angular = haslib('angularjs');
  this.include.bootstrap = haslib('bootstrap');

  this.include.gulp = hasci('gulp');
  this.include.grunt = hasci('grunt');

  this.config.set('coffeescript', this.coffee); // <-- ここに追加！！

  done();
}.bind(this));
``

合わせて、``somefile.js``をコピーして``somefile.coffee``を作成します。

generatorテンプレート作成時に保存された``.yo-rc``の値は``this.config.get()``で取得することが出来ます。

``subgen/index.js``の内容を以下の用に編集します。

generatorテンプレート作成時に選ばれたcoffeescriptの値により、somefile.jsとsomefile.coffeeのどちらかをコピーするという処理を追加します。

```javascript

'use strict';

var util = require('util');
var yeoman = require('yeoman-generator');

var SampleGenerator = yeoman.generators.NamedBase.extend({
  init: function () {
    console.log('You called the sample subgenerator with the argument ' + this.name + '.');
    this.coffee = this.config.get('coffeescript');
    console.log('this.coffee',this.coffee);
  },

  files: function () {

  	console.log('this.name',this.name);

  	var fileext = (this.coffee?".coffee":".js");
  	var copyScript =  this.name + fileext;

	this.copy('somefile.' + fileext, copyScript);
  }
});

module.exports = SampleGenerator;
```

また最初からgeneratorを実行すると、最初に選択された設定に紐づき、ジェネレータが生成されるようになります。

以上で今回のハンズオンの内容は終了です、以下に参考ドキュメントなどをおいてますので

これから色々いじってみましょう。

## sub content

### Document

 + [GeneratorAPI](http://yeoman.github.io/generator/)
	 + [Modules](https://github.com/MSakamaki/GeneratorAPI/blob/master/Module.md)
	 + [Classes](https://github.com/MSakamaki/GeneratorAPI/blob/master/Classes.md)
	 + [Mixins](https://github.com/MSakamaki/GeneratorAPI/blob/master/Mixins.md)


### Link's


 + [Generator-generator](https://github.com/yeoman/generator-generator)

 + **必見！**[YEOMAN TEAM BLOG](http://yeoman.io/blog/)

 + [GithubSource](https://github.com/yeoman/generator)

 + [yeoman-generator](https://github.com/yeoman/yeoman/wiki/Generators#wiki-frequently-asked-questions)

 + [Testing-generators](https://github.com/yeoman/generator/wiki/Testing-generators)

 + [WRITING CUSTOM YEOMAN APP GENERATORS](http://yeoman.io/generators.html)

 + [WRITING CUSTOM YEOMAN APP GENERATORSの翻訳](http://qiita.com/sys1yagi/items/da002b32b6663faaa705)

 + [日本語訳Yeoman App Generatorsの書き方](http://qiita.com/sys1yagi/items/da002b32b6663faaa705)


