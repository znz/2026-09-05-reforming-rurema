# Reforming the Japanese Ruby reference manual

author
:   Kazuhiro NISHIYAMA

institution
:   株式会社Ruby開発

date
:   2026-08-13

allotted-time
:   5m

theme
:   lightning-simple

# self.introduction

- 西山 和広
- github など: `@znz`
- Ruby のコミッター
- https://github.com/rurema の管理者の一人

# るりまリニューアル

- Fable が期間限定の間に一気に進展
- 長年の課題だった Markdown 化が完了
- 関連作業も一気に進めた

(https://rhc.connpass.com/event/392503/ RubyKaigi 2026 follow up で発表予定の内容です)

# 執筆側

- doctree の書式が bitclust RD から Markdown へ
  - AI は bitclust RD を `BitClust::RRDParser` という実装の名前から勝手に RRD と言おうとするが正式名称はない
- GitHub のプレビューのため、できるだけ GFM 互換
- `### def ...` や `#@since 3.1` 〜 `#@end` などは独自を維持
  - mention 誤爆回避のため `#%since 3.1` 〜 `#%end` に変更
- `[m:Array#each]` などのリンク (`[[m:Array#each]]` から変更)
- モジュール関数は `Math.#atan2` から RBS に似せて `Math?.atan2` に変更

# 読む側

- コードブロックが ruby.wasm で実行可能に
- メソッドに「Ruby 3.2から」のような対応バージョンのバッジ追加
- 各ページに検索ボックス追加
  - 検索はクライアントサイド (RDoc の Aliki の検索システムの派生)
  - `defined?`, `undef`, `alias` でも検索可能に
- `/ja/search/` もるりまサーチから移行
  - 大量アクセスでほぼ使えなくなっていたのを改善
  - ここが発表タイトルの Reforming

# 中身も一斉整備

- doctree に積み上がっていた issues 181件を全件棚卸し
  - 対応できるものをまとめて解消
  - 残りは方針検討中の数件
- 説明の誤りを実測して修正
- サンプルコードの書き方も明文化して改善
- 出力例は「`# =>`」、例外は「`# ~>`」に統一

# 移行手段

- Markdown から RD へのラウンドトリップ検証
- データベース検証: RD と Markdown それぞれから構築して比較
- HTML 検証: 新旧で生成して突合せ

# 謝辞

今回の移行(変換器の実装、検証、bitclust のネイティブ対応、本番切替まで)は、
勤務先の**株式会社Ruby開発**が契約してくれている Claude Max(Claude Fable 5)を
使って進めました。独自記法のパーサと格闘しながら 1250 ファイルの等価性を
検証し切るような作業がここまで短期間で完了したのは間違いなくこのおかげです。
業務ツールを OSS 活動にも使わせてくれている会社に感謝します。
