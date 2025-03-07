---
sourcePath: en/tracker/api-ref/get-board.md
---
# Get board parameters

Use this request to get the parameters of an issue board.

## Request format {#section_zvs_yjc_4fb}

To get the parameters of all issue boards, use an HTTP `GET` request:

```json
GET /{{ ver }}/boards/<board-id>
Host: {{ host }}
Authorization: OAuth <token>
X-Org-ID: <organization ID>
```

#### Resource {#req-resource}

- **\<board-id\>**

    Board ID.

#### Headers {#req-headers}

- **Host**

    Address of the node that provides the API:

    ```
    {{ host }}
    ```

- **Authorization**

    OAuth token in `OAuth <token value>` format. For example:

    ```
    OAuth 0c4181a7c2cf4521964a72ff57a34a07
    ```

- **X-Org-ID**

    Organization ID.

## Response format {#section_a21_q4c_4fb}

{% list tabs %}

- Request executed successfully

    If the request is successful, the API returns a response with code 200. The response body contains a JSON object with board parameters.

    #### Response body {#answer-body}

    ```json
    {
      "self" : "http://api.tracker.yandex.net/v2/boards/1",
      "id" : 1,
      "version" : 1412806202302,
      "name" : "Testing", 
      "columns" : 
      [ 
       {
        "self" : "http://api.tracker.yandex.net/v2/boards/1/columns/1387461731452",
        "id" : "1387461731452",
        "display" : "Open"
       },
       ...
      ],
       "filter": {
          "<key of parameter 1>": "<value 1>",
          "<key of parameter 2>": [
              "<value 2>", 
                            ...
           ],
            ...
        },
       "orderBy": "updated",
       "orderAsc": false,
       "query": "<Parameter 1>: <Value 1> AND <Parameter 2>: <Value 2> OR <Parameter 3>: <Value 3>...",
       "useRanking": false,
       "estimateBy": {
          "self": "https://api.tracker.yandex.net/v2/fields/storyPoints",
          "id": "storyPoints",
          "display": "Story Points"
        }, 
       "country": {
          "self": "https://api.tracker.yandex.net/v2/countries/1",
          "id": "1",
          "display": "Russia"
        },
       "defaultQueue": {
          "self": "https://api.tracker.yandex.net/v2/queues/DOC",
          "id": "3",
          "key": "DOC",
          "display": "Documenting"
        },
        "calendar": {
           "id": 6
          }     
       }
    ```

    #### Response parameters {#answer-params}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with board parameters. | String |
    | id | Board ID. | Number |
    | version | Board version. Each change to the board increases its version number. | Number |
    | name | Board name. | String |
    | [columns](#columns) | Object with information about board columns. | Object |
    | [filter](#filter) | Object with information about filter conditions used for selecting issues for the board.<br/>Issue parameters are made up of fields and values. | Object |
    | orderBy | Field key.<br/>The field is used as a parameter for sorting board issues.<br/>Full list of fields: [{{ link-admin-fields }}]({{ link-admin-fields }}) | String |
    | orderAsc | Field value sorting order:<ul><li>`true`: Ascending.</li><li>`false`: Descending.</li></ul> | Boolean |
    | query | Parameters of the filter used to select issues for the board.<br/>The parameters are specified in the [query language](user/query-filter.md). | String |
    | useRanking | Shows if you can change the order of issues on the board:<ul><li>`true`: Yes.</li><li>`false`: No.</li></ul> | Boolean |
    | [estimateBy](#estimateBy) | Object with information about what parameter is used to evaluate issues on the board. <br/>By default, the `Story Points` parameter is used. | Object |
    | [country](#country) | Object with information about the country. Data of a country's business calendar is used in the [Burn down chart](manager/burndown.md).<br/>To get a list of countries, use the HTTP request `GET /v2/countries` | Object |
    | [defaultQueue](#defaultQueue) | Object with information about the queue where issues are created by default. | Object |
    | [calendar](#calendar) | Object with information about the business calendar used for this board. This calendar is used to calculate work days and days off in the [Burn down chart](manager/burndown.md). | Number |

    **Object fields** `columns` {#columns}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with information about the board column. | String |
    | id | Column ID. | String |
    | display | Column name displayed. | String |

    **Object fields** `filter` {#filter}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | \<key of parameter 1\> | Key of the field that is used as a parameter for selecting issues for the board.<br/>Full list of fields: [{{ link-admin-fields }}]({{ link-admin-fields }}) | String |
    | \<key of parameter 2\> | Array with the keys of the fields that are used as parameters for selecting issues for the board.<br/>Full list of fields: [{{ link-admin-fields }}]({{ link-admin-fields }}) | Array |

    **Object fields** `estimateBy` {#estimateBy}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with information about the issue evaluation parameter. | String |
    | id | ID of the issue evaluation parameter. | String |
    | display | Displayed name of the issue evaluation parameter. | String |

    **Object fields** `country` {#country}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with the country name. | String |
    | id | Country ID. | String |
    | display | Country name displayed. | String |

    **Object fields** `defaultQueue` {#defaultQueue}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with information about the queue. | String |
    | id | Queue ID. | String |
    | key | Queue key. | String |
    | display | Queue name displayed. | String |

    **Object fields** `calendar` {#calendar}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | id | Calendar ID. | Number |

- Request failed

    If the request is processed incorrectly, the API returns a message with error details:

    | HTTP error code | Error description |
    | --------------- | --------------- |
    | 400 Bad Request | One of the request parameters has an invalid value or data format. |
    | 403 Forbidden | The user or application has no access rights to the resource, the request is rejected. |
    | 404 Not Found | The requested resource not found. |
    | 500 Internal Server Error | Internal service error. Try again later. |
    | 503 Service Unavailable | The API service is temporarily unavailable. |

{% endlist %}

