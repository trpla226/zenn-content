---
title: "Photoshopのレイヤーエフェクトを使って長方形で囲む小技"
emoji: "🖍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["photoshop"]
published: true 
---

やりたいこと
====

こんな感じに、目立たせたい部分を四角く囲みたい。WindowsなのでSkitchは使えないし、ScreenPressoもなぜか自分の環境では動かなかった。

![](https://storage.googleapis.com/zenn-user-upload/bla5nyqj22nnuaumw1t1dsp4qwfe)

やりかた
====

Photoshopに画像を読み込む
----

任意の手段で撮ったスクリーンショットを、ファイルを開いたりペーストしたりしてPhotoshopに読み込みます。レイヤー名が「背景」になっていたら適当なレイヤー名に変更します。

![](https://storage.googleapis.com/zenn-user-upload/25q7fq1uguhmfg9fgl6seln2hpwo)

レイヤーを追加
----

枠を描くレイヤーを作ります。レイヤーパネルの下の四角にプラスのマークでも、メインメニュー > レイヤー > 新規(N) > レイヤー でも、Ctrl + Shift + N でもいいです。

![](https://storage.googleapis.com/zenn-user-upload/as2qvzgffqdtypd0pincujta41bl)

選択して塗りつぶし
----

矩形選択ツールで囲みたい部分を選択し

![](https://storage.googleapis.com/zenn-user-upload/71qe6c5pifew5ivg2jeh4hgjco44)

先ほど作ったレイヤー上でホワイトで塗りつぶします。

![](https://storage.googleapis.com/zenn-user-upload/qrhl5e1j0jv2elxr4aardgnrngyo)

こうなります。

![](https://storage.googleapis.com/zenn-user-upload/gejehhu322ehhxfsql59qfqc6km1)

レイヤーの種類変更
----

ホワイトで塗りつぶしを行ったほうのレイヤーの種類を「乗算」に変更します。乗算では白(#ffffff)は完全な透明になります。 

境界線レイヤーエフェクトを追加
----

レイヤーパネル下部の「fx」というボタンをクリックし、「境界線...」を選びます。
サイズで線の太さを変更し、好きなカラーを選びます。今回は太さ5pxでSkitchっぽい色にしてみました。

![](https://storage.googleapis.com/zenn-user-upload/pzapiw8m74qh3dof73pwpcbzl4ea)

白で塗りつぶした部分は透明になり、境界線は通常通り表示されることで枠を描画することができました。

![](https://storage.googleapis.com/zenn-user-upload/8bynmyk5tw0xfn6w7rdpl76004pf)

環境
====

Windows 10 Pro
Photoshop 2021