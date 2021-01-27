---
title: "Xamarin.MacのソリューションにF#のクラスライブラリプロジェクトを追加する"
emoji: "👋"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

やること
====

Xamarin.Mac/C#/.Net Framework4.8で開発を行っているソリューションに、F#のクラスライブラリプロジェクトを追加する

手順
====

コンソールでソリューションのディレクトリを開く


donet new コマンドで言語、出力先ディレクトリ、ターゲットフレームワークを指定して新たなプロジェクトを作成します。
今回の環境ではターゲットフレームワークの既定値はnet5.0ですが、この設定でプロジェクトを作成すると既存の.Net Framework4.8のプロジェクトから参照することができません。また、プロジェクト作成後に変更することもできないので、dotnet new時に指定しておきます。ここではnetstandard2.0を選択しました。

```
dotnet new classlib --language="F#" -o myLibrary --framework netstandard2.0
```

メモ
====

Visual StudioのGUIからF#のクラスライブラリプロジェクトを作成したところ、ターゲットフレームワークは.NET Framework4.8(net48)となり、選択できるターゲットフレームワークも.NET Frameworkの中から選ぶようになった。一方でdotnetコマンドで作成した場合の既定値は.NET 5.0(net5.0)となった。また、dotnetコマンドではnet48は選択できなかった。なぜこのような挙動になるのか不明。

呼び出す側のアプリのフレームワーク

.NET Modern  dotnetコマンドでnetstandard2.1を指定
.NET Framework 4.8 VisualStudioのソリューションウィンドウから作成 or dotnetコマンドでnetstandard2.1を指定



環境
====

Mac OS X 10.15.6
Visual Studio for Mac Community 8.8.1(build 37)
Xamarin Mac 7.0.0.15
XCode Version 12.2
