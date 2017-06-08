
prometheus 快速接入包
====================

Installation
------------
```shell
composer require imj/prometheus_client_php_wrapper
```

Basic Usage
------------

```php
require __DIR__ . '/../vendor/autoload.php';

// 初始化
PrometheusWrapper\Wrapper::ins()->setConfig([
  "app" => "test",
  "idc" => "dev",
  "counter_path" => [ // 添加 counter 统计的 path
    "/wrapperTest.php"
  ],
  "histogram_path" => [ // 添加 histogram 统计的 path
    "/wrapperTest.php"
  ],
  "log_method" => [ // method 过滤
    "GET",
    "POST",
    "HEAD"
  ],
  "buckets" => [1,2,3,4,5,6,7,8,9,10,11,13,15,17,19,22,25,28,32,36,41,47,54,62,71,81,92,105,120,137,156,178,203,231,263,299,340,387,440,500], // 桶距配置
  "adapter" => "redis",
  "redisOptions" => [
    'host' => '127.0.0.1',
    'auth' => "123456"
  ],
  "redisIns" => null // 也可以传入一个 redis 实例
])->init();

if (isset($_GET['clean'])) {
  // 清除统计数据
  PrometheusWrapper\Wrapper::ins()->flush();
}

// 自定义统计项
PrometheusWrapper\Wrapper::ins()->latencyLog(rand(1, 20), "searcher", "/get", "GET"); // 延迟
PrometheusWrapper\Wrapper::ins()->counterLog(1, "searcher", "/get", "GET", 200); // 计数

// 统计页面
echo PrometheusWrapper\Wrapper::ins();
```

License
------------

licensed under the MIT License - see the `LICENSE` file for details