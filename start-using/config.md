# 配置

需要改动的配置不多，大部分使用默认值就可以了：

```php
// 配置（包含支付宝的公共配置，日志配置，http配置等）
$config = [
    'sys_params' => [
        'app_id' => '888888888888888',
        'notify_url' => 'http://alipay.docs.wannanbigpig.com/',
        'return_url' => 'http://alipay.docs.wannanbigpig.com/',
    ],
    'private_key_path' => STORAGE_ROOT.'private_key.pem',
    'alipay_public_Key_path' => STORAGE_ROOT.'alipay_public_key.pem',
];
```

完整配置：

```php
// 配置（包含支付宝的公共配置，日志配置，http配置等）
$config = [
  	/**
  	 * 公共参数配置
  	 */
    'sys_params' => [
        'app_id' => '888888888888888',
        'charset' => 'UTF-8',
        'sign_type' => 'RSA2',
        'app_auth_token' => '', // 该参数也可在具体使用之前通过调用setAppAuthToken方法的是方式写入
        'notify_url' => 'http://alipay.docs.wannanbigpig.com/',
        'return_url' => 'http://alipay.docs.wannanbigpig.com/',
    ],
    'private_key_path' => STORAGE_ROOT.'private_key.pem',
  	// 'private_key' => '私钥字符串', // 和 private_key_path 二选一
    'alipay_public_Key_path' => STORAGE_ROOT.'alipay_public_key.pem',
  	// 'alipay_public_Key' => '支付宝公钥字符串', // 和 alipay_public_Key_path 二选一
    'handle_response' => true, // 处理支付宝的返回值，不填默认true
    /**
     * 指定 API 调用返回结果的类型：array/collection/object/raw，不填默认array
     */
    'response_type' => 'array',
    /**
     * 网关配置：dev，normal两种模式，dev则使用沙箱网关，normal正常网关，不填默认normal
     */
    'env' => 'normal',
  	/**
  	 * 以下是log默认的配置
  	 */
    'log' => [
        'driver' => 'single', // 目前支持两种single，daily可选
        'identify' => 'wannanbigpig.support',
        'level' => 'notice', // 日志级别, 可选为：debug/info/notice/warning/error/critical/alert/emergency
        'format' => "%datetime% > %channel% [ %level_name% ] > %message% %context% %extra%\n",
        'path' => '/tmp/wannanbigpig.alipay.log', // 绝对路径
        // 'day' => 0, // driver 为 daily 时选填，0为无限文件数量
    ],
    /**
     * 接口请求相关配置，超时时间等，具体可用参数请参考：
     * https://guzzle-cn.readthedocs.io/zh_CN/latest/request-options.html
     * - log_template: 指定 HTTP 日志模板，请参考：https://github.com/guzzle/guzzle/blob/master/src/MessageFormatter.php
     */
    'http' => [
        'timeout' => 6.0,
        'connect_timeout' => 6.0,
        // 'base_uri' => 'https://openapi.alipay.com/gateway.do', // 默认根据env配置项选择正式网关或者沙箱网关
        'log_template' => "\n>>>>>>>>request\n--------\n{request}\n--------\n>>>>>>>>response\n--------\n{response}\n--------\n>>>>>>>>error\n--------\n{error}\n--------\n",
    ],
];
```

