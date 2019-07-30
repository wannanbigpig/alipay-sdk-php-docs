# 支付

你在阅读本文之前确认你已经仔细阅读了：[支付宝开发文档](https://docs.open.alipay.com/api_1)。

### 配置

配置在前面的例子中已经提到过了，支付的相关配置如下：

```php
use EasyAlipay\Alipay;

$config = [
  	// 必要配置
    'sys_params' => [
        'app_id' => '888888888888888',
        // 'notify_url' => 'http://alipay.docs.wannanbigpig.com/',
        // 'return_url' => 'http://alipay.docs.wannanbigpig.com/',
    ],
    'private_key_path' => STORAGE_ROOT.'private_key.pem',
    'alipay_public_Key_path' => STORAGE_ROOT.'alipay_public_key.pem',
];

$app = Alipay::payment($config);
```

`$app` 在后面的支付文档都是指  `Alipay::payment` 得到的实例，在此说明。

### 服务商

#### 设置子商户信息

```php
$app->setAppAuthToken('app_auth_token'); 
```

### 条码支付（统一收单交易支付接口）

[支付宝官方文档](https://docs.open.alipay.com/api_1/alipay.trade.pay)

```php
$result = $app->pay([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    // 'scene' => 'bar_code', // 条码支付可以不传，sdk默认 bar_code
    'auth_code' => '283856205796385922',
    'subject' => '大乐透',
    'total_amount' => '10',
]);
```

### 注意

1、接口中的notify_url和return_url默认读取传入配置参数，如需对个别接口修改可以如下操作：

```php
$app->setNotifyUrl($notifyUrl);
$result = $app->pay([
    ...
])
// or
$app->setNotifyUrl($notifyUrl)->pay([
    ...
]);
```

需要修改return_url的同上操作，使用方法 ```setReturnUrl(string $returnUrl)```

2、后续文档中有些默认值列出来的可不传，具体根据不同方法调用说明操作



