# ame-iwato

画面をロックする小さなコマンド(swaylock の代わり。名前は天岩戸から)。

[ame-shell](https://github.com/TatsuyaM2667/ame-shell)(Wayland のデスクトップシェル)の一部を、単独で使えるように切り出したものです。
ame-shell は画面の要らない仕事を、1 つのことをして標準入出力でやりとりする小さなコマンドに分けています。これはその 1 つです。

## 使い方

```text
ame-iwato: 画面をロックする小さな道具(swaylock の代わり)。
名前は天照大神がこもって世界を閉ざした天岩戸(あまのいわと)から。

  ame-iwato        ロックし、正しいパスワードが入るまで戻らない
  ame-iwato -f     ロックできたら裏に回り、すぐ戻る(放置で自動ロックする道具から呼ぶとき)

ame-shell の中のロック画面(顔認証・曲のカードつき)とは別の、どのコンポジタでも動く単体のもの。
ame-shell が落ちてロックが残ったときに外す道具にもなる(別の端末から WAYLAND_DISPLAY を合わせて実行)。
画面: 雨の夜の色の上に、入力の輪(打った数だけ点・確かめ中は橙・違ったら赤)。文字は使わない。
照合: PAM(サービス ame-shell、無ければ swaylock)を子プロセスで。FreeBSD は root の setuid の ame-auth に頼む。
終了コード: 0 外した / 1 ロックできない(コンポジタが対応していない・ほかのロックが動いている・照合の準備ができない)
```

## ビルド

```sh
zig build -Doptimize=ReleaseSafe   # zig-out/bin/ame-iwato(Zig 0.13、libc・wayland-client・xkbcommon・wayland-scanner)
zig build test
```

実行に要るもの: `libpam`

## このリポジトリについて

正本は ame-shell の `src/cmd/ame-iwato.zig` です。このリポジトリは `scripts/split-repos.sh` が生成して同期しています。
直したいところがあれば ame-shell の方へお願いします。

ライセンス: GPL-3.0(ame-shell と同じ)
