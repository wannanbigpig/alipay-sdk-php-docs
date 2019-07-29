# 统一收单交易

### POS机支付

scene参数可以不传，sdk默认bar_code（条码支付）

```php
$result = $app->pay([
    'out_trade_no' => \WannanBigPig\Supports\Str::getRandomInt(),
    // 'scene' => 'bar_code', // 条码支付可以不传，sdk默认 bar_code
    'auth_code' => '283856205796385922',
    'subject' => '大乐透',
    'total_amount' => '10',
]);
```



