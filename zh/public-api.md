## Security > Security Advisor > API Guide
The guide describes Security Advisor Public API.
## Common Preparations
To use the APIs, you need an API endpoint and a token.

### API Endpoints
| Region | Endpoint |
| --- | ----- |
| All regions | [https://security-advisor.api.nhncloudservice.com](https://security-advisor.api.nhncloudservice.com) |

### Obtain the Authentication Token
Security Advisor uses the NHN Cloud token for API authentication and authorization.
Refer to [NHN Cloud API Call and Authentication](https://docs.nhncloud.com/en/nhncloud/en/public-api/api-authentication/) for the necessary information on using the authentication token.

## API Common Information

### API Common Request Information

To use the API, the following information is required.

* After issuing the token, include the token information in the API request headers.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| x-nhn-authorization | Header | String | O | Token |

* Service Appkey
    * You can check the service Appkey from the **URL & Appkey** menu at the top right of the Security Advisor console or from **Services in Use** under Project Management.
    * The Appkey is included in the service URL path.

### API Common Response Information

* The following response codes may be returned as a result of an API request.
    * 200 OK
    * 400 Bad Reuqest
    * 404 Not Found
    * 405 Method Not Allowed
    * 500 Internal Server Error
* All response codes include a common response body.
    * Common Response body

| Name | Type | Description |
| --- | --- | --- |
| header | Object |  |
| header.isSuccessful | Boolean | true: normal<br>false: error |
| header.resultCode | Integer | 1: normal<br>others: error |
| header.resultMessage | String | "SUCCESS": normal<br>others: error cause message |

* <span style="color:rgb(49, 51, 56);">For details beyond the common response body, see Response Body Header.</span>

> [Caution] API response may show the fields not specified by the guide. These fields are internally used by NHN Cloud, and not used because they are subject to change without prior notice.
## Security Advisor

### Query Last Inspection Date

Retrieves last inspection date.

```
GET "/advisor/v1.0/appKey/{appKey}/last_inspection_date"
```
##### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |

##### Response

| Name | Format  | Required | Description |
| --- | --- | --- | --- |
| latestInspectionTime | String | O | Last inspection date (datetime) |

<details>
  <summary>Example</summary>
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

### Query Auto Inspection Settings

Retrieves the auto inspection settings configured by the administrator.

```
GET "/advisor/v1.0/appKey/{appKey}/setting"
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |

#### Response

| Name | Format | Required | Description |
| --- | --- | --- | --- |
| <span style="">emails</span> | <span style="">Array</span> | O | <span style="">Email addresses to receive notification</span><br><span style="">upon completion of inspection</span> |
| <span style="">isEnableAutoInspect</span> | <span style="">Boolean</span> | O | <span style="">Whether to set auto inspection</span><br><span style="">(If this value is false, all other settings are ignored)</span> |
| <span style="">inspectionList</span> | <span style="">Array</span> | X | <span style="">Selected items for auto inspection</span> |
| <span style="">inspectionCycle</span> | <span style="">Object</span> | X | <span style="">Inspection cycle settings</span> |
| <span style="">inspectionCycle.isWeek</span> | <span style="">Boolean</span> | X | <span style="">Whether weekly selection is enabled</span> |
| <span style="">inspectionCycle.time</span> | <span style="">String(hh:mm)</span> | X | <span style="">Inspection execution time (00:00)</span> |
| <span style="">inspectionCycle.day</span> | <span style="">Integer</span> | X | <span style="">Days of the week for inspection execution (Sunday is represented as 1)</span> |
| <span style="">isWhole</span> | <span style="">Boolean</span> | X | <span style="">Whether full inspection is selected</span> |

<details>
  <summary>Example</summary>
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

### Query Summary of Last Inspection Result

Retrieves summary information of the most recent inspection result.

```
GET "/advisor/v1.0/appKey/{appKey}/inspection_results?region={region}&lang={lang}&page={page}&size={size}"
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | URL | String | O | Service Appkey |
| region | Query | String | O | Region code (KR1: Pangyo, KR2: Pyeongchon,<br>JP1: Japan, US1: United States) |
| lang | Query | String | O | Language code (KO: Korean, EN: English, JA: Japanese) |

#### Response

| Name | Format | Required | Description |
| --- | --- | --- | --- |
| ruleNo | Integer | O | Inspection item number |
| status | String | O | Inspection result (critical: high risk, warning: caution advised, interest: needs attention, good: no issues) |
| inspectRange | String | O | Inspection target range (PROJECT: projects, ORG: organizations) |
| inspectContent | String | O | Inspection target content |
| detectionCount | Integer | O | Number of detections |
| exceptionCount | Integer | O | Number of exceptions |
| inspectTime | String | O | Inspection time (datetime) |

<details>
  <summary>Example</summary>
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
            "inspectContent": "Security Groups Inspection",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2023-06-12T19:53:35+09:00"
        },
        {
            "ruleNo": 11,
            "status": "good",
            "inspectRange": "PROJECT",
            "inspectContent": "Database Security Groups Inspection",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2023-06-12T19:53:35+09:00"
        },
        {
            "ruleNo": 1,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAM Login Failure Security Inspection",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:42+09:00"
        },
        {
            "ruleNo": 2,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAM Sign-in Session Inspection",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:42+09:00"
        },
        {
            "ruleNo": 3,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAM Sign-in Session Count Inspection",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:42+09:00"
        },
        {
            "ruleNo": 4,
            "status": "good",
            "inspectRange": "ORG",
            "inspectContent": "Inactive IAM Accounts of Project Members Inspection",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 5,
            "status": "good",
            "inspectRange": "ORG",
            "inspectContent": "IAM Account Usage Status in Project Inspection",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 6,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "2FA Setting Inspection for Project Members’ NHN Cloud Accounts",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 7,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "2FA Setting Inspection for Project Members’ IAM Accounts",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 8,
            "status": "good",
            "inspectRange": "ORG",
            "inspectContent": "IAM Console Domain Setting Inspection",
            "detectionCount": 0,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 9,
            "status": "critical",
            "inspectRange": "ORG",
            "inspectContent": "IAM Console IP ACL Setting Inspection",
            "detectionCount": 1,
            "exceptionCount": 0,
            "inspectTime": "2025-03-11T16:00:43+09:00"
        },
        {
            "ruleNo": 12,
            "inspectRange": "PROJECT",
            "inspectContent": "RDS Access Control Inspection",
            "detectionCount": 0,
            "exceptionCount": 0
        },
        {
            "ruleNo": 13,
            "inspectRange": "PROJECT",
            "inspectContent": "NCR Image Vulnerability Scan Setting Inspection",
            "detectionCount": 0,
            "exceptionCount": 0
        }
    ]
}
```

</details>
