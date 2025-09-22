<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "26fd39046d264ba185dcb086d3a8cf3e",
  "translation_date": "2025-08-23T23:41:50+00:00",
  "source_file": "5-browser-extension/start/README.md",
  "language_code": "ja"
}
-->
# Carbon Trigger ブラウザー拡張機能: スターターコード

tmrowのC02 Signal APIを使用して電力使用量を追跡し、地域の電力使用状況がどれほど重いかをブラウザーで直接確認できるリマインダーを作成するブラウザー拡張機能を構築します。この拡張機能を臨時で使用することで、この情報に基づいて活動に関する判断を下す助けになります。

![拡張機能のスクリーンショット](../../../../5-browser-extension/extension-screenshot.png)

## はじめに

[npm](https://npmjs.com) をインストールする必要があります。このコードをコンピューターのフォルダーにダウンロードしてください。

必要なパッケージをすべてインストールします:

```
npm install
```

webpackを使用して拡張機能をビルドします:

```
npm run build
```

Edgeにインストールするには、ブラウザーの右上にある「三点メニュー」から拡張機能パネルを見つけます。そこで「Load Unpacked」を選択して新しい拡張機能を読み込みます。プロンプトで「dist」フォルダーを開くと拡張機能が読み込まれます。使用するには、CO2 SignalのAPIキーが必要です ([こちらからメールで取得](https://www.co2signal.com/) - このページのボックスにメールアドレスを入力してください) と、[Electricity Map](https://www.electricitymap.org/map) に対応する地域コード ([地域コードはこちら](http://api.electricitymap.org/v3/zones)) が必要です。例えば、ボストンでは「US-NEISO」を使用します。

![インストール手順](../../../../5-browser-extension/install-on-edge.png)

APIキーと地域コードを拡張機能のインターフェースに入力すると、ブラウザー拡張機能バーの色付きドットが地域のエネルギー使用状況を反映して変化し、エネルギー消費の多い活動を行うべきかどうかの指針を示します。この「ドット」システムのコンセプトは、カリフォルニア州の排出量に関する [Energy Lollipop 拡張機能](https://energylollipop.com/) から着想を得ました。

**免責事項**:  
この文書は、AI翻訳サービス [Co-op Translator](https://github.com/Azure/co-op-translator) を使用して翻訳されています。正確性を追求しておりますが、自動翻訳には誤りや不正確な表現が含まれる可能性があることをご承知おきください。原文（元の言語で記載された文書）が公式な情報源として優先されるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の使用に起因する誤解や誤認について、当方は一切の責任を負いません。