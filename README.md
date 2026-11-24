# ちょこまな みまもり

GitHub・Streamlit Cloud・既存のちょこまな用Supabaseで使うセットです。保護者と子どものアプリは、既存の学習者IDと学習記録を共用します。

## 反映手順

1. **SupabaseのSQL Editor**で `mimamori.sql` を実行します。
2. **SupabaseのEdge Functions**で既存の `chokomana-watch` を開き、エントリーファイル `index.ts` を同梱の `index.ts` の内容で置き換えてデプロイします。アプリ独自のセッション認証を使うため、既存の `verify_jwt = false` を維持します。
3. 保護者用のGitHubリポジトリに `app.py_mimamori.py` と `requirements.txt` を置きます。Streamlit Cloudでこのリポジトリを選び、起動ファイルを `app.py_mimamori.py` に指定します。既存のちょこまなID・パスワードと保護者用PINで使えます。管理アプリは既存のSupabase URLを内蔵しており、管理アプリのSecretsにサービスキーを追加する必要はありません。
4. 集約アプリにも反映する場合は、同梱の `app.py_hub.py` を使います。このファイルは最新版 `app.py_hub(4).py` と同じ内容です。すでに同じ版を使っていれば、集約アプリの差し替えは不要です。既存のSecretsは引き継ぎ、保護者画面へのリンクを出す場合は `MIMAMORI_APP_URL = "https://保護者アプリ名.streamlit.app"` を追加します。

集約アプリの個人別・年代別の誤答分析を新たに使う場合は、その機能用の `chokomana_answer_analysis.sql` を別途反映します。

## 確認する操作

- 保護者用アプリで教科配分、分類の「学習しない」、単元の重点設定を保存し、集約アプリで「きょうやること」を更新します。
- 子ども側の「今日の成果」から「これ、みて！」を送り、保護者側の「きょうの学習」で確認して、スタンプか声で返信します。金メダルは「アピールする」ボタンからも送れます。
- Streamlit版は、管理アプリの画面を閉じている間のスマホへのプッシュ通知には対応していません。
