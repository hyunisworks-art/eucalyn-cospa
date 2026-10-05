# Eucalyn Cost-Performance Layout (Eucalyn配列コスパモデル)

**English:** A Japanese romaji–oriented logical keyboard layout derived from [Eucalyn](https://eucalyn.hatenadiary.jp/entry/about-eucalyn-layout). It keeps more QWERTY key positions than the base Eucalyn layout (about 42% letter match) while still improving home-row usage for Japanese typing. Includes a browser-based trainer (`index.html`) and layout JSON for tooling.

**日本語:** Eucalyn 配列をベースに、移行コストとショートカットの使いやすさを重視した論理配列です。詳しい背景は [note 記事](https://note.com/hyu_nisworks/n/n98e034b02379) を参照してください。

- **Web 版（練習サイト）:** https://eucalyn-cust-performance-mudel.netlify.app/

## 配列図（アルファベット段）

QWERTY 配列のキー位置（物理位置）に対して、次の文字が割り当てられます。

```
段1: q w e , . f d r y p
段2: a i u o - g t k s n
段3: z x c v b m h j l /
```

ホームポジション（段2）: `a i u o -` / `g t k s n`

## 特徴

- **左手に母音を集約:** 左手中指に `u` と `e` を置き、5 母音を横一列に並べない凸型に調整しています（`a` / `i` / `u` / `o` は Eucalyn と同系の配置感）。
- **Neovim / Vim の HJKL:** 右下の逆 T 字（`h` `j` `k` `l`）は Eucalyn と同じ考え方を維持。
- **QWERTY との一致を増やす:** アルファベット 26 キーのうち 11 キーが QWERTY と同位置（約 42%）。`q` `w` や保存・終了で使う `w` `q` など、ショートカットで触るキーを残しやすくしています。
- **効率は控えめ:** 最高効率より、移行後の違和感とショートカット互換を優先した「コスパ」設計です。

## ほかの Eucalyn 系との違い（概要）

| 観点 | Eucalyn（原版） | Eucalyn改配列 | **コスパモデル（本リポ）** |
| --- | --- | --- | --- |
| 目的 | Vim 配慮 + バランス | 原版より効率を押し上げ | 移行コストとショートカット互換 |
| QWERTY 一致（目安） | 約 34%（9/26） | 原版から再配置 | **約 42%（11/26）** |
| 母音（左手） | 5 母音が横並び | 改版方針に沿った配置 | 凸型（`u`/`e` を中指など） |
| 右上 `d`/`r` | 配置が逆 | 改版固有 | **`r` を中指側に**（打鍵頻度を考慮） |

配列の比較用に、同梱の 30 文字スロット定義では次のように読み替わります（QWERTY スロット名 → 本配列の文字）:

- Eucalyn 原版から主な変更: 段1の `,` 位置 → `e`、`.` → `,`、`m`/`r`/`d` → `f`/`d`/`r` など
- 詳細は `layout/eucalyn-cospa-typing.json` を参照

## 導入方法

論理配列は OS やキー remapper で「押したキー → 出力文字」を設定します。手順は環境ごとに異なるため、ここでは方針のみ記載します。

1. **まず Web 版で練習する**（日本語 IME は OFF、英字入力で練習）
2. **配列定義を参照して remapper を設定する**
   - 30 文字スロット形式: [`layout/eucalyn-cospa-typing.json`](layout/eucalyn-cospa-typing.json)
   - Keybr 互換のフルキー定義: [`layout/eucalyn-cospa-keybr.json`](layout/eucalyn-cospa-keybr.json)
3. **macOS:** [Karabiner-Elements](https://karabiner-elements.pqrs.org/) などで simple modifications を設定
4. **Windows:** [PowerToys Keyboard Manager](https://learn.microsoft.com/en-us/windows/powertoys/keyboard-manager) や AutoHotkey など

QWERTY に戻せば、従来どおり QWERTY で入力できます（両方の配列を使い分ける利用者もいます）。

## Eucalyn Trainer（同梱）

このリポジトリの `index.html` は、コスパモデルへ移行するための **パソコン専用** タイピング練習サイトです（単体 HTML、ビルド不要）。

### 使い方

1. 日本語入力を OFF にする。
2. 必要なら右上で Windows／Mac 表示を選ぶ。
3. スペースキーで選択中の課題を始めるか、「今日の5分」を選ぶ。
4. 「進捗」で弱点、自己ベスト、次の小目標を確認する。

コースは手動でも選べます。おすすめ段階は、入力履歴に応じて「キー探索 → 短いワード → 例文 → 実務練習」と進みます。

### 最低限の実務入力の目安

- 15 WPM 以上
- 正確率 95% 以上
- 上記を例文・実務練習の 5 分セッションで 3 回記録

合否ではなく、実務文へ進むための目安です。

### 進捗データ

入力履歴とセッション結果はブラウザ内に保存します。「進捗」から JSON でバックアップ・復元・全削除ができます。サーバーへは送信しません。

### 対応環境

- パソコン専用（画面幅 1024px 以上）
- Windows／Mac
- Chromium 系ブラウザで検証済み

### ローカルで開く

```bash
python -m http.server 4173 --bind 127.0.0.1
```

- 練習: http://127.0.0.1:4173/
- 自動テスト: http://127.0.0.1:4173/tests/test-runner.html

## テスト

[`tests/test-runner.html`](tests/test-runner.html) が `index.html` を iframe で読み込み、UI とキー入力を検証します。手順は [`tests/README.md`](tests/README.md)、過去の実行記録は [`tests/TEST_RESULTS.md`](tests/TEST_RESULTS.md) を参照してください。

## 引用・紹介

配列を紹介する場合は、[note 記事](https://note.com/hyu_nisworks/n/n98e034b02379) へのリンクを付けてください（配列作者の希望に基づく）。

## 関連リンク

- [Eucalyn 配列（ゆかりメモ）](https://eucalyn.hatenadiary.jp/entry/about-eucalyn-layout)
- [Eucalyn 改配列（biacco42）](https://biacco42.hatenablog.com/entry/2018/12/16/235959)
