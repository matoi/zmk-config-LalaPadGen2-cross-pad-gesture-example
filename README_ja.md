# LalaPad Gen2 Cross-Pad Gesture Example

📄 **[English version](README.md)**

[zmk-driver-iqs9151 の cross-pad gesture 機能](https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture) を有効にした LalaPad Gen2 向けファームウェア設定の例です。

## Cross-Pad Gesture とは

左右分割キーボードの両側トラックパッドに**同時にタッチ**することで、特殊なジェスチャーを実行する機能です。

### ピンチ イン/アウト（ズーム）

両側のトラックパッドにそれぞれ **1本指** を置き、どちらかの指を**横方向**にスライドします。

- 指を外側に開く → **ズームイン**（拡大）
- 指を内側に閉じる → **ズームアウト**（縮小）

デフォルトでは Ctrl + スクロールとして動作します。modifier は設定で変更可能です（例: マウスボタン4）。

ピンチズームの方向が逆になる場合は、右側の `.conf` に `CONFIG_INPUT_IQS9151_CROSS_PAD_PINCH_INVERT=y` を追加してください。`zip_scroll_transform` でスクロール方向を反転している場合に必要です。

### プレス＆ホールド（ドラッグ）

片側のトラックパッドに **2本指** を置き、もう片側に **1本指** を置きます。

- 2本指側がドラッグの「ボタンを押し続ける」役割
- 1本指側でカーソルを動かして**ドラッグ操作**を行います
- 1本指側を離して置き直しても、2本指側が維持されていればドラッグは継続します
- 2本指側を離すとドラッグが終了します

### 3本指スワイプ（ブラウザの進む/戻る）

片側のトラックパッドに **3本指** を置き、もう片側に任意の本数の指を置いて**水平にスワイプ**します。

- 右にスワイプ → **ブラウザで進む**（デフォルト: macOS の Cmd+]）
- 左にスワイプ → **ブラウザで戻る**（デフォルト: macOS の Cmd+[）
- キーストロークのプリセットは `CONFIG_INPUT_IQS9151_CROSS_PAD_SWIPE_PRESET` で変更可能です（0=macOSブラウザ, 1=Windowsブラウザ, 2=macOSワークスペース切り替え）

## オリジナルからの変更点

この設定例では、元の [zmk-config-LalaPadGen2](https://github.com/ShiniNet/zmk-config-LalaPadGen2) に対して以下の変更のみを加えています:

- `config/west.yml` — ドライバのリポジトリとブランチを fork に変更
- `config/boards/shields/lalapadgen2/lalapadgen2_left.conf` — `CONFIG_INPUT_IQS9151_CROSS_PAD=y` を追加
- `config/boards/shields/lalapadgen2/lalapadgen2_right.conf` — `CONFIG_INPUT_IQS9151_CROSS_PAD=y` を追加
- `config/boards/shields/lalapadgen2/lalapadgen2.dtsi` — `cross_pad_gate` input-processor ノードを追加
- `config/boards/shields/lalapadgen2/lalapadgen2_left.overlay` — `cross-pad-peer-input` プロパティを追加
- `config/boards/shields/lalapadgen2/lalapadgen2_right.overlay` — `cross-pad-peer-input` プロパティを追加
- `config/lalapadgen2.keymap` — ペリフェラルリスナーの input-processor チェインに `<&cross_pad_gate>` を追加

## ファームウェアのビルド

このリポジトリのビルド済み最新ファームウェアは [Actions ページ](https://github.com/matoi/zmk-config-LalaPadGen2-cross-pad-gesture-example/actions) からダウンロードできます。

設定をカスタマイズする場合は、このリポジトリを fork し、fork 先で GitHub Actions を有効にしてください。push 時に自動でファームウェアがビルドされます。

> **注意:** 設定リポジトリに変更がなくても、[ドライバリポジトリ](https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture) が更新された場合はファームウェアの再ビルドが必要です。fork 先の Actions タブからワークフローを手動実行するか、空コミットを push してください。

## 注意事項

この機能は [ShiniNet/zmk-driver-iqs9151](https://github.com/ShiniNet/zmk-driver-iqs9151) 本家には含まれていない**独自拡張の PoC (Proof of Concept)** です。動作は無保証であり、予告なく変更・削除される可能性があります。本家ドライバとの互換性も保証されません。

## ドライバリポジトリ

https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture
