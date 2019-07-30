# 退款

### 1、退款

**官方文档：**

[alipay.trade.refund(统一收单交易退款接口)](https://docs.open.alipay.com/api_1/alipay.trade.refund/)

**请求参数说明：**

一般退款传交易号和退款金额就行，如有特殊需求，官方文档中需要传递的其他参数通过$params传递

**代码示例：**

```php
$result = $app->refund(string $tradeNo, $amount, string $outTradeNo = null, array $params = []);
```

### 2、退款查询

**官方文档：**

[alipay.trade.fastpay.refund.query(统一收单交易退款查询)](https://docs.open.alipay.com/api_1/alipay.trade.fastpay.refund.query/)

**代码示例：**

```php
$result = $app->refund->query(string $tradeNo, string $outTradeNo = null, string $outRequestNo = null, string $orgPid = null);
```

### 3、退款页面接口

**官方文档：**

[alipay.trade.page.refund(统一收单退款页面接口)](https://docs.open.alipay.com/api_1/alipay.trade.page.refund/)

**代码示例：**

```php
$result = $app->refund->page(string $tradeNo, $amount, string $outRequestNo, string $outTradeNo = null, array $params = [], string $httpMethod = 'POST');
```