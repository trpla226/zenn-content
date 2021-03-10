---
title: "Xamarin.Macで動的にlog4netの設定を行う"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["XamarinMac", "CSharp", "log4net"]
published: false
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
   

ファイルから設定を読み込む
----

Resource下のlog4net.configをファイルストリームとしてXMLConfiguratorに渡すことで設定を行う。Resourceの設定方法はこちらの記事を参照のこと。

設定に必要な情報（今回はユーザのホームディレクトリ）を取得する
----

Appenderのインスタンスを取得する 
----


AppenderのFileプロパティを設定する
----

設定したプロパティを反映する
----
 

ハマったポイント
====

 当初、Appenderを取得して設定を行う処理をデフォルトビューのコントローラーのViewDidLoadメソッドに記述していた。
 ファイルからの設定読み込みをAppDelegateのDidFinishLaunchに記述していたが、実はDidFinishLaunchはViewDidLoadが完了した後に呼ばれる。これにより、Appenderも何も生成されていない段階でAppenderの取得を試み用としてハマってしまった。