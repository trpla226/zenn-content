---
title: "Xamarin.MacでSpecialFolderを利用する"
emoji: "📁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Xamarin.Mac", "csharp"]
published: true
---

.NET Frameworkには、特殊なフォルダのパスを取得するメソッドがある。
```csharp
System.Environment.GetFolderPath(Environment.SpecialFolder.DesktopDirectory)
```

このメソッドは、SpecialFolder列挙体を渡すことでパスを取得するフォルダを指定する。この列挙体の中には、「Windows」などの、環境依存なものもある。Xamarin.MacでもWindowsフォルダのパスの取得を試みることができるが、どのような結果になるか気になったため調べてみた。また、せっかくなのでSpecialFolder列挙体全てについて結果を確認してみた。

調査結果
====

空欄は空文字列で、nullになることはない。

|SpecialFolder列挙体|パス|
| ---- | ---- |
|Desktop|/Users/<ユーザ名>/Desktop|
|Programs| |
|MyDocuments|/Users/<ユーザ名>|
|Favorites|/Users/<ユーザ名>/Library/Favorites|
|Startup||
|Recent||
|SendTo||
|StartMenu||
|MyMusic|/Users/<ユーザ名>/Music|
|MyVideos|/Users/<ユーザ名>/Videos|
|DesktopDirectory|/Users/<ユーザ名>/Desktop|
|MyComputer||
|NetworkShortcuts||
|Fonts|/Users/<ユーザ名>/Library/Fonts|
|Templates|/Users/<ユーザ名>/Templates|
|CommonStartMenu||
|CommonPrograms||
|CommonStartup||
|CommonDesktopDirectory||
|ApplicationData|/Users/<ユーザ名>/.config|
|PrinterShortcuts||
|LocalApplicationData|/Users/<ユーザ名>/.local/share|
|InternetCache|/Users/<ユーザ名>/Library/Caches|
|Cookies||
|History||
|CommonApplicationData|/usr/share|
|Windows||
|System||
|ProgramFiles|/Applications|
|MyPictures|/Users/<ユーザ名>/Pictures|
|UserProfile|/Users/<ユーザ名>|
|SystemX86||
|ProgramFilesX86||
|CommonProgramFiles||
|CommonProgramFilesX86||
|CommonTemplates|/usr/share/templates|
|CommonDocuments||
|CommonAdminTools||
|AdminTools||
|CommonMusic||
|CommonPictures||
|CommonVideos||
|Resources||
|LocalizedResources||
|CommonOemLinks||
|CDBurning||


コード
====

上記の出力を得るために以下のコードを使用した

```csharp
foreach(Environment.SpecialFolder f in Enum.GetValues(typeof(Environment.SpecialFolder)))
{
    var name = f.ToString();
    var path = Environment.GetFolderPath(f);
    logger.Info($"|{name}|{path ?? "null"}|");
}
```

環境
====

Mac OS X 10.15.6
Visual Studio for Mac Community 8.8.1(build 37)
Xamarin Mac 7.0.0.15
XCode Version 12.