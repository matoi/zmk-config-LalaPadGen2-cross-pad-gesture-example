# LalaPad Gen2 Cross-Pad Gesture Example

[zmk-driver-iqs9151 の cross-pad gesture 機能](https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture) を有効にした LalaPad Gen2 向けファームウェア設定の例です。

## Cross-Pad Gesture とは

左右分割キーボードの両側トラックパッドに同時にタッチすることで、特殊なジェスチャーを実行する機能です。

| 指数 (MAX) | ジェスチャー | 動作 |
|-----------|------------|------|
| 1 | ピンチ イン/アウト | modifier + スクロール（ズーム） |
| 2 | プレス＆ホールド | BTN_0 ホールド + カーソル移動（ドラッグ） |

## オリジナルからの変更点

この設定例では、元の [zmk-config-LalaPadGen2](https://github.com/ShiniNet/zmk-config-LalaPadGen2) に対して以下の変更のみを加えています:

- `config/west.yml` — ドライバのリポジトリとブランチを fork に変更
- `config/boards/shields/lalapadgen2/lalapadgen2_left.conf` — `CONFIG_INPUT_IQS9151_CROSS_PAD=y` を追加
- `config/boards/shields/lalapadgen2/lalapadgen2_right.conf` — `CONFIG_INPUT_IQS9151_CROSS_PAD=y` を追加
- `config/boards/shields/lalapadgen2/lalapadgen2_left.overlay` — `cross-pad-peer-input` プロパティを追加
- `config/boards/shields/lalapadgen2/lalapadgen2_right.overlay` — `cross-pad-peer-input` プロパティを追加

## ドライバリポジトリ

https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture
