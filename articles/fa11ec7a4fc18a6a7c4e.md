---
title: "UnityのImageの画像の透明度を簡単に変更するC#クラス拡張"
emoji: "🖼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unity", "csharp"]
published: true
---

やりたいこと
====

ScriptからImage Componentのついた画像の透明度を変えたい

課題
====

TransformやImageには透明度のパラメータがなく、Alphaを設定した新しいColorインスタンスをセットする必要がある。
Imageに既にColorが設定されていた場合、元の色味を保持したまま半透明にするには、一度Colorを取得してrgbの各チャンネルの輝度を元にColorインスタンスを生成する必要があり、記述が冗長になりがち。

解決策
====

Imageコンポーネントを拡張し、元の色味の取得と新しいColorのインスタンス化・セットを行うようにする。

拡張のソースコード
====

```csharp
// ImageExt.cs
// author: trpla226
using UnityEngine;
using UnityEngine.UI;

public static class ImageExt
{
    /// <summary>
    /// Imageの不透明度を設定する
    /// </summary>
    /// <param name="image">設定対象のImageコンポーネント(this)</param>
    /// <param name="alpha">不透明度。0=透明 1=不透明</param>
    public static void SetOpacity(this Image image, float alpha)
    {
        var c = image.color;
        image.color = new Color(c.r, c.g, c.b, alpha);
    }
}
```

使い方
====

 1. 制御先のImageのついたGameObjectを用意します。
 1. 上記のImageExt.csをAsset内に配置します。
 2. 制御元のC#スクリプトを用意してImageExtをusing staticします。
 3. 制御元のC#スクリプトで、Imageコンポーネントへの参照を取得します。
 4. 取得したImageコンポーネントにSetOpacity()メソッドが追加されているのでこれを使って不透明度を設定します。


使用サンプル
====

予めScene上で透明にしておいたImageを不透明にするサンプルです

``` csharp
// 制御元スクリプト
using static ImageExt;

// 開始時に不透明にする
void Start() {
    // GameObjectの取得
    GameObject target = GameObject.Find("Target");
    // Imageの取得
    Image image = target.GetComponent<Image>();
    // 0=透明 1=不透明なので、1.0で完全に不透明になる
    image.SetOpacity(1.0f);
}

```

おわりに
====

C#のextensionは応用範囲が広く、簡潔に書くのに役立つので不透明度以外にも色々なところで使えると思います。ぜひやってみてください。