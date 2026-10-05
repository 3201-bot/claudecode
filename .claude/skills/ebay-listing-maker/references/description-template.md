# 商品説明のHTMLテンプレート

商品説明は必ずこのHTML骨格で生成する(プレーンテキストで出さない)。e-STOCKERの説明エディタにはソースモード(またはエディタAPI)でHTMLごと流し込む。

## デフォルトテンプレート

```html
<div style="font-family:Arial,Helvetica,sans-serif;max-width:800px;color:#222;line-height:1.6;">
  <h2 style="border-bottom:2px solid #1e3a5f;padding-bottom:8px;">{{英語タイトル}}</h2>

  <p style="background:#f5f7fa;padding:10px 14px;border-left:4px solid #1e3a5f;">
    <b>CONDITION NOTES</b> (please read)
  </p>
  <ul>
    <li><b>Operation:</b> {{動作状態。仕入元の記載に忠実に}}</li>
    <li><b>Appearance:</b> {{外観。傷・スレ・錆は具体的に明記}}</li>
    <li><b>Includes:</b> {{付属品。「写真にある物が全て」と明記}}</li>
  </ul>

  <h3 style="color:#1e3a5f;">SHIPPING</h3>
  <p>Ships from Japan with full tracking. Carefully packed with cushioning.</p>

  <h3 style="color:#1e3a5f;">NOTE</h3>
  <p>Please check all photos carefully. Feel free to message me with any questions!</p>
</div>
```

## 生成ルール

- CONDITION NOTESの行は商材に合わせて追加する(カメラなら Optics / Viewfinder、時計なら Battery / Movement、ゲーム機なら Screen / Buttons など)
- **内容は必ず仕入元の実物ページから**。過大表記の禁止(仕入元が「傷あり」なら Excellent と書かない)
- ジャンク・訳あり品は、CONDITION NOTESの**先頭行**に症状を明記する(例: <li><b>FOR PARTS:</b> Untested / Battery dead — sold as-is.</li>)
- eBayの説明ではscriptや外部読み込みは使わない。インラインstyleの単純なHTMLに留める

## ユーザー独自テンプレート対応

ユーザーが自分のテンプレート(HTMLまたは文面)をチャットに貼ってきたら:
1. 作業フォルダに `description-template-custom.html` として保存する
2. 以後の説明生成はそのテンプレートをデフォルトにする
3. 「テンプレートを標準に戻して」と言われたら本ファイルのデフォルトに戻す
