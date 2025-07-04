# 接口文档

## 帐户管理

### 获取当前帐户配置信息

>**GET** /v1/account

**返回数据**

| 参数名             | 类型     | 说明      |
|--------|--------|---------|
| serverNotifyUrl | string | 服务端通知地址 |

**返回数据示例**

```json
 {
  "serverNotifyUrl": "https://xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

### 设置回调地址

>**PATCH** /v1/account

**请求参数**

| 参数名             | 类型     | 说明      | 默认值 |
|--------|--------|---------|-----|
| serverNotifyUrl | string | 服务端通知地址 |     |

**请求数据示例**

```json
 {
  "serverNotifyUrl": "https://xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```
------

## 门店管理

### 获取当前关联门店信息
>**GET** /v1/stores

**返回数据**

| 参数名               | 类型       | 说明     |
|-------------------|----------|--------|
| stores            | object[] | 门店列表   |
| stores.id         | string   | 旅拍门店ID |
| stores.name       | string   | 店铺名称   |
| stores.outStoreId | string   | 外部门店ID |

**返回数据示例**

```json
{
  "stores": [
     {
       "id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
       "outStoreId": "3333333",
       "name": "name"
     }
  ]
}
```

### 配置关联门店信息
>**PATCH** /v1/stores

**请求参数**

| 参数名               | 类型       | 是否必填 | 说明     | 默认值 |
|-------------------|----------|------|--------|-----|
| stores            | object[] | 是    | 门店列表   |     |
| stores.id         | string   | 是    | 门店ID   |     |
| stores.outStoreId | string   | 否    | 外部门店ID |     |


**请求数据示例**

```json
 {
  "stores": [
     {
       "id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
       "outStoreId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
     }
  ]
}
```

------

## 订单管理

**订单状态枚举**

| 状态码           | 描述          |
|---------------|-------------|
| Initializing  | 修图准备中       |
| Retouching    | 修图中         |
| Retouched     | 修成完成，等待用户选片 |
| PhotoSelected | 用户选片完成      |

### 创建订单
>**POST** /v1/orders

**请求参数**

| 参数名                                   | 类型       | 是否必填 | 说明       | 默认值 |
|---------------------------------------|----------|------|----------|-----|
| storeId                               | string   | 是    | 旅拍门店ID   |     |
| outOrderId                            | string   | 是    | 外部系统订单ID |     |
| customers                             | object[] | 是    | 客户信息     |     |
| customers.mobile                      | string   | 是    | 客户手机号    |     |
| customers.age                         | string   | 否    | 年龄       |     |
| consumptionPackage                    | object   | 是    | 套餐信息     |     |
| consumptionPackage.photoNumber        | number   | 是    | 底片数量     |     |
| consumptionPackage.retouchPhotoNumber | number   | 是    | 精修数量     |     |

**请求数据示例**
```json
{
  "storeId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "outOrderId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "customers": [
    {
      "mobile": "15900000000",
      "age": "18"
    }
  ],
  "consumptionPackage": {
    "photoNumber": 1,
    "retouchPhotoNumber": 1
  }
}
```

**返回数据**

| 参数名        | 类型     | 说明     |
|------------|--------|--------|
| orderId    | string    | 旅拍订单ID |
| outOrderId | string    | 外部订单ID |
| storeId    | string    | 旅拍门店ID |
| tradeNo    | string    | 业务订单号  |
| status     | string   | 订单状态   |
| qrCode     | string   | 二维码    |

**返回数据示例**
```json
 {
  "orderId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "outOrderId": "4433455",
  "storeId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "tradeNo": "345324",
  "status": "Initializing",
  "qrCode": "http://xxxxx"
}
```

### 提交订单图片urls
>**PATCH** /v1/orders/{id}/image-urls

**请求参数**

| 参数名         | 类型       | 是否必填 | 说明   | 默认值 |
|-------------|----------|------|------|-----|
| images      | object[] | 是    | 图片列表 |     |
| images.name | string   | 否    | 图片名  |     |
| images.url  | string   | 是    | 下载地址 |     |

**请求数据示例**
```json
{
  "images": [
     {
       "name": "name",
       "url": "http://xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
     }
  ]
}
```

**返回数据**

| 参数名        | 类型     | 说明     |
|------------|--------|--------|
| orderId    | string    | 旅拍订单ID |
| outOrderId | string    | 外部订单ID |
| storeId    | string    | 旅拍门店ID |
| tradeNo    | string    | 业务订单号  |
| status     | string   | 订单状态   |
| qrCode     | string   | 二维码    |

**返回数据示例**
```json
 {
  "orderId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "outOrderId": "4433455",
  "storeId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "tradeNo": "345324",
  "status": "Initializing",
  "qrCode": "http://xxxxx"
}
```


### 获取订单详情
>**GET** /v1/orders/{orderId}

**返回数据**

| 参数名        | 类型     | 说明     |
|------------|--------|--------|
| orderId    | string    | 旅拍订单ID |
| outOrderId | string    | 外部订单ID |
| storeId    | string    | 旅拍门店ID |
| tradeNo    | string    | 业务订单号  |
| status     | string   | 订单状态   |
| qrCode     | string   | 二维码    |

**返回数据示例**
```json
 {
  "orderId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "outOrderId": "4433455",
  "storeId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "tradeNo": "345324",
  "status": "Initializing",
  "qrCode": "http://xxxxx"
}
```