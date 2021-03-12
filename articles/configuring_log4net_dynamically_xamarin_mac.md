---
title: "Xamarin.Macで動的にlog4netの設定を行う"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["XamarinMac", "CSharp", "log4net"]
published: true
---

やりたいこと
====

Xamarin.Macを使用したアプリで、log4netの設定をアプリ起動後にプログラムから変更したい。
今回は、ユーザのホームディレクトリを取得してそれをログ出力のフォルダに設定する。

手順
====    

 1. ファイルから設定を読み込む
 1. 設定に必要な情報（今回はユーザのホームディレクトリ）を取得する
 1. Appenderのインスタンスを取得する 
 1. AppenderのFileプロパティを設定する
 1. 設定したプロパティを反映する

なお、「ファイルから設定をを読み込む」 については、[【Xamarin.Mac】プロジェクト内のリソースファイルを実行時にアプリから読み込む](https://zenn.dev/trpla226/articles/76f49b14a1b48a5d5d9b) の手順で既に設定ファイルがリソースに追加されていることを前提としています。
   

実際のコード
====

```csharp
// 1. ファイルから設定を読み込む
// Resource下のlog4net.configをファイルストリームとしてXMLConfiguratorに渡すことで設定を行う。
var configStream = Assembly
    .GetExecutingAssembly();
    .GetManifestResourceStream("MyApp.Resources.log4net.config");
XmlConfigurator.Configure(configStream);

// 2. 設定に必要な情報（今回はユーザのホームディレクトリ）を取得する
var personalFolderPath = Environment.GetFolderPath(
    Environment.SpecialFolder.Personal);

// 3. Appenderのインスタンスを取得する 
var appender = LogManager.GetRepository()
    .GetAppenders()
    .OfType<FileAppender>()
    .SingleOrDefault();

// 4. AppenderのFileプロパティを設定する
appender.File = personalFolderPath + "/MyApp.log";

// 5. 設定したプロパティを反映する
appender.ActivateOptions(); 
```

ハマったポイント
====

 当初、Appenderを取得して設定を行う処理をデフォルトビューのコントローラーのViewDidLoadメソッドに記述していた。
 ファイルからの設定読み込みをAppDelegateのDidFinishLaunchingに記述していたが、実はDidFinishLaunchはViewDidLoadが完了した後に呼ばれる。これにより、Appenderも何も生成されていない段階でAppenderの取得を試み用としてハマってしまった。

 環境
 ====

Mac OS X 10.15.6
Visual Studio for Mac Community 8.8.1(build 37)
Xamarin Mac 7.0.0.15
XCode Version 12.2
