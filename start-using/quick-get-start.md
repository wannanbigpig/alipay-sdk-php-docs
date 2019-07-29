# 快速入门

```php
use EasyAlipay\Alipay;

// 配置（包含支付宝的公共配置，日志配置，http配置等）
$config = [
    'sys_params' => [
        'app_id' => '888888888888888',
        'notify_url' => 'http://alipay.docs.wannanbigpig.com/',
    ],
    'private_key_path' => STORAGE_ROOT.'private_key.pem',
    'alipay_public_Key_path' => STORAGE_ROOT.'alipay_public_key.pem',
];

$app = Alipay::payment($config);

// 当面付 统一收单交易支付接口
$response = $app->pay([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    'scene' => 'bar_code',
    'auth_code' => '283867319836385922',
    'subject' => 'ceshiapi',
    'total_amount' => '100',
]);

if($response['code'] === '10000'){
    echo $response['trade_no'];    // 2019072722001491681000180973
}
```