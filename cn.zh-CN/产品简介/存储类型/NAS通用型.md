# NAS通用型 {#concept_71454_zh .concept}

NAS 通用型是 NAS 中最为常用的存储类型。该存储类型无需本地客户端，使用方便，能够满足用户日常业务对文件存储的需求。

## 简介 {#section_yhk_zm5_2fb .section}

NAS 通用型又可分为容量型和性能型两种。这两种存储类型使用不同的存储介质，在性能、协议兼容性及计费方式等方面均有所不同，二者的核心区别如下：

-   NAS 性能型专注于高性能，旨在为工作负载提供更高吞吐量（约为容量型的 4 倍）、更高 IOPS 及更低时延（比容量型低约 2 至 4 倍）的高存储性能。
-   NAS 容量型专注于低成本，旨在以更低的成本为工作负载提供高效可靠的存储空间。

## 应用场景 {#section_kh2_dn5_2fb .section}

NAS 通用型存储能够满足用户业务对文件存储的需求，适用于各种文件存储场景，如：

-   业务系统文件共享
-   业务系统日志存储与分析
-   业务系统开发测试数据存储
-   企业数据库备份存储
-   OA（Office Automation, 办公自动化）系统后端文件存储
-   Web 站点数据的存储和分发

在使用 NAS 通用型存储时，用户还需要根据实际场景对 NAS 性能型和 NAS 容量型进行选择：

-   如果应用场景对吞吐量或时延要求较高，如文件操作频繁或需要即时反映文件修改结果，可以使用 NAS 性能型，从而保证存储性能。
-   如果应用场景对性能要求不高且存储容量较大，如大量文件数据的静态备份，可以使用 NAS 容量型，从而降低存储成本。

## 特性比较 {#section_dtd_hn5_2fb .section}

下表对 NAS 性能型和 NAS 容量型的性能指标、协议兼容性和计费方式进行了比较，供您在选择时进行参考。

|对比项|NAS性能型|NAS容量型|
|---|------|------|
|存储介质|SSD|SSD + SATA HDD|
|吞吐上限（MB/s）|0.58 MB/s \* 文件系统存储空间（GB） + 600 MB/s（最大 20GB/s\)|0.14 MB/s \* 文件系统存储空间（GB） + 150 MB/s（最大 10GB/s\)|
|最大 IOPS|50000|15000|
|兼容协议|NFS \(v3.0/v4.0\)，SMB \(v2.0/v2.1/v3.0\)|NFS \(v3.0/v4.0\)，SMB \(v2.0/v2.1/v3.0\)|
|计费方式|支持按量付费和存储包，可在创建文件系统时选择是否绑定存储包。|必须绑定存储包，如果实际存储容量超过存储包，超出部分按量付费。|

## 计费方式 { .section}

有关 NAS 的详细计费方式，请参见[文件存储详细价格信息](https://www.alibabacloud.com/zh/product/nas/pricing)。

