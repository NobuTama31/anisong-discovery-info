# AnisongDiscovery

しょぼいカレンダーの公開APIを利用する、開発中の個人向けローカルツールです。
アニメ作品と楽曲の掲載情報を整理し、所有音源と照合して、CDレンタル・購入で探したい楽曲の候補を見つけることを目的としています。

## アプリの識別

- アプリ名：AnisongDiscovery
- バージョン：0.1
- 運用者：[@NobuTama31](https://github.com/NobuTama31)
- 案内ページ：https://github.com/NobuTama31/anisong-discovery-info
- User-Agent：`AnisongDiscovery/0.1 (+https://github.com/NobuTama31/anisong-discovery-info)`

## データ取得について

取得先は、しょぼいカレンダーの公式API `https://cal.syoboi.jp/db.php` です。
`TitleLookup` を使用し、作品ID・作品名・開始年・カテゴリ・更新日時・Comment内の楽曲掲載情報を取得します。
現在の対象年代は作品の開始年が2007〜2026年のものです。進行中の年については取得時点で登録されている情報が対象です。

- リクエストは直列に実行し、応答後の取得間隔は初期設定で60秒です。
- 作品詳細は1回につき最大100 IDにまとめます。
- 全作品のメタデータを確認した後、対象年代・カテゴリに該当する作品の楽曲情報を取得します。
- 取得結果をローカルに保存して再利用し、HTTPのキャッシュ指定を尊重します。
- 更新確認には `LastUpdate` による差分取得を利用します。
- HTTP 429では `Retry-After` に従い、一時的な障害では待ち時間を増やして最大3回まで試行します。
- 取得失敗時は、保存済みの正常なデータを維持します。
- しょぼいカレンダーの作品HTMLのスクレイピングは行いません。

利用にあたっては、[しょぼいカレンダーのbot利用方針](https://docs.cal.syoboi.jp/rule/bot/)と[API仕様](https://docs.cal.syoboi.jp/spec/db.php/)を確認します。
このツールはしょぼいカレンダーの公式サービスではありません。

## 連絡方法

本ツールのアクセス、動作、不具合などについては、このリポジトリの[Issuesから運用者へご連絡ください](https://github.com/NobuTama31/anisong-discovery-info/issues/new)。GitHubアカウントで投稿できます。

このリポジトリはアプリの識別と連絡窓口のための案内です。音源、所有曲一覧、収集したデータベースは公開していません。
