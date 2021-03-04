---
title: "Xamarin.Macでlog4netを利用する"
emoji: "🍎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["VisualStudio", "dotnet", "XamarinMac", "Mac", "csharp"]
published: true
---

やりたいこと
====

Xamarin.Macで作成したアプリに[log4net](https://logging.apache.org/log4net/)を導入して、ログ出力に利用する


Nugetでインストール
====

Visual Studioのメニューから「プロジェクト > NuGetパッケージの管理...」をクリックし、検索窓に「log4net」を入力してパッケージを見つけ、「パッケージの追加」をクリックしてインストールする。


設定はResourceから読み込む
====

log4netを使ってファイルやコンソールに出力を行うためには設定を行う必要があります。log4net.Config.XmlConfiguratorクラスを使って設定を読み込ませます。

設定を読み込ませる部分のソースコードは以下のような感じです。

```csharp
var assm = Assembly.GetExecutingAssembly();
var configStream = assm.GetManifestResourceStream("MyApp.Resources.log4net.config");
XmlConfigurator.Configure(configStream);
```

設定ファイルをリソースに含める方法は、以下の記事を参考にしてください。

[【Xamarin.Mac】プロジェクト内のリソースファイルを実行時にアプリから読み込む](https://zenn.dev/trpla226/articles/76f49b14a1b48a5d5d9b)

また、log4net.configの書き方については当記事では触れません。なおlog4netにはWindowsやLinuxの環境で利用できるがMacからは利用できない機能もあるようなので、留意してください。

ソースコードにログ出力を埋め込む
====

ログ出力を行う際にはまずロガーのインスタンスを生成します。

```csharp
private static readonly ILog logger
    = Modules.LogModule.Log.GetLogger("MyLogger");
```

GetLoggerメソッドの引数にはロガーの名前を指定しています。
[ドキュメント](https://logging.apache.org/log4net/release/sdk/html/M_log4net_LogManager_GetLogger_2.htm) によれば、すでにその名前のロガーインスタンスが存在していればそれを取得し、そうでなければ新しいインスタンスを生成するとあります。

ロガーのインスタンスが生成できれば、出力したいログレベルに応じてロガーのインスタンスメソッドを呼ぶことで、log4net.configで設定したアペンダでログが出力されます。

```csharp
logger.Error(exception);
logger.Warn("設定を見なおしてください");
logger.Info("何かの処理が行われました");
logger.Debug($"myData:{data}");
logger.Trace($"myData:{data}");
```

注意
====

設定ファイルを読み込むConfigメソッドが実行される前にログ出力メソッドを呼んでしまうと、当然ながらそのメソッドでのログ出力は行われません。ありがちなミスなので気をつけましょう。


環境
====

Mac OS X 10.15.6
Visual Studio for Mac Community 8.8.1(build 37)
Xamarin Mac 7.0.0.15
XCode Version 12.2