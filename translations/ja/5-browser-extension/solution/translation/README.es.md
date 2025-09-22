<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "cbaf73f94a9ab4c680a10ef871e92948",
  "translation_date": "2025-08-23T23:49:43+00:00",
  "source_file": "5-browser-extension/solution/translation/README.es.md",
  "language_code": "ja"
}
-->
# Carbon Triggerブラウザ拡張機能: 完全なコード

tmrowのCO2 Signal APIを使用して電力使用量を追跡し、地域の電力消費に関するリマインダーをブラウザで直接表示する拡張機能を作成します。このアドホックな拡張機能を使用することで、この情報に基づいて活動を決定するのに役立ちます。

![extension screenshot](../../../../../5-browser-extension/solution/start/extension-screenshot.png)

## 始める

[npm](https://npmjs.com)がインストールされている必要があります。このコードのコピーをコンピュータのフォルダにダウンロードしてください。

必要なすべてのパッケージをインストールします:

```
npm install
```

webpackを使用して拡張機能をビルドします:

```
npm run build
```

Edgeにインストールするには、ブラウザの右上にある「三点メニュー」から「拡張機能」パネルを見つけます。そこから「パッケージ化されていない拡張機能を読み込む」を選択して新しい拡張機能を読み込みます。プロンプトが表示されたら「dist」フォルダを開き、拡張機能が読み込まれます。使用するには、CO2 Signal APIのAPIキーが必要です（[こちらでメールで取得](https://www.co2signal.com/) - このページのボックスにメールアドレスを入力してください）と、[Electricity Map](https://www.electricitymap.org/map)に対応する地域コードが必要です（例えば、ボストンでは「US-NEISO」を使用します）。

![installing](../../../../../5-browser-extension/solution/start/install-on-edge.png)

APIキーと地域コードを拡張機能のインターフェースに入力すると、ブラウザの拡張機能バーにある色付きの点が地域のエネルギー使用量を反映して変化し、高エネルギー消費活動に関する適切な指標を提供します。この「点」システムのコンセプトは、カリフォルニアの排出量に関する[Energy Lollipop拡張機能](https://energylollipop.com/)から着想を得ました。

**免責事項**:  
この文書は、AI翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性を期すよう努めておりますが、自動翻訳には誤りや不正確な表現が含まれる可能性があります。元の言語で記載された文書が正式な情報源と見なされるべきです。重要な情報については、専門の人間による翻訳をお勧めします。この翻訳の使用に起因する誤解や誤認について、当方は一切の責任を負いません。