---
title: "Xamarin.Macでコマンドライン引数を取得する"
emoji: "🤴"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["xamarin","mac","Cocoa","csharp"]
published: true
---

やりたいこと
====

Xamarin.Macのデスクトップアプリで、コマンドライン引数を受け取りたい

TL;DR
====
NSProcessInfo.ProcessInfo.Argumentsで取得できる

サンプルコード
====

```
string[] args = NSProcessInfo.ProcessInfo.Arguments;
```

string型配列で取得できます。実際に試してみたところ、第一引数にカレントディレクトリらしきパス（アプリケーションパッケージの内部でした）、第二引数にProcess Serial Numberが入っていました。

[NSProcessInfo - Apple Developer Documentation](https://developer.apple.com/documentation/foundation/nsprocessinfo)
[macos - OS X- strange -psn command line parameter when launched from Finder - Stack Overflow](https://stackoverflow.com/questions/10242115/os-x-strange-psn-command-line-parameter-when-launched-from-finder)

環境
====

Mac OS X 10.15.6
Visual Studio for Mac Community 8.8.1(build 37)
Xamarin Mac 7.0.0.15
XCode Version 12.