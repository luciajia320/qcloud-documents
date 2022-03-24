bucket-tagging 命令用于创建（修改）、获取、删除存储桶标签

## 命令选项
bucket-tagging 命令包含以下可选 flag：

|flag 简写|flag 全称| flag 用途|
|----|----|----|
|-m|--method|指定需要进行的操作，包括 put、get、delete|
|-h|--help|输出帮助信息|
|-c|--config-path|指定要使用的配置文件路径|
|-e|--endpoint|除了在配置文件中提前配置存储桶的地域外，COSCLI 也支持在命令中通过`-e`指定存储桶的 endpoint，endpoint 形如`cos.<region>.myqcloud.com`，其中`<region>`代表存储桶地域，如`ap-guangzhou`、`ap-beijing`等，COS 支持的地域列表可参考 [地域与访问域名](https://cloud.tencent.com/document/product/436/6224)|
|-i|--sercret-id|指定访问 COS 使用的密钥中的 SecretId|
|-k|--sercret-key|指定访问 COS 使用的密钥中的 SercretKey |
|-t|--sesssion-token|若用户通过临时密钥访问 COS，可通过`-t`指定临时密钥中的 token|

## 添加或修改存储桶标签
存储桶标签是用一组健值对（Key-Value）来表示，只有存储桶所有者及拥有 PutBucketTagging权限的用户才可以添加或修改存储桶标签，否则会返回错误码 403 AccessDenied
### 命令格式
```
./coscli bucket-tagging --method put cos://<BucketName-APPID> key1#value1 key2#value2
```
其中，`key#value`表示标签键值对Key-Value，key和value之间以井号（#）分割。若存储桶未设置标签，此命令将为存储桶添加指定的标签；若存储桶已设置标签，此命令将覆盖原有标签。

### 使用示例
为存储桶 examplebucket配置两组标签，其中一组标签的key为1，value为111，一组标签的key为2，value为222。命令如下，

```
./coscli bucket-tagging --method put cos://exmaplebucket-125000000 1#111 2#222
```

## 获取存储桶标签
### 命令格式
```
./coscli bucket-tagging --method get cos://<BucketName-APPID>
```

### 使用示例
```
./coscli bucket-tagging --method get cos://exmaplebucket-125000000
```
以下输出结果表明examplebucket配置了两组标签，其中一组标签的key为1，value为111，一组标签的key为2，value为222。
```
  KEY | VALUE  
------+--------
    1 |   111  
    2 |   222 
```

## 删除存储桶标签
### 命令格式
```
./coscli bucket-tagging --method delete cos://<BucketName-APPID>
```
### 使用示例
```
./coscli bucket-tagging --method delete cos://exmaplebucket-125000000
```
