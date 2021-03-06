# Kubernetes 集群扩容 {#reference_agj_fx2_xdb .reference}

增加集群中Worker节点的数量（该操作仅限于ROS生成的资源）。

## 请求信息 {#section_r2n_jx2_xdb .section}

**请求行 RequestLine**

``` {#codeblock_bco_6ar_7pp}
PUT /clusters/{cluster_id} HTTP/1.1
```

**请求行参数 URI Param**

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|cluster\_id|string|是|集群ID|

**特有请求头 RequestHead**

无，请参考[公共请求头部](intl.zh-CN/开发指南/集群 API 调用方式/公共参数.md#section_mr5_lf1_wdb)。

**请求体 RequestBody**

``` {#codeblock_ny5_axb_6kh}
{
    "disable_rollback": "失败是否回滚",
    "timeout_mins": "集群创建超时时间",
    "worker_instance_type": "Worker实例规格",
    "login_password": "节点SSH登录密码",    
    "num_of_nodes": "Worker节点数",
    "tags": "给扩容节点打tag标签, 数组格式对象"
}
```

**请求体解释**

|名称|类型|必须|描述|
|:-|:-|:-|:-|
|disable\_rollback|bool|是|失败是否回滚，true 表示失败不回滚，false 表示失败回滚。如果选择失败回滚，则会释放创建过程中所生产的资源，不推荐使用 false|
|timeout\_mins|int|是|集群资源栈创建超时时间，以分钟为单位，默认值 60。|
|worker\_instance\_type|string|是|Worker 节点 ECS 规格类型代码。更多详细信息，参见[../../../../dita-oss-bucket/SP\_2/DNA0011858383/ZH-CN\_TP\_9548.md\#](../../../../intl.zh-CN/实例/实例规格族.md#)。|
|login\_password|string|是|SSH登录密码。密码规则为8 - 30 个字符，且同时包含三项（大、小写字母，数字和特殊符号）该密码必须和创建集群时的密码一致。 **说明：** login\_password与num\_of\_nodes两者只能配置一个，且需要与创建集群时选用的参数一致。

 |
|num\_of\_nodes|int|是|Worker节点数。范围是\[0,300\]。如果是扩容，该值要大于已有Worker节点数。 **说明：** login\_password与num\_of\_nodes两者只能配置一个，且需要与创建集群时选用的参数一致。

 |
|tags|list|否|给集群打tag标签： -   key：标签名称
-   value：标签值

 |

## 返回信息 {#section_w1l_gz2_xdb .section}

**返回行 ResponseLine**

``` {#codeblock_hgz_owu_3ez}
HTTP/1.1 202 Accepted
```

**特有返回头 ResponseHead**

无，请参考[公共返回头部](intl.zh-CN/开发指南/集群 API 调用方式/公共参数.md#section_zr5_lf1_wdb)。

**返回体 ResponseBody**

``` {#codeblock_5dv_rs8_f7w}
{
    "cluster_id":"string",
    "request_id":"string",
    "task_id":"string"
}
```

## 示例 {#section_dsh_jz2_xdb .section}

**请求示例**

``` {#codeblock_mbk_pyv_1no}
PUT /clusters/Cccfd68c474454665ace07efce924f75f HTTP/1.1
<公共请求头>
{
    "disable_rollback": true,
    "timeout_mins": 60,
    "worker_instance_type": "ecs.sn1ne.large",
    "login_password": "Hello1234",
    "tags":[]
}
```

**返回示例**

``` {#codeblock_efe_vh2_3qr}
HTTP/1.1 202 Accepted
<公共响应头>
{
    "cluster_id": "Cccfd68c474454665ace07efce924f75f",
    "request_id": "687C5BAA-D103-4993-884B-C35E4314A1E1",
    "task_id": "T-5a54309c80282e39ea00002f"
}
```

