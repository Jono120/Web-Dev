<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "21b364c158c8e4f698de65eeac16c9fe",
  "translation_date": "2025-08-23T23:51:32+00:00",
  "source_file": "5-browser-extension/solution/translation/README.ms.md",
  "language_code": "ja"
}
-->
# Carbon Trigger ブラウザー拡張機能: 完全なコード

tmrowのCO2 Signal APIを使用して電力消費を検出し、地域の電力使用状況に関する通知をブラウザーで受け取れる拡張機能を構築します。この拡張機能を利用することで、提供される情報に基づいて活動を検討する助けになります。

![ブラウザー拡張機能のスクリーンショット](../../../../../5-browser-extension/extension-screenshot.png)

## 始め方

まず、[npm](https://npmjs.com)をインストールしてください。このコードのコピーをコンピューターのフォルダーにダウンロードします。

必要なパッケージをすべてインストールします:

```
npm install
```

webpackを使用して拡張機能をビルドします:

```
npm run build
```

Edgeにインストールするには、ブラウザー右上の「三点メニュー」から拡張機能パネルを開きます。そこから「Load Unpacked」を選択して新しい拡張機能を読み込みます。「dist」フォルダーを選択すると拡張機能がロードされます。使用するには、CO2 Signal APIのAPIキーが必要です（[こちらからメールで取得できます](https://www.co2signal.com/) - ページのボックスにメールアドレスを入力してください）と、[Electricity Map](https://www.electricitymap.org/map)に対応する地域コードが必要です（例えば、ボストンでは「US-NEISO」を使用します）。

![ダウンロード中](../../../../../5-browser-extension/install-on-edge.png)

APIキーと地域コードを拡張機能のインターフェースに入力すると、ブラウザー拡張バーの色付きドットが地域のエネルギー使用状況を反映して変化し、適切な活動の指針を提供します。この「ドット」システムのコンセプトは、カリフォルニア州向けにリリースされた[Energy Lollipopブラウザー拡張機能](https://energylollipop.com/)から着想を得ています。

**免責事項**:  
この文書は、AI翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性を追求しておりますが、自動翻訳には誤りや不正確な部分が含まれる可能性があることをご承知おきください。元の言語で記載された文書が公式な情報源とみなされるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の使用に起因する誤解や誤認について、当方は一切の責任を負いません。