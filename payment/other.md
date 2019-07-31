# 其他操作

### 1、支付结果查询

**官方文档：**

[alipay.trade.query(统一收单线下交易查询) ](https://docs.open.alipay.com/api_1/alipay.trade.query/)

**代码示例：**

```php
$result = $app->query(string $tradeNo, string $outTradeNo = null, string $orgPid = null);
```

### 2、撤销交易

**官方文档：**

[alipay.trade.cancel(统一收单交易撤销接口)](https://docs.open.alipay.com/api_1/alipay.trade.cancel/)

**代码示例：**

```php
$result = $app->cancel(string $tradeNo, string $outTradeNo = null);
```

### 3、关闭交易

**官方文档：**

[alipay.trade.close(统一收单交易关闭接口)](https://docs.open.alipay.com/api_1/alipay.trade.close/)

**代码示例：**

```php
$result = $app->close(string $tradeNo, string $outTradeNo = null, string $operatorId = null);
```

### 4、交易结算

**业务请求参数说明：**

$royaltyParameters 传入的是一维数组SDK会自动转换成二维数组

**官方文档：**

[alipay.trade.order.settle(统一收单交易结算接口)](https://docs.open.alipay.com/api_1/alipay.trade.order.settle/)

**代码示例：**

```php
$result = $app->orderSettle(
    string $outRequestNo, 
    string $tradeNo, 
    array $royaltyParameters, 
    string $operatorId = null
);
```

### 5、支付宝订单信息同步

**官方文档：**

[alipay.trade.orderinfo.sync(支付宝订单信息同步接口)](https://docs.open.alipay.com/api_1/alipay.trade.orderinfo.sync/)

**代码示例：**

```php
$result = $app->orderInfoSync(
    string $tradeNo, 
    string $outRequestNo, 
    string $bizType, 
    string $origRequestNo = null, 
    string $orderBizInfo = null
);
```

### 6、对账单下载

**官方文档：**

[alipay.data.dataservice.bill.downloadurl.query(查询对账单下载地址)](https://docs.open.alipay.com/api_15/alipay.data.dataservice.bill.downloadurl.query)

**代码示例：**

```php
$result = $app->bill->get(string $billType, string $billDate);
```

