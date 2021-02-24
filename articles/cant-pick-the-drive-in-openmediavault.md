---
title: "OpenMediaVaultで、共有フォルダ作成時にドロップダウンにデバイスが表示されない"
emoji: "🖊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["raspberrypi", "NAS", "openmediavault"]
published: true
---

やりたいこと
====

ラズベリーパイにUSB接続したHDDをOpenmediavaultの共有フォルダにしてLAN内のWindowsマシンからネットワークドライブとしてアクセスさせたい。

問題
=====

openmediavaultインストール後、共有フォルダを作成しようとしたが、モーダルウィンドウの「デバイス」ドロップダウンメニューにどのドライブも表示されない

![](https://storage.googleapis.com/zenn-user-upload/bmr4gn0f75i925fqui2ivvw891de)

解決方法
====

ドライブを一度アンマウントし、openmediavaultからマウントし直す。

「ファイルシステム」画面から該当のディスクを選択し「アンマウント」をクリックする。
![](https://storage.googleapis.com/zenn-user-upload/aromu4co45y76qa81amsubbggclv)

アンマウントできたら今度は「マウント」をクリックする。数十秒～数分間程度の処理が実行される。

共有フォルダ作成のドロップダウンにデバイスが表示される。
![](https://storage.googleapis.com/zenn-user-upload/aromu4co45y76qa81amsubbggclv)

参考
====

https://openmediavault.readthedocs.io/en/5.x/troubleshooting.html

公式ドキュメントのトラブルシュートの項目を見ると「openmediavaultのwebインターフェース以外でドライブをマウントしないでください。webインターフェースのマウント操作は、ドロップダウンに表示するのに必要な情報をデータベースに作成します」とあります。

どうやら、接続したHDDをすぐに使えるようにOSが気を効かせてマウントしてくれていたのが裏目に出ていたようです。


補足
====

筆者はストレージとしてWD DegitalのMyBookを使用したが、工場出荷状態では「My Book」というラベルが設定されており、マウント時に "The filesystem label contains blanks" というエラーが出た。これはドライブを一度別のWindowsマシンに接続してラベルをリネームすることでエラー回避した。

環境
====

Raspberry Pi 4 ModelB
Raspbian GNU/Linux 10 (buster)
openmediavault 5.6.0-1 (Usul)
