## Description

This API is used to create a shipping task. When using this API, you need to manually grant CLS the permission to write to the specified bucket.

## Request
### Request example

```
POST /shipper HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "bucket": "test-1250000001",
  "prefix": "test",
  "shipper_name": "myname",
  "interval": 300,
  "max_size": 256,
  "partition": "%Y%m%d",
  "compress": {
    "format": "none"
  },
  "content": {
    "format": "csv",
    "csv_info": {
      "print_key": true,
      "keys": ["key1", "key2"],
      "delimiter": "|",
      "escape_char": "'",
      "non_existing_field": "null"
    }
  },
  "filter_rules": [{
    "key": "",
    "regex": "",
    "value": ""
  }]
}
```

### Request line

```
POST /shipper
```

### Request header

No special request header is used except for the common header.

### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| topic_id | string | body | Yes | ID of the topic to which the shipping task to be created belongs |
| bucket | string | body | Yes | Shipping bucket of the shipping task to be created. Format: {bucketName}-{appid} |
| prefix | string | body | Yes | Prefix of the shipping directory of the shipping task to be created |
| shipper_name | string | body | Yes | Shipping rule name |
| interval | int | body | No | Shipping interval (in sec). Default is 300. Value range: 60-3600 |
| max_size | int | body | No | The maximum size of a file to be shipped (in MB). Default is 256 MB. Value range: 100-10240 |
| custom_uin | long | body | No | UIN of the customer to which the shipping task to be created belongs, which is retained since it is compatible with the old API. |
| filter_rules | array | body | No | Rules for filtering logs to be shipped. Logs that match the rules are shipped. The relation between rules is `and`. The number of rules is limited to 5. If the array is left empty, all logs are shipped without filtering. |
| partition | string | body | No | Rules for partitioning logs to be shipped. `Strftime` can be used to define the time format. |
| compress | object | body | No | Compression configuration of logs to be shipped |
| content | object | body | No | Format configuration of logs to be shipped |

Rule is composed as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | ---- | ----------------------------------------------------- |
| key | string | Yes | The key used for comparison. `__CONTENT__` means full text. |
| regex | string | Yes | The regular expression used to extract the comparison content |
| value | string | Yes | The value used to compare with the content extracted by using the above regex. The rule is hit if they are consistent. |

compress is composed as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | ---- | ------------------------------------------ |
| format | string | Yes | Compression format, including `gzip`, `lzop` and `none` (do not compress). |

content is composed as follows:

| Field Name | Type | Required | Description |
| -------- | ------ | -------- | --------------------------- |
| format | string | Yes | Content format, which supports `json` and `csv`. |
| csv_info | object | No | Required when the content format is `csv` |

csv_info is composed as follows:

| Field Name | Type | Required | Description |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key | bool | Yes | Indicates whether to write the first line of key to the csv file |
| keys | array(string) | Yes | Key name of each column |
| delimiter | string | Yes | The separator between fields |
| escape_char | string | Yes | Escape characters are used to enclose the separators contained in a field. |
| non_existing_field | string | Yes | It is used to populate the fields specified above that do not exist or are invalid. |


## Response
### Response example

```
 HTTP/1.1 200 OK
 Content-Type: application/json
 Content-Length: 0
 {
   "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
 }
```

### Response header

No special response header is used except for the common response header.

### Response parameters

| Field Name | Type | Required | Description |
| ---------- | ------ | ---- | ----------------- |
| shipper_id | string | Yes | ID of the new shipping task |

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

