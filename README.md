# Choreia 人財

職業紹介・人材派遣（M2Labo 人財部）の取引先／案件／候補者／マッチング管理。

**本番:** https://choreia.github.io/Jinzai/

## 構成
[Choreia Flow](https://github.com/Choreia/Flow) と同一アーキテクチャ。

| 要素 | 技術 |
|------|------|
| フロントエンド | 単一 HTML SPA（ビルド不要） |
| 認証 | Google OAuth 2.0（組織ドメイン限定・フリーメール排除） |
| データ保存 | Google Sheets API v4（初回セットアップで自動作成） |
| 面接 | Google Calendar API（Meet自動発行・sendUpdates=all） |
| 面接要約 | Gemini「メモを作成」のドキュメントをカレンダー添付から自動取り込み |
| ホスティング | GitHub Pages |

## シート構成（初回セットアップで自動作成）
取引先 / 案件 / 候補者 / 選考 / 書類 / 機微 の6シート。
ID体系: CL- / JOB- / CAN- / APP- / DOC-（「人材ビジネス案件管理案」2026-08-05 準拠）。

## 機微情報
- パスポート番号・面談評価は「機微」シートに分離。config の `sensitiveViewers` に載っているメールのみ画面表示・編集可
- **マイナンバーは扱わない設計**（入力欄なし）

## Gemini面接メモの自動取り込み
面接イベント終了後、カレンダーイベントの添付から Gemini 生成ドキュメント（タイトルに Gemini/メモ/Notes）を探し、text/plain でエクスポートして選考レコードに保存。会議で「メモを作成」をONにしておくこと（Workspace の Gemini 機能が必要）。

## 設定ファイル
`choreia-jinzai-config.json`（選択した共有ドライブフォルダに保存）: domain / admins / sensitiveViewers / spreadsheetId
