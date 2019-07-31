# 支付

### 1、POS机支付（条码支付）

**官方文档：**

[alipay.trade.pay(统一收单交易支付接口)](https://docs.open.alipay.com/api_1/alipay.trade.pay)

**默认业务请求参数：**

scene参数可以不传，sdk默认bar_code（条码支付）

**代码示例：**

```php
$result = $app->pay([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    // 'scene' => 'bar_code', // 条码支付可以不传，sdk默认 bar_code
    'auth_code' => '283856205796385922',
    'subject' => '大乐透',
    'total_amount' => '10',
]);
```

### 2、扫码支付（生成支付二维码）

**官方文档：**

[alipay.trade.precreate(统一收单线下交易预创建)](https://docs.open.alipay.com/api_1/alipay.trade.precreate/)

**代码示例：**

```php
$result = $app->preCreate([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    'total_amount' => 100,
    'subject' => 'mac X pro 2080',
    'body' => 'mac X pro 2080',
]);
```

### 3、小程序支付

**官方文档：**

[alipay.trade.create(统一收单交易创建接口)](https://docs.open.alipay.com/api_1/alipay.trade.create/)

**代码示例：**

```php
$result = $app->create([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    'total_amount' => 100,
    'buyer_id' => '2088102177891684',
    'subject' => 'mac X pro 2080',
    'body' => 'mac X pro 2080',
]);
```

### 4、pc支付

**默认业务请求参数：**

```
'timeout_express' => '1c',
'product_code' => 'FAST_INSTANT_TRADE_PAY',
```

**官方文档：**

[alipay.trade.page.pay(统一收单下单并支付页面接口)](https://docs.open.alipay.com/api_1/alipay.trade.page.pay/)

**代码示例：**

```php
$result = $app->pay->pc([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    'subject' => '绿茶-黄山毛峰',
    'total_amount' => '22134.36',
]);
```

### 5、wap支付

**默认业务请求参数：**

```
'timeout_express' => '1c',
'product_code' => 'QUICK_WAP_WAY',
```

**官方文档：**

[alipay.trade.wap.pay(手机网站支付接口2.0)](https://docs.open.alipay.com/api_1/alipay.trade.wap.pay/)

**代码示例：**

```php
$result = $app->pay->wap([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    'subject' => '绿茶-黄山毛峰',
    'total_amount' => '22134.36',
]);
```

### 6、app支付

**默认业务请求参数：**

```
'timeout_express' => '1c',
'product_code' => 'QUICK_MSECURITY_PAY',
```

**官方文档：**

[alipay.trade.app.pay(app支付接口2.0)](https://docs.open.alipay.com/api_1/alipay.trade.app.pay/)

**代码示例：**

```php
$result = $app->pay->app([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    'subject' => '绿茶-黄山毛峰',
    'total_amount' => '22134.36',
]);
```

### 7、刷脸支付初始化

**官方文档：**

[zoloz.authentication.customer.smilepay.initialize(人脸初始化唤起zim)](https://docs.open.alipay.com/api_46/zoloz.authentication.customer.smilepay.initialize)

**代码示例：**

```php
$result = $app->pay->face(string $zimmetainfo);
```

