# Phi-3.5-Instruct WebGPU RAG Chatbot

## WebGPUとRAGパターンを活用したデモ

Phi-3.5 Onnx Hostedモデルを使用したRAGパターンは、リトリーバル・オーグメンテッド・ジェネレーション（RAG）アプローチを活用し、効率的なAIデプロイメントを実現します。このパターンは、ドメイン固有のタスク向けにモデルを微調整するための重要な手法であり、高品質、コスト効率、長い文脈理解を提供します。Azure AIのスイートの一部として、多様な業界のカスタマイズニーズに応えるため、簡単に見つけて試し、使用できる幅広いモデルが用意されています。

## WebGPUとは
WebGPUは、ウェブブラウザからデバイスのグラフィックス処理ユニット（GPU）に直接効率的にアクセスできるように設計された最新のウェブグラフィックスAPIです。WebGLの後継を目指しており、以下のような主要な改善点を提供します：

1. **最新GPUとの互換性**: WebGPUは、現代のGPUアーキテクチャとシームレスに連携するよう設計されており、Vulkan、Metal、Direct3D 12といったシステムAPIを活用します。
2. **性能向上**: 一般的なGPU計算や高速な操作をサポートしており、グラフィックスレンダリングだけでなく機械学習タスクにも適しています。
3. **高度な機能**: より複雑で動的なグラフィックスや計算ワークロードを可能にする高度なGPU機能へのアクセスを提供します。
4. **JavaScriptの負荷軽減**: より多くのタスクをGPUにオフロードすることで、JavaScriptの負荷を大幅に軽減し、パフォーマンスの向上とスムーズな体験を実現します。

WebGPUは現在、Google Chromeなどのブラウザでサポートされており、他のプラットフォームへのサポート拡大が進行中です。

### 03.WebGPU
必要な環境：

**対応ブラウザ:**
- Google Chrome 113以上
- Microsoft Edge 113以上
- Safari 18 (macOS 15)
- Firefox Nightly

### WebGPUを有効にする：

- Chrome/Microsoft Edgeの場合 

`chrome://flags/#enable-unsafe-webgpu`フラグを有効にします。

#### ブラウザを開く:
Google ChromeまたはMicrosoft Edgeを起動します。

#### フラグページにアクセス:
アドレスバーに`chrome://flags`と入力してEnterキーを押します。

#### フラグを検索:
ページ上部の検索ボックスに「enable-unsafe-webgpu」と入力します。

#### フラグを有効化:
検索結果のリストから#enable-unsafe-webgpuフラグを見つけます。

その隣のドロップダウンメニューをクリックし、「Enabled」を選択します。

#### ブラウザを再起動:

フラグを有効にした後、変更を適用するためにブラウザを再起動する必要があります。ページ下部に表示される「Relaunch」ボタンをクリックしてください。

- Linuxの場合、`--enable-features=Vulkan`を使用してブラウザを起動します。
- Safari 18 (macOS 15)ではWebGPUがデフォルトで有効になっています。
- Firefox Nightlyでは、アドレスバーにabout:configと入力し、`set dom.webgpu.enabled to true`を設定します。

### Microsoft Edge用GPUの設定

WindowsでMicrosoft Edge用の高性能GPUを設定する手順は以下の通りです：

- **設定を開く:** スタートメニューをクリックし、「設定」を選択します。
- **システム設定:** 「システム」から「ディスプレイ」に進みます。
- **グラフィックス設定:** 下にスクロールして「グラフィックス設定」をクリックします。
- **アプリを選択:** 「設定を選択するアプリの種類」で「デスクトップアプリ」を選び、「参照」をクリックします。
- **Edgeを選択:** Edgeのインストールフォルダ（通常は`C:\Program Files (x86)\Microsoft\Edge\Application`）に移動し、`msedge.exe`を選択します。
- **優先設定を設定:** 「オプション」をクリックし、「高パフォーマンス」を選択して「保存」をクリックします。
これにより、Microsoft Edgeが高性能GPUを使用してパフォーマンスを向上させるようになります。
- **再起動:** これらの設定を反映させるために、マシンを再起動してください。

### サンプル: [このリンク](https://github.com/microsoft/aitour-exploring-cutting-edge-models/tree/main/src/02.ONNXRuntime/01.WebGPUChatRAG)をクリックしてください。

**免責事項**:  
本書類は、AIによる機械翻訳サービスを使用して翻訳されています。正確さを追求しておりますが、自動翻訳には誤りや不正確な表現が含まれる可能性があります。本書類の原文（元の言語）が信頼できる情報源として優先されるべきです。重要な情報については、専門の人間による翻訳を推奨します。本翻訳の利用に起因する誤解や誤認について、当方は一切の責任を負いかねます。