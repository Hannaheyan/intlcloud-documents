## 1. 接口描述
本接口(RecordDelete)用于删除解析记录。
接口请求域名：<font style="color:red">cns.api.qcloud.com</font>

## 2. 输入参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见 [公共请求参数](https://intl.cloud.tencent.com/document/api/377/4153) 页面。其中，此接口的 Action 字段为 RecordDelete。

| 参数名称 | 是否必选  | 类型 | 描述 |
|---------|---------|---------|---------|
| domain | 是 | String | 解析记录所在的域名 |
| recordId | 是 | Int | 解析记录ID |


## 3. 输出参数
| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | Int | 公共错误码, 0表示成功，其他值表示失败。 |
| message | String | 模块错误信息描述，与接口相关。|


## 4. 示例
```
https://cns.api.qcloud.com/v2/index.php?
&<公共请求参数>
&Action=RecordDelete
&domain=qcloud.com
&recordId=371266
```


返回示例如下：
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success"
}
```
