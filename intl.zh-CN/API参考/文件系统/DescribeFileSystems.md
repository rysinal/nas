# DescribeFileSystems {#doc_api_NAS_DescribeFileSystems .reference}

DescribeFileSystems用于返回文件系统的描述信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DescribeFileSystems&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeFileSystems|操作接口名，系统规定参数，取值：DescribeFileSystems

 |
|FileSystemId|String|否|109c042666|文件系统 ID

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |
|PageNumber|Integer|否|1|列表的分页页码（从 1 开始计数）

 |
|PageSize|Integer|否|1|每个分页包含的文件系统个数（默认为 10）

 |
|VpcId|String|否|vpc-bp1sevsgtqvk5gxblhhod|专有网络 ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|列表的分页页码

 |
|PageSize|Integer|1|每个分页包含的文件系统个数

 |
|RequestId|String|035B3A3A-E514-4B41-B906-5D906CFBD65F|请求 ID

 |
|TotalCount|Integer|1|文件系统的总个数

 |
|FileSystems| | |文件系统描述信息

 |
|Bandwidth|Long|150|文件系统吞吐上限（单位MB/s），通用型没有该字段

 |
|Capacity|Long|1|文件系统容量（单位GB）

 |
|CreateTime|String|2017-05-27T15:43:06CST|文件系统创建时间

 |
|Description|String|空|文件系统描述

 |
|Destription|String|空|文件系统描述

 |
|FileSystemId|String|109c042666|文件系统ID

 |
|MeteredSize|Long|1611661312|文件系统已使用量（上一小时最大使用量，非当前值，单位Byte）

 |
|MountTargets| | |挂载目标

 |
|AccessGroupName|String|test-001|挂载点使用的权限组名称

 |
|MountTargetDomain|String|109c042666-wjb85.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|NetworkType|String|vpc|网络类型，枚举值：vpc、classic

 |
|Status|String|active|挂载点状态，通用型 NAS：active、inactive

 |
|VpcId|String|vpc-bp1sevsgtqvk5gxblhhod|vpcid

 |
|VswId|String|vsw-bp1omfzsszekkvaxnz66e|vswid

 |
|Packages| | |已绑定的存储包

 |
|PackageId|String|naspackage-xxxxxxxxxxx-xxxxxx|存储包ID

 |
|ProtocolType|String|NFS|协议类型

 |
|RegionId|String|cn-hangzhou|区域ID

 |
|Status|String|Pending|文件系统状态，仅极速型NAS有，状态枚举值包括：Pending、Running、Stopped，当状态为Running时才可以进行后续操作（如创建挂载点等）

 |
|StorageType|String|Performance|存储类型，通用型NAS：Capacity、Performance，极速型NAS：standard、advance

 |
|ZoneId|String|cn-hangzhou-b|所在可用区

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeFileSystems
&FileSystemId=109c042666
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeFileSystemsResponse>
    <PageNumber>1</PageNumber>
    <TotalCount>1</TotalCount>
    <PageSize>1</PageSize>
    <RequestId>035B3A3A-E514-4B41-B906-5D906CFBD65F</RequestId>
    <FileSystems>
        <FileSystem>
            <FileSystemId>109c042666</FileSystemId>
            <ProtocolType>NFS</ProtocolType>
            <RegionId>cn-hangzhou</RegionId>
            <CreateTime>2017-05-27T15:43:06CST</CreateTime>
            <Destription></Destription>
            <MountTargets>
                <MountTarget>
                    <MountTargetDomain>109c042666-wjb85.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
                </MountTarget>
            </MountTargets>
            <StorageType>Performance</StorageType>
            <MeteredSize>1611661312</MeteredSize>
        </FileSystem>
    </FileSystems>
</DescribeFileSystemsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":1,
	"RequestId":"BC7C825C-5F65-4B56-BEF6-98C56C7C546E",
	"FileSystems":{
		"FileSystem":[
			{
				"FileSystemId":"31a8e48eda",
				"Description":"31a8e48eda",
				"Packages":{
					"Package":[
						{
							"PackageId":""
						}
					]
				},
				"ProtocolType":"NFS",
				"CreateTime":"2017-04-18T00:22:56CST",
				"RegionId":"cn-shanghai",
				"Destription":"31a8e48eda",
				"ZoneId":"cn-shanghai-b",
				"StorageType":"Performance",
				"MountTargets":{
					"MountTarget":[
						{
							"NetworkType":"vpc",
							"Status":"active",
							"VswId":"vsw-uf64zi0nn71ntvkbzdti4",
							"AccessGroupName":"DEFAULT_VPC_GROUP_NAME",
							"MountTargetDomain":"31a8e48eda-ykf64.cn-shanghai.nas.aliyuncs.com",
							"VpcId":"vpc-uf65wx2khu08h4dlw2qfv"
						}
					]
				},
				"MeteredSize":4295639040
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

