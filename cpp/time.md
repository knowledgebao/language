# time

## 简介

## ctime

## chrono

```C++
#include <chrono>
using namespace chrono;
```

### duration

duration 是 chrono 裡面，用来记录时间长度的类别，他基本上是一个 template class，可以自行定义他的意义；chrono 也有提供一些比较常见的时间类别，可以直接拿来使用，下面就是内建的 duration 的型别：

```C++
typedef duration<long long, nano> nanoseconds;
typedef duration<long long, micro> microseconds;
typedef duration<long long, milli> milliseconds;
typedef duration<long long> seconds;
typedef duration<int, ratio<60> > minutes;
typedef duration<int, ratio<3600> > hours;
```

```C++
std::chrono::minutes t1( 10 );
std::chrono::seconds t2( 60 );
std::chrono::seconds t3 = t1 - t2;
std::cout << t3.count() << " second" << std::endl;//540 .count()取的一个duration的值
cout << chrono::duration_cast<chrono::minutes>( t3 ).count() << endl;//9
```

### time_point

相较于 duration 是用来记录时间的长度的
time_point 是用来记录一个特定时间点的资料类别。
他一样是一个 template class，需要指定要使用的 clock 与时间单位（duration）。

`system_clock` 是直接去抓系统的时间，1970-01-01 00:00:00 UTC逝去的时间单位是1个tick
`steady_clock` 系统开机到现在逝去的纳秒
`high_resolution_clock` typedef steady_clock high_resolution_clock;

```C++
std::chrono::steady_clock::time_point t1 = std::chrono::steady_clock::now();
std::cout << "Hello World\n";
std::chrono::steady_clock::time_point t2 = std::chrono::steady_clock::now();
std::cout << "Printing took "
  << std::chrono::duration_cast<std::chrono::microseconds>(t2 - t1).count()
  << "us.\n";
std::chrono::system_clock::time_point nt = t1 + std::chrono::hours(10);
std::time_t now_c = std::chrono::system_clock::to_time_t( nt );//输出先转为time_t
std::cout << std::ctime( &now_c ) << std::endl;
```

## 参考资料

1. [C++11 时间工具chrono](https://www.jianshu.com/p/170164adae0f)
