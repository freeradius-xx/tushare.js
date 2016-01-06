# tushare.js

这是[tushare](http://tushare.org/)的nodejs版，正在开发当中。如果有感兴趣的同学，非常欢迎一起完善该项目。

tushare的数据大多来自于各大网站股票金融频道的数据。本质上是去抓取这些网站的数据，以此方便二次使用。文档目前并不完善，使用方法（接口）
请参考`test/`目录内的单元测试

### 使用方法:
```
npm install tushare --save
npm run build
npm run test
```

然后:
```
var tushare = require('tushare');
tushare.stock.getTodayAll(function(err, data) {
  console.log(data);
});

```

## 交易数据

## 1. 获取个股历史数据
```
const option = {
  code: '600848',
  ktype: 'week'
};
tushare.stock.getHistory(options, function(err, data) {
  console.log(data);
});

```

`options` 参数说明：
```
{
code: {String} 股票代码，6位数字代码
ktype: {String} 数据类型，day=日k线 week=周 month=月 5=5分钟 15=15分钟 30=30分钟 60=60分钟，默认为day
start: {String} 开始日期，格式YYYY-MM-DD
end: {String} 结束日期，格式YYYY-MM-DD
}
```

## 2. 获取历史分笔数据
```
const options = {
  code: '600848',
  date: '2015-12-31'
};
tushare.stock.getTick(options, function(err, data) {
  console.log(data);
});
```

`options` 参数说明：
```
{
  date: {String} 历史分笔日期，格式YYYY-MM-DD
  code: {String} 股票代码，6位数字代码
}
```

## 3. 实时行情
```
tushare.stock.getTodayAll(function(err, data) {
  console.log(data);
});
```

`options(可选)` 参数说明：
```
{
  pageSize: 设置单次返回股票的数量，默认10000，即全部股票
  pageNo: 页码，都懂得
}
```

## 4. 实时分笔
```
var options = {
  codes: [
    '600848',
    '600000'
  ]
};
tushare.stock.getLiveData(options, function(err, data) {
  console.log(data);
});
```

`options` 参数说明：
```
{
  codes: 股票代码数组
}
```

## 5. 当日历史分笔
>该方法返回指定时间前五分钟的分笔数据，如需获得所有数据，需要多次调用该方法

```
var options = {
  code: '600848',
  end: '15:00:00'
};
tushare.stock.getTodayTick(options, function(err, data) {
  console.log(data);
});
```

`options` 参数说明：
```
{
  code: 股票代码，6位数字
  end: 结束时间
}
```

## 6. 大盘指数行情数据
```
tushare.stock.getIndex(function(err, data) {
  console.log(data);
});
```

## 7. 大单交易数据
```
var options = {
  code: '600848',
  volume: 700
};
tushare.stock.getSinaDD(options, function(err, data) {
  console.log(data);
});
```

`options` 参数说明：
```
{
  code: 股票代码，6位数字
  volume: (手)默认400，返回大于xx手的大单数据
}
```
