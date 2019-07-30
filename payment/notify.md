# 通知

### 交易异步通知

**handleNotify方法中传入匿名函数的参数说明：**

$request 是 \WannanBigPig\Supports\Collection 对象，可以像操作数组一样取出支付请求的值

$response 是一个函数，只有一个参数，布尔值类型，返回值字符串 `success` 或 `fail`

**handleNotify方法返回值：**

\Symfony\Component\HttpFoundation\Response 对象。如果你需要直接输出使用 `$response->send()`, 在一些框架里（如 Laravel）不是输出而是返回：`return $response`。

**代码示例：**

> 以下示例是伪代码，开发者在使用此方法时根据业务需求仔细判断核对准确。sdk已经自动验证签名。如果签名验证不通过将会记录一条error级别的日志，调试时可根据日志判断验证签名是否通过。

```php
$response = $app->handleNotify(function($request, $response){
    $order = Sql::query(['out_trade_no' => $request->out_trade_no]);
    if(!$order || $order->pay_status === 1){
        // 订单不存在或者订单已处理，直接return，下面将不再继续处理
        return $response(false);
    }
  	// 判断订单金额是否一致
    if($order->total_amount !== $request->total_amount){
         return $response(false);
    }
  	// 判断 seller_id 、app_id等其他校验数据是否正常
    ...
    // 判断支付宝交易状态，然后修改服务端支付订单的状态
    if($request->trade_status === 'TRADE_SUCCESS'){
        ...
    }
    // 返回成功
  	return $response(); // $response默认参数true，所以成功时可不传参数
});

// 这一步别忘记了，不然支付宝服务器会不断重发通知，直到超过24小时22分钟
$response->send(); // return $response;

```

**异步通知说明**

* **第一步：** 在通知返回参数列表中，除去 sign、sign_type 两个参数外，凡是通知返回回来的参数皆是待验签的参数。

* **第二步：** 将剩下参数进行 url_decode，然后进行字典排序，组成字符串，得到待签名字符串：

```
app_id=2016092101248425&buyer_id=2088102114562585&buyer_pay_amount=0.80&fund_bill_list=[{"amount":"0.80","fundChannel":"ALIPAYACCOUNT"},{"amount":"0.20","fundChannel":"MDISCOUNT"}]&gmt_create=2016-10-12 21:36:12&gmt_payment=2016-10-12 21:37:19&invoice_amount=0.80&notify_id=7676a2e1e4e737cff30015c4b7b55e3kh6&notify_time=2016-10-12 21:41:23&notify_type=trade_status_sync&out_trade_no=mobile_rdm862016-10-12213600&passback_params=passback_params123&point_amount=0.00&receipt_amount=0.80&seller_id=2088201909970555&subject=PC网站支付交易&total_amount=1.00&trade_no=2016101221001004580200203978&trade_status=TRADE_SUCCESS&voucher_detail_list=[{"amount":"0.20","merchantContribute":"0.00","name":"5折券","otherContribute":"0.20","type":"ALIPAY_DISCOUNT_VOUCHER","voucherId":"2016101200073002586200003BQ4"}]
```

* **第三步：** 将签名参数（sign）使用 base64 解码为字节码串。

* **第四步：** 使用 RSA 的验签方法，通过签名字符串、签名参数（经过 base64 解码）及支付宝公钥验证签名。

* **第五步：**需要严格按照如下描述校验通知数据的正确性**：**
  1. 商户需要验证该通知数据中的 out_trade_no 是否为商户系统中创建的订单号；
  2. 判断 total_amount 是否确实为该订单的实际金额（即商户订单创建时的金额）；
  3. 校验通知中的 seller_id（或者 seller_email) 是否为 out_trade_no 这笔单据的对应的操作方（有的时候，一个商户可能有多个 seller_id/seller_email）；
  4. 验证 app_id 是否为该商户本身。