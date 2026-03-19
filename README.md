# LalaPad Gen2 Cross-Pad Gesture Example

[zmk-driver-iqs9151 の cross-pad gesture 機能](https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture) を有効にした LalaPad Gen2 向けファームウェア設定の例です。

## Cross-Pad Gesture とは

左右分割キーボードの両側トラックパッドに**同時にタッチ**することで、特殊なジェスチャーを実行する機能です。

### ピンチ イン/アウト（ズーム）

両側のトラックパッドにそれぞれ **1本指** を置き、どちらかの指を**横方向**にスライドします。

- 指を外側に開く → **ズームイン**（拡大）
- 指を内側に閉じる → **ズームアウト**（縮小）

macOS の場合、デフォルトでは Ctrl + スクロールとして動作します。modifier は設定で変更可能です（例: マウスボタン4）。

### プレス＆ホールド（ドラッグ）

片側のトラックパッドに **2本指** を置き、もう片側に **1本指** を置きます。

- 2本指側がドラッグの「ボタンを押し続ける」役割
- 1本指側でカーソルを動かして**ドラッグ操作**を行います
- 1本指側を離して置き直しても、2本指側が維持されていればドラッグは継続します
- 2本指側を離すとドラッグが終了します

## オリジナルからの変更点

この設定例では、元の [zmk-config-LalaPadGen2](https://github.com/ShiniNet/zmk-config-LalaPadGen2) に対して以下の変更のみを加えています:

- `config/west.yml` — ドライバのリポジトリとブランチを fork に変更
- `config/boards/shields/lalapadgen2/lalapadgen2_left.conf` — `CONFIG_INPUT_IQS9151_CROSS_PAD=y` を追加
- `config/boards/shields/lalapadgen2/lalapadgen2_right.conf` — `CONFIG_INPUT_IQS9151_CROSS_PAD=y` を追加
- `config/boards/shields/lalapadgen2/lalapadgen2_left.overlay` — `cross-pad-peer-input` プロパティを追加
- `config/boards/shields/lalapadgen2/lalapadgen2_right.overlay` — `cross-pad-peer-input` プロパティを追加

## ドライバリポジトリ

https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture
