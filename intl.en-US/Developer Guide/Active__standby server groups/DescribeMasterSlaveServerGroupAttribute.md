# DescribeMasterSlaveServerGroupAttribute {#doc_api_Slb_DescribeMasterSlaveServerGroupAttribute .reference}

Queries the details of an active/standby server group.

## Debug {#apiExplorer .section}

Use [OpenAPI Explorer](https://api.aliyun.com/#product=Slb&api=DescribeMasterSlaveServerGroupAttribute) to perform debug operations and generate SDK code examples.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example value|Description|
|---------|----|---------|-------------|-----------|
|Action|String|Yes|DescribeMasterSlaveServerGroupAttribute| The name of this action.

 Value: **DescribeMasterSlaveServerGroupAttribute**

 |
|MasterSlaveServerGroupId|String|Yes|rsp-cige6j5e7p| The ID of the active/standby server group to be queried.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the SLB instance belongs.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example value|Description|
|---------|----|-------------|-----------|
|MasterSlaveServerGroupId|String|rsp-cige6j5e7p| The ID of the active/standby server group.

 |
|MasterSlaveServerGroupName|String|Group1| The name of the active/standby server group.

 |
|MasterSlaveBackendServers| | | A list of backend servers in the active/standby server group.

 |
|└ServerId|String|vm-233| The ECS instance ID or ENI ID.

 |
|└Port|Integer|90| The port used by the backend server.

 |
|└Weight|Integer|100| The weight of the backend server.

 |
|└ServerType|String|Slave| The backend server type. Valid values:**Master | Slave**. Default value: Master

 |
|└Description|String|A description of the active/standby server group| A description of the active/standby server group.

 |
|└Type|String|ecs| The backend server type. Valid values:

 -   **ecs**: ECS instance \(default\)
-   **eni**: Elastic Network Interface \(ENI\)

 |
|RequestId|String|9DEC9C28-AB05-4DDF-9A78-6B08EC9CE18C| The ID of the request.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

http(s)://[Endpoint]/? Action=DescribeMasterSlaveServerGroupAttribute
&MasterSlaveServerGroupId=rsp-cige6j5e7p
&RegionId=cn-hangzhou
&<CommonParameters>

```

Response example

`XML` format

``` {#xml_return_success_demo}
<DescribeMasterSlaveServerGroupAttributeResponse>
  <RequestId>9DEC9C28-AB05-4DDF-9A78-6B08EC9CE18C</RequestId>
  <MasterSlaveServerGroupId>rsp-cige6j5e7p</MasterSlaveServerGroupId>
  <MasterSlaveBackendServers>
    <MasterSlaveBackendServers>
      <ServerId>vm-233</ServerId>
      <Port>80</Port>
      <Weight>100</Weight>
      <ServerType>Master</ServerType>
    </MasterSlaveBackendServers>
    <MasterSlaveBackendServers>
      <ServerId>vm-232</ServerId>
      <Port>90</Port>
      <Weight>100</Weight>
      <ServerType>Slave</ServerType>
    </MasterSlaveBackendServers>
  </MasterSlaveBackendServers>
</DescribeMasterSlaveServerGroupAttributeResponse>

```

## Error codes {#section_zx4_hma_tz5 .section}

[See common error codes.](https://error-center.alibabacloud.com/status/product/Slb)

