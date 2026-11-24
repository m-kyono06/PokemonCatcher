# PokemonCatcher 左右アイコン表示

ベースは [Lua対応版melonDS v2.0.1-lua.14](https://github.com/RicksCodes/MelonDS_Android_wLuaScript/tree/v2.0.1-lua.14) です。

上画面の表示枠をもとに左右の余白を計算します。左に現在地と陸上・いわくだき、右になみのり・釣りの候補を表示します。片側しか空いていない場合は、空いている側にまとめます。DS画面のレイアウト設定はそのまま使えます。

## ビルド

配布元の `v2.0.1-lua.14` のソースを取得し、ソースのルートで `git apply /path/to/melonds-sidebar.patch` を実行します。配布元のREADMEに従ってAndroid SDK・NDKを準備し、`./gradlew :app:assembleGitHubProdDebug` でビルドします。このパッチのデバッグ版は `me.magnum.melonds.catcher` で、既存のmelonDSと別にインストールできます。

## アイコン画像を読み込む

1. 同梱の `pokemon-icons-gen4.png` と `soulsilver_jp_sidebar.lua` を端末へコピーします。
2. 改修版のポーズメニューで **Lua scripts → PokemonCatcher アイコン画像を読み込む** を選び、`pokemon-icons-gen4.png` を読み込みます。
3. **Lua scripts → Load script…** で同梱の `soulsilver_jp_sidebar.lua` を読み込みます。

アイコンの出典は [PokéAPI Sprites の第4世代アイコン](https://github.com/PokeAPI/sprites/tree/master/sprites/pokemon/versions/generation-iv/icons) です。全国図鑑番号1〜493のPNGを1枚に並べています。端末でのアイコン表示はオフラインで動作します。
