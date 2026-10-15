# Gmail（任意）

利用者自身の Google Cloud プロジェクトで Gmail API とデスクトップ用 OAuth クライアントを設定する。組織の場合は管理者の許可を確認する。要求 scope は `gmail.send` と `gmail.readonly`。メール検索・本文読取・送信が可能なため、利用者が許可したメールだけを扱う。

秘密ストアから `GMAIL_OAUTH_CLIENT_ID` と `GMAIL_OAUTH_CLIENT_SECRET` を環境変数へ渡す。利用者自身のローカル端末で `bash bin/gmail auth` を実行してブラウザで認可する。ループバック接続を使用する。標準出力に refresh token が出るため、チャットや共有ログへ出さず秘密ストアへ保存し、`GMAIL_OAUTH_REFRESH_TOKEN` として設定する。

```bash
bash bin/gmail list --q "is:unread" --max 5
bash bin/gmail send --to recipient@example.com --subject "空室確認" --body "問い合わせ本文" --dry-run
```

送信前に宛先・件名・本文・CC/BCC を利用者へ提示し承認を得る。承認後だけ `--dry-run` を外す。返信は `reply <message-id> --body ... --dry-run` で確認する（返信の dry-run は元メールの読取のため API に接続する）。送信元は認可アカウントで、この CLI は送信エイリアスの指定に対応していない。

送信結果は利用者の非公開の作業記録へ残す。メール本文・宛先・トークンを公開リポジトリへ保存しない。認可と送信の実動作は公開準備では未検証。
