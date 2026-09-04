# Reforming the Japanese Ruby reference manual

author
:   Kazuhiro NISHIYAMA

institution
:   株式会社Ruby開発

date
:   2026-09-05

allotted-time
:   5m

theme
:   lightning-simple

# self.introduction

- 西山 和広
- github など: `@znz`
- Ruby のコミッター
- **https://github.com/rurema の管理者の一人**

# るりまリニューアル

- Claude Fable 5 が期間限定の間に一気に進展
  - 終わる終わるサギや何度もリミットがリセットされたおかげ
- 長年の課題だった Markdown 化が完了
- 関連作業も一気に進めた

# 執筆側

- doctree の書式が bitclust RD から Markdown へ
- 1250 ファイルを機械変換して 3 段階検証で一致
- GitHub のプレビューのため、できるだけ GFM 互換
  - `### def ...` や `#%since 3.1` 〜 `#%end` などは独自を維持
- モジュール関数は `Math.#atan2` から RBS に似せて `Math?.atan2` に変更
- 編集はページ下のリンクから .md の GitHub 編集画面へ
  - 誤字 1 文字から歓迎

# 読む側

- コードブロックが ruby.wasm で実行可能に
  - Ruby 3.2 以降、bundled gems 込み
- メソッドに対応バージョンのバッジ追加 (例: 「Ruby 3.2から」)
- RBS 型シグネチャをメソッド見出し下に表示 (Ruby 4.0 以降)
- bitclust 1.6.0 (7 月 29 日) と 1.7.0 (8 月 29 日) をリリース
  - refe2 も Markdown 版に対応
  - irb から引ける bitclust-irb を新設

# Reforming

- 各ページに検索ボックス追加
  - 検索はクライアントサイド (RDoc の Aliki の検索システムの派生)
- `/ja/search/` もるりまサーチから移行
  - 大量アクセスでほぼ使えなくなっていたのを改善
  - 旧版 1.8.7〜2.7.0 も検索対象に復活
- docs.ruby-lang.org 全体を S3 + Fastly の静的配信に移行
  - 旧 EC2 は terminate 済み
- llms.txt・sitemap 整備、各ページ (latest のみ) の Markdown 版を text/markdown で配信 (AI 向け)

# 中身も一斉整備

- doctree に積み上がっていた issues 181 件を全件棚卸し
  → 残り 6 件、いずれも方針検討中
- 組み込みクラスや標準ライブラリの棚卸し、実測して修正
- 執筆ルール明文化
  - 出力例は「`# =>`」、例外は「`# ~>`」に統一
  - リテラル優先: `Rational(1, 3)` より `1/3r`、`Regexp.new('\d+')` より `/\d+/`
  - 「自身」は `self` に統一
  - バージョンは「Ruby 3.0」と teeny 省略
  - 処理系は「CRuby」(「MRI」「C Ruby」は使わない)

# 謝辞

- 勤務先の**株式会社Ruby開発**が契約している Claude Max (Claude Fable 5) で 6〜9 月に集中作業
  - 変換器の実装、3 段階検証、bitclust の Markdown ネイティブ対応、本番切替、棚卸し、S3 移行まで
- 人間の役割は方針判断とレビュー、push・PR・AWS 操作
  - 説明の修正は複数バージョンで実測してから
- 業務ツールを OSS 活動にも使わせてくれる会社に感謝
- issue や PR の作成、レビューをしてくれたみなさんに感謝
  - 誤字 1 文字の修正から PR 歓迎
