# **ココフォリア追加チャットパレット**

<sub>Userscript / Tampermonkey ・ by Apocrypha (a.k.a. ぬべ太郎) – MIT License</sub>

---

## ✨ これは何？

[ココフォリア] のチャットパレットを  
*ボタン・ミニスクリプト・変数* で超拡張する Tampermonkey スクリプトです。

* **ボタン化** : よく使うコマンドをワンクリック  
* **ミニ JS** : `[ ... ]` で囲った JS で判定 / ダイス結果を自動処理  
* **動的変数** : `:HP-{NUM}` や `NUM += 1` のようにゲーム中に書き換え  
* **ファイル保存** : `.ccp` にエクスポートして仲間へ共有

---

## 🖥️ インストール

1. ブラウザに **Tampermonkey** を入れる  
2. このリポジトリの  
   <kbd>Userscript.user.js</kbd> を **Raw** で開き → `Install`  

> **更新時**  
> スクリプトのバージョンが変わったら自動でリロード確認ダイアログが出ます。

---

## ⌨️ ホットキー

| キー | 動作                       |
|------|---------------------------|
| **Alt + P** | パレット表示/非表示 |
| **Alt + O** | コマンド編集        |
| **Alt + V** | 変数編集            |
| **A**        | Auto スクリプト画面（開発中） |

---

## 📐 ウィンドウ操作

* **ドラッグ** … タイトルバーを掴んで移動（座標は自動保存）  
* **リサイズ** … 右下の <kbd>↘︎</kbd> で  
* **⤓ / ⤒** … 設定を **エクスポート / インポート**  
  * `.ccp` は JSON ベース  
  * エクスポートすると **ローカル設定が初期化** → 共有しやすい

---

## 📝 コマンド編集（基本）

:AP-1  
[ WAIT 500 ]  
CCB<=70 【攻撃】  
[ if (CMessage[0].Find('S')) CMessage[0].Send('1d6 【ダメージ】'); ]

* 1行 = 1 コマンドボタン  
* `[ WAIT ms ]` … ミリ秒待機  
* `[ ... ]` … JavaScript ブロック

### スクリプトで使えるもの

| オブジェクト | メソッド | 戻り値 | 例 |
|--------------|----------|--------|----|
| **`SEnd()`** | – | 即時終了 | `SEnd();` |
| **`CMessage[n]`** | `.Find('S')` | bool | 成功/スペシャルを含む？ |
| | `.FindAt('M')` | number | `M` の出現数 |
| | `.GetNum()` | number | `… ＞ 12` → `12` |
| | `.Send(':HP-5')` | void | 送信（内部で WAIT 遵守） |

> **KW_ALIAS**  
> `'S'` = 成功 / スペシャル、 `'F'` = 致命的失敗 …など。  
> `CMessage[0].Find('S')` のように使えます。

---

## 📦 エクスポート内容

```jsonc
{
  "version": 1,
  "cmds":   [ /* ボタンとコマンド配列 */ ],
  "vars":   [ /* 変数名 / 値 */ ],
  "autoCmd": [ /* Auto スクリプト */ ]
}
```

ファイル名は `追加チャット情報YYYY-MM-DDTHH-MM-SS.ccp` が初期値。  
ダイアログで好きな名前・場所に変更可。

[MIT](LICENSE)  
Copyright © Apocrypha

> 本スクリプトとココフォリア運営様とは一切関係ありません。  
> 利用は自己責任でお願いします。


_（見てわかると思うんだけど普通にこのREADMEはChatGPTに適当に投げて作りました。多分正確かもしれない）_
