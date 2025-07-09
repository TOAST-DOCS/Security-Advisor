## Security > Security Advisor > APIガイド
Security Advisor Public APIを説明します。
## 共通準備事項
APIを使用するには、APIエンドポイントとトークンが必要です。

### APIエンドポイント
| リージョン | エンドポイント |
| --- | ----- |
| 全てのリージョン | [https://advisor.api.nhncloudservice.com](https://advisor.api.nhncloudservice.com/) |

### 認証トークン発行
Seucirty AdvisorはAPI認証/認可を受けるためにNHN Cloudトークンを使用します。
[NHN Cloud API呼び出し及び認証](https://docs.nhncloud.com/ko/nhncloud/ko/public-api/api-authentication/)を確認し、認証トークン使用に必要な情報を確認してください。
## API使用共通情報

### APIリクエスト共通情報

APIを使用するには、以下の情報が必要です。

* トークン発行後、APIヘッダにトークン情報を含めます。

| 名前 | 種類 | 形式 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| x-nhn-authorization | Header | String | O | トークン |
* サービスAppkey
    * Security Advisorコンソールの右上にある **URL & Appkey** メニューまたはプロジェクト管理の **利用中のサービス** で確認できます。
    * サービスURL PathにAppkeyが含まれます。

### APIレスポンス共通情報

* APIリクエストに対するレスポンスとして、以下のレスポンスコードを返すことができます。
    * 200 OK
    * 400 Bad Reuqest
    * 404 Not Found
    * 405 Method Not Allowed
    * 500 Internal Server Error
* 全てのレスポンスコードは共通のResponse bodyを含みます。
    * 共通Response body

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| header | Object |  |
| header.isSuccessful | Boolean | true:正常<br>false:エラー |
| header.resultCode | Integer | 1:正常<br>その他:エラー |
| header.resultMessage | String | "SUCCESS":正常<br>その他:エラー原因メッセージ |

* <span style="color:rgb(49, 51, 56);">共通Response body以外の詳細なレスポンス結果はレスポンス本文ヘッダを参照します。</span>

> [注意] APIレスポンスガイドに明示されていないフィールドが表示される場合があります。これらのフィールドはNHN Cloud内部用であり、事前の通知なしに変更される可能性があるため、使用しないでください。
## Security Advisor

### 最終点検日照会

最終点検日を照会します。

```
GET "/advisor/v1.0/appKey/{appKey}/last_inspection_date"
```
##### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | サービスAppkey |

##### レスポンス

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| latestInspectionTime | String | O | 最終点検日(datetime) |

<details>
  <summary>例</summary>
<p>

```json
{
    "header": {
        "resultCode": 1,
        "resultMessage": "Request success",
        "isSuccessful": true
    },
    "body": {
        "latestInspectionTime": "2025-03-11T16:00:32+09:00"
    }
}
```

<br>
</details>

### 自動点検設定照会

管理者が設定した自動点検設定値を照会します。

```
GET "/advisor/v1.0/appKey/{appKey}/setting"
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | サービスAppkey |

#### レスポンス

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| <span style="">emails</span> | <span style="">Array</span> | O | <span style="">点検完了時に完了メールを</span><br><span style="">受信するメールアドレスのリスト</span> |
| <span style="">isEnableAutoInspect</span> | <span style="">Boolean</span> | O | <span style="">自動点検設定の有無</span><br><span style="">(該当値がfalseの場合、残りの設定を無視)</span> |
| <span style="">inspectionList</span> | <span style="">Array</span> | X | <span style="">自動点検進行時に選択した項目</span> |
| <span style="">inspectionCycle</span> | <span style="">Object</span> | X | <span style="">点検周期設定</span> |
| <span style="">inspectionCycle.isWeek</span> | <span style="">Boolean</span> | X | <span style="">週単位での選択の有無</span> |
| <span style="">inspectionCycle.time</span> | <span style="">String(hh:mm)</span> | X | <span style="">点検進行時間(00:00)</span> |
| <span style="">inspectionCycle.day</span> | <span style="">Integer</span> | X | <span style="">点検進行曜日(日曜日が1から開始)</span> |
| <span style="">isWhole</span> | <span style="">Boolean</span> | X | <span style="">全体点検の選択有無</span> |

<details>
  <summary>例</summary>
<p>

```json
{
    "header": {
        "resultCode": 1,
        "resultMessage": "Request success",
        "isSuccessful": true
    },
    "body": {
        "emails": ["nhncloud@nhn.com"],
        "isEnableAutoInspect": true,
        "inspectionList": [
            1,
            2,
            3,
            4,
            5,
            6,
            7,
            8,
9
        ],
        "inspectionCycle": {
            "isWeek": true,
            "time": "00:00",
            "day": 2
        },
        "isWhole": false
    }
}
```

<br>
</details>

### 最後の点検結果要約照会

最後の点検結果に対する要約情報を照会します。

```
GET "/advisor/v1.0/appKey/{appKey}/inspection_results?region={region}&lang={lang}&page={page}&size={size}"
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | サービスAppkey |
| region | Query | String | O | リージョンコード(KR1:パンギョ、 KR2:ピョンチョン、<br>JP1:日本、 US1:米国) |
| lang | Query | String | O | 言語コード(KO:ハングル、 EN:英語、 JA:日本語) |

#### レスポンス

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| ruleNo | Integer | O | 点検項目番号 |
| status | String | O | 点検結果(critical:危険, warning:注意、 interest:関心, good:良好) |
| inspectRange | String | O | 点検対象範囲(PROJECT:プロジェクト、 ORG:組織) |
| inspectContent | String | O | 点検対象タイトル |
| detectionCount | Integer | O | 検出数 |
| exceptionCount | Integer | O | 例外数 |
| inspectTime | String | O | 点検時間(datetime) |

<details>
  <summary>例</summary>
<p>

```json
{
    "header": {
        "resultCode": 1,
        "resultMessage": "Request success",
        "isSuccessful": true
    },
    "body": [
        {
            "ruleNo": 10,
            "status": "good",
            "inspectRange": "PROJECT",
            "inspectContent": "Security Groups点検",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2023-06-12T19:53:35+09:00"
        },
        {
            "ruleNo": 11,
            "status": "good",
            "inspectRange": "PROJECT",
            "inspectContent": "Database Security Groups点検",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2023-06-12T19:53:35+09:00"
        },
        {
            "ruleNo": 1,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAMログイン失敗セキュリティ診断",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:42+09:00"
        },
        {
            "ruleNo": 2,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAMログインセッション時間点検",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:42+09:00"
        },
        {
            "ruleNo": 3,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAMログインセッション数点検",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:42+09:00"
        },
        {
            "ruleNo": 4,
            "status": "good",
            "inspectRange": "ORG",
            "inspectContent": "プロジェクトメンバーの未使用IAMアカウント点検",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 5,
            "status": "good",
            "inspectRange": "ORG",
            "inspectContent": "プロジェクトのIAMアカウント使用状況を点検",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 6,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "プロジェクトメンバー会員アカウントの二要素認証設定を点検",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 7,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "プロジェクトメンバーIAMアカウントの二要素認証設定を点検",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 8,
            "status": "good",
            "inspectRange": "ORG",
            "inspectContent": "IAMコンソールドメイン設定を点検",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 9,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAMコンソールのIP ACL設定を点検",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 12,
            "inspectRange": "PROJECT",
            "inspectContent": "RDSアクセス制御を点検",
            "detectionCount": 0,
            "exceptionCount": 0
        },
        {
            "ruleNo": 13,
            "inspectRange": "PROJECT",
            "inspectContent": "NCRイメージ脆弱性点検設定を点検",
            "detectionCount": 0,
            "exceptionCount": 0
        }
    ]
}
```

</details>
