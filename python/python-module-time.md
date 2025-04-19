# python-module-time（时间相关模块）

## 时间相关模块

- time
- datetime
- calendar

## 时间（`time`）

- 时间结构体 time.struct_time(tm_year,tm_mon,tm_mday,tm_hour,tm_min,tm_sec,tm_wday,tm_yday,tm_isdst)
- 方法中未指定时间浮点数/时间结构体时，默认当前时间

```py
import time

# 时间浮点数（如：1530495527.6279528）
time.time()

# 时间结构体（time.struct_time）
time.localtime([时间浮点数])

# 标准格式时间字符串'星期 月 日 时:分:秒 年'（如：'Mon Jul  2 09:39:41 2018'）
time.asctime([时间结构体])

# 格式化后的时间字符串（如：'2018-07-02 09:41:34'）
time.strftime('%Y-%m-%d %H:%M:%S'[, 时间结构体])

# 格式化后的时间字符串（如：'Mon Jul 02 09:43:17 2018'）
time.strftime('%a %b %d %H:%M:%S %Y'[, 时间结构体])

# 符合指定格式的时间字符串转成时间结构体（time.struct_time）
time.strptime('Mon Jul 02 09:43:17 2018', '%a %b %d %H:%M:%S %Y')

# 时间结构体对应的时间浮点数（如：1530495797.0）
time.mktime(time.strptime('Mon Jul 02 09:43:17 2018', '%a %b %d %H:%M:%S %Y'))

# 休眠（秒）
time.sleep(5)
```

## 日期（`datetime`）

```py
from datetime import datetime

# 同 time.strptime()
datetime.strptime('5/30/2018 17:30:00', '%m/%d/%Y %H:%M:%S')
```

## 日历（`calendar`）

```py
import calendar

# 返回带换行符和占位符的日历字符串
calendar.month(2018, 7)

# 显示日历
print(calendar.month(2018, 7))
```