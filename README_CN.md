### 初始化

建议优先用测试服务器

在线接口测试[https://www.bitmex.com/api/explorer/](https://www.bitmex.com/api/explorer/)

测试服务器[https://testnet.bitmex.com](https://testnet.bitmex.com)

正式服务器[https://www.bitmex.com](https://www.bitmex.com)

所有的接口方式初始化与bitmex提供的接口方式一样，详细请看src/api

行情数据[more](https://github.com/zhouaini528/bitmex-php/blob/master/tests/position.php)
```php
//Get market data
//Market parameters can not key and secret
try {
    $bitmex=new Bitmex();
    $result=$bitmex->orderBook()->get([
        'symbol'=>'ETHUSD',
        'depth'=>20
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```

订单类[more](https://github.com/zhouaini528/bitmex-php/blob/master/tests/order.php)
```php
//Test API address  default  https://www.bitmex.com
$key='eLB_l505a_cuZL8Cmu5uo7EP';
$secret='wG3ndMquAPl6c-jHUQNhyBQJKGBwdFenIF2QxcgNKE_g8Kz3';
$host='https://testnet.bitmex.com';

$bitmex=new Bitmex($key,$secret,$host);

//bargaining transaction
try {
    $result=$bitmex->order()->post([
        'symbol'=>'XBTUSD',
        'price'=>'100',
        'side'=>'Buy',
        'orderQty'=>'1',
        'ordType'=>'Limit',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

//track the order
try {
    $result=$bitmex->order()->getOne([
        'symbol'=>'XBTUSD',
        'orderID'=>$result['orderID'],
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

//cancellation of order
try {
    $result=$bitmex->order()->delete([
        'symbol'=>'XBTUSD',
        'orderID'=>$result['orderID'],
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```


仓位查询[more](https://github.com/zhouaini528/bitmex-php/blob/master/tests/position.php)
```php
//bargaining transaction
try {
    $bitmex=new Bitmex($key,$secret,$host);
    $result=$bitmex->position()->get([
        'symbol'=>'XBTUSD',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```

更多用例请查看[more](https://github.com/zhouaini528/bitmex-php/tree/master/tests)

更多API请查看[more](https://github.com/zhouaini528/bitmex-php/tree/master/src/Api)

