
# yeoman-generator ハンズオン

 + 目次
	1. generatorの基本
		+ generatorの仕組み
		+ generatorのできること
			+ テンプレートの作成 
			+ テンプレートに沿う機能の追加とか
			+ ジェネレータの品質保持
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


## generatorの基本

### generatorの仕組み

### generatorのできること

#### テンプレート作成

#### テンプレートに沿う機能の追加とか

#### ジェネレータの品質保持

## generator-generator

まず、node, yeoman シリーズが入っていることが前提条件です。

まず、以下のコマンドでgenerator-generatorをインストールします。

```sh

npm i -g generator-generator

```

### 雛形を作る

まずは、generatorフォルダを作ります。

```sh

mkdir generator-XXXX

```

``XXXX``の部分は好きな名前で構いません、そこがジェネレータの名前になります。

以下のコマンドでgeneratorの雛形が作成されます。

```sh

yo generator

```

最初に作成者名を聞かれるので適当に答えます。

2番目にジェネレータの名前を聞かれます。

デフォルトでは``generator-XXXX``の``XXXX``部分が名前になります。

すると、以下のようなフォルダが作成されます。

```sh

./generator-XXXX
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

そのため、パスが通っている場所に先程作成した```generator-XXXX```のパスを通せば認識されます。

Mac,Linuxの場合はシンボリックリンク ``ln -s [generator-xxxxフォルダ絶対パス] generator-XXXX``でシンボリックリンクを作成します。

Windowsの場合はgenerator-XXXXフォルダにパスを通すか、パスが通っているフォルダにgenerator-をコピーして下さい。

## yo my generator

### generatorの実行

では早速generatorを実行してみましょう

新たにフォルダを作成し、そのフォルダの中で以下のコマンドを実行して下さい。

```sh

yo XXXX

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

### 選択肢の結果でもジュールをインストールする

## yo my gsubgenerator

### subgeneratorを作ってみる

### 設定を引き継いでsubgeneratorを動かしてみる

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


