## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (ModifyLaunchConfigurationAttributes) modifies one or more attributes for the specified launch configuration.

* The changes of launch configuration do not affect the existing instances. New instances will be created based on the modified configuration.
* This API supports modifying certain simple types of launch configuration.

Default API request frequency limit: 20 times/second.

Note: Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/377/30987).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyLaunchConfigurationAttributes |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/30987#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| LaunchConfigurationId | Yes | String | Launch configuration ID |
| ImageId | No | String | Specify a valid [image](https://cloud.tencent.com/document/product/213/4940) ID in the format of `img-8toqc6s3`. There are four types of images: <br/><li>Public image </li><li>Custom image </li><li>Shared image </li><li>Service Market image </li><br/>The ID of an available image can be obtained in the following ways: <br/><li>Query the ID of a `public image`, `custom image`, or `shared image` in the [console](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE); query the ID of a `Service Market image` in the [Service Market](https://market.cloud.tencent.com/list). </li><li>Get the `ImageId` field in the return message after calling the [DescribeImages](https://cloud.tencent.com/document/api/213/15715) API. </li> |
| InstanceTypes.N | No | Array of String | List of instance types. Different instance models specify different resource specifications. Up to 5 instance models can be supported. <br/>Types of launch configurations. `InstanceType`: one single instance type; `InstanceTypes`: multiple instance types. After `InstanceTypes` is successfully specified for the launch configuration, the original `InstanceType` will be automatically invalidated. |
| InstanceTypesCheckPolicy | No | String | Instance type verification policy which works when InstanceTypes is actually modified; valid values: ALL, ANY; ANY by default. <br/><br><li> ALL: The verification will success only if all instance types (InstanceType) are available; otherwise, an error will be returned. <br/><br><li> ANY: The verification will success if any instance type (InstanceType) is available; otherwise, an error will be returned. <br/><br/>Common reasons why an instance type is unavailable include running out of the instance type or the corresponding cloud disk. <br/>If a model in InstanceTypes does not exist or has been discontinued, a verification error will be returned regardless of the value of InstanceTypesCheckPolicy. |
| LaunchConfigurationName | No | String | Name of the launch configuration. The name can be up to 60 bytes in size and contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points. |
| UserData | No | String | Base64-encoded custom data. Maximum 16 KB. If you want to clear UserData, specify it as an empty string |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues |

## 4. Sample

### Modifying the Image, Instance Type and Name of the Specified Launch Configuration

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&ImageId=img-8toqc6s3
&InstanceTypes.0=S2.SMALL1
&LaunchConfigurationName=updated_config
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "07022dcb-5bba-48f0-a2b0-800ad006d031"
    }
}
```

### Clearing UserData

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&UserData=
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "2c027f22-3a3b-489a-a77a-89c53fc15212"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyLaunchConfigurationAttributes)

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
| AccountQualificationRestrictions | The requesting account failed to pass the qualification review. |
| CallCvmError | CVM API call failed. |
| InvalidImageId.NotFound | The image was not found. |
| InvalidLaunchConfiguration.NameDuplicate | The launch configuration name already exists. |
| InvalidParameterValue.CvmConfigurationError | Exception with CVM parameter validation. |
