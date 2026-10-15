# 旅行検索と行程出力

リポジトリのルートで実行する。Python 3.10+ と Bash を用意し、各コマンドの `--help` で入力を確認する。

| コマンド | 用途 | 必要な設定 |
|---|---|---|
| `bash bin/flightx HND CTS 2027-07-01 --currency JPY --json` | 片道フライト検索 | SerpAPI の利用者キー `SERP_API_KEY` |
| `bash bin/hotel Kyoto --checkin 2027-07-01 --checkout 2027-07-03 --adults 2` | 宿検索 | 同上 |
| `bash bin/places search "京都 美術館"` | 場所検索 | Places API (New) を有効化した `GOOGLE_MAPS_API_KEY` |
| `bash bin/tz 35.681 139.767 --at 2027-07-01T03:00` | UTC 基準の時差確認 | Time Zone API を有効化した `GOOGLE_MAPS_API_KEY` |
| `bash bin/trip-map --in trip.json --out index.html` | 地図 HTML 作成 | Maps JavaScript API 用 `GOOGLE_MAPS_BROWSER_API_KEY` |
| `python3 bin/trip-kml --in trip.json --kml spots.kml --csv spots.csv` | KML/CSV 変換 | 不要 |

SerpAPI と Google Cloud のアカウント、必要な API と課金は利用者自身が設定する。サーバー用 Google キーは対象 API と実行元に制限する。ブラウザ専用キーは HTML に含まれるため、公開先の HTTP リファラーと Maps JavaScript API に制限し、サーバー用キーと共用しない。実キー入り HTML はこのリポジトリへコミットしない。

`trip.json` の例（実在の旅行履歴ではない）:

```json
{"title":"京都旅行","days":[{"label":"Day 1","points":[{"name":"京都駅","lat":34.9858,"lng":135.7588,"note":"集合"}]}]}
```

地図の線は地点間の直線。道路経路や所要時間を意味しない。HTML 生成には自分で確認した文字列だけを入力する。KML/CSV は利用者がマイマップへインポートするファイルであり、自動アップロードしない。

検索失敗・空結果を満席の確証と扱わない。価格は通貨と確認時刻を添え、税・手数料・キャンセル条件は予約先で確認する。外部 API のライブ動作はこの公開準備では未検証。
