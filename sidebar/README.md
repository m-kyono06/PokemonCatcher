# PokemonCatcher 左右アイコン表示

ベースは [Lua対応版melonDS v2.0.1-lua.14](https://github.com/RicksCodes/MelonDS_Android_wLuaScript/tree/v2.0.1-lua.14) です。次の日本語版に対応しています。Luaを読み込むと、起動中のバージョンに合わせて通常出現候補を表示します。

| 作品 | 読み込むLua |
| --- | --- |
| ダイヤモンド（`ADAJ`）、パール（`APAJ`）、プラチナ（`CPUJ`） | [`dppt_jp_sidebar.lua`](./dppt_jp_sidebar.lua) |
| ハートゴールド（`IPKJ`）、ソウルシルバー（`IPGJ`） | [`hgss_jp_sidebar.lua`](./hgss_jp_sidebar.lua) |

上画面の表示枠をもとに左右の余白を計算します。左に現在地と陸上・いわくだき、右になみのり・釣りの候補を表示します。1行に最大2匹ずつ並べ、余白に収まるようアイコンの表示サイズを調整します。捕獲済みのポケモンも同じ位置に残り、暗くなったアイコンの右下にモンスターボールが付きます。片側しか空いていない場合は、空いている側にまとめます。DS画面のレイアウト設定はそのまま使えます。

## ビルド

配布元の `v2.0.1-lua.14` のソースを取得し、ソースのルートで `git apply /path/to/melonds-sidebar.patch` を実行します。配布元のREADMEに従ってAndroid SDK・NDKを準備し、`./gradlew :app:assembleGitHubProdDebug` でビルドします。このパッチのデバッグ版は `me.magnum.melonds.catcher` で、既存のmelonDSと別にインストールできます。

## アイコン画像を読み込む

1. [改修版APK（ARM64）](./melonds-pokemoncatcher-v14-arm64.apk) をインストールします。すでに横2匹表示に対応した改修版を使用中なら、使う作品に合わせてLuaを読み込んでください。
2. [`pokemon-icons-gen4.png`](./pokemon-icons-gen4.png) と、上の表で選んだLuaを端末へコピーします。
3. 改修版のポーズメニューで **Lua scripts → PokemonCatcher アイコン画像を読み込む** を選び、`pokemon-icons-gen4.png` を読み込みます。
4. 日本語版のゲームを起動し、**Lua scripts → Load script…** で作品に合ったLuaを読み込みます。

アイコンの出典は [PokéAPI Sprites の第4世代アイコン](https://github.com/PokeAPI/sprites/tree/master/sprites/pokemon/versions/generation-iv/icons) です。全国図鑑番号1〜493のPNGを1枚に並べています。端末でのアイコン表示はオフラインで動作します。

モンスターボールの画像は [PokéAPI Sprites のアイテム画像](https://github.com/PokeAPI/sprites/blob/master/sprites/items/poke-ball.png) を使用しています。

通常出現のバージョン差は [pret/pokeheartgold](https://github.com/pret/pokeheartgold/blob/master/files/fielddata/encountdata/gs_enc_data.json) を参照しています。両バージョンの描画データを模擬メモリで確認済みです。ハートゴールドのAndroid実機での動作は未確認です。

ダイヤモンド・パールは [pret/pokediamond](https://github.com/pret/pokediamond)、プラチナは [pret/pokeplatinum](https://github.com/pret/pokeplatinum) の通常出現データを参照しています。大量発生、ポケトレ、ダブルスロットなどによる追加候補は対象外です。模擬メモリで3作品の出現候補と捕獲表示を確認済みです。Android実機での動作は未確認です。
