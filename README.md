# wxwork_finance_sdk_wrapper

企业微信-获取会话内容PHP扩展


## 依赖
企业微信提供的sdk;

PHP VERSION >= 7.0

## 安装步骤及要求
```
       $INSATLL_PATH_PATH/bin/phpize
        
       ./configure --with-php-config=$INSTALL_PHP_PATH/php-config --with-wxwork-finance-sdk=$WXWORK_FINANCE_C_SDK_PATH
       
        make && make install
```
    php.ini 增加 extension=wxwork_finance_sdk.so
    
## API
```php
    WxworkFinanceSdkExcption::__construct();
```

```php
    WxworkFinanceSdk::__construct(string $corpId, string $secret, array $options);
    string $corpId 企业号

    string $secret 秘钥

    array $options = [ // 可选参数
        'proxy_host' => string,
        'proxy_password' => string,
        'timeout' => 10, // 默认超时时间为10s
    ]
```

```php
   string WxworkFinanceSdk::getChatData(int $seq, int $limit);
    * 拉取聊天数据
    $seq 起始位置
    $limit 获取条数
``` 

```php
   array WxworkFinanceSdk::getMediaData(string $fileId, string $indexBuf = '')
   * 拉取媒体消息
    $filedId  从GetChatData返回的聊天消息中，媒体消息包括的sdkfileid
    $indexBuf 下一次拉取记录

    返回结构:
    [
        'data' => '媒体内容',
        'nextIndex' => '下一次拉取记录',
        'isFininshed' => bool // true 数据已全部拉取完毕
    ]

```

 ## 示例
 ```php
        $sdk = new WxworkFinanceSdk("wwd08coe7d775abaaa", "zJ6k0naVVQ--gt9PUSSEvs03zW_nlDVmjAkPOTAfrew", [
                   "proxy_host" => "hello", // 代理地址
                   "proxy_password" => "world", // 代理密码
                   "timeout" => 100, // 超时时间
               ]);
               
               var_dump(json_decode($sdk->getChatData(0, 100)));
       
                return [
                    'data' => string // 返回的数据,
                    'nextIndex' => string // 下一个指针,
                    'isFinished' => bool // 是否继续获取 下一条数据标识
                ];
               
               var_dump($sdk->getMediaData("dddd"));
 ```
    
