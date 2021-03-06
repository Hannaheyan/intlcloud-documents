## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DescribeAutoScalingInstances) describes one or more Auto Scaling instances

* You can query the details of instances based on information such as instance ID and scaling group ID. For more information about filters, see `Filter`.
* If the parameter is empty, a number that same as the `Limit` (the default is 20) of scaling groups will be returned.

Default API request frequency limit: 10 times/second.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.




## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/30987).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeAutoScalingInstances |
| Version | Yes | String | Common parameter; the version this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/30987#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| InstanceIds.N | No | Array of String | ID of the CVM instance to be queried. The parameter does not support specifying both InstanceIds and Filters at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/31018#Filter) | Filter. <br/><li> instance-id - String - Required: No - (Filter) Filter by instance ID. </li><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by scaling group ID. </li><br/>The maximum number of `Filters` per request is 10. The upper limit for `Filter.Values` is 5. The parameter does not support specifying both `InstanceIds` and `Filters` at the same time. |
| Offset | No | Integer | Offset, 0 by default. For more information about `Offset`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |
| Limit | No | Integer | Number of returned results, 20 by default, up to 100. For more information about `Limit`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| AutoScalingInstanceSet | Array of [Instance](/document/api/377/31018#Instance) | List of instance details. |
| TotalCount | Integer | Number of eligible instances. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Querying a Specified Instance

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingInstances
&InstanceIds.0=ins-1fswxz1m
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "TotalCount": 1,
        "AutoScalingInstanceSet": [
            {
                "ProtectedFromScaleIn": false,
                "Zone": "ap-guangzhou-3",
                "LaunchConfigurationId": "asc-5fzsm72a",
                "InstanceId": "ins-1fswxz1m",
                "AddTime": "2018-08-21T12:05:12Z",
                "CreationType": "AUTO_CREATION",
                "AutoScalingGroupId": "asg-4o61gsxi",
                "HealthStatus": "HEALTHY",
                "LifeCycleState": "IN_SERVICE",
                "LaunchConfigurationName": "series 2 local disk",
                "InstanceType": "S2.SMALL2"
            }
        ],
        "RequestId": "2ae3e836-d47a-431c-b54b-4e1c2f419e5b"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingInstances)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/377/30990#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidFilter | Invalid filter. |
| InvalidParameter.Conflict | Parameters that cannot co-exist are specified at the same time. |
| InvalidParameterValue.Filter | Invalid filter. |
