# Calendar



```python
import calendar
```

#### 基本calendar操作

```python
#将星期日设置为一周的第一天
calendar.setfirstweekday(firstweekday=6)
```

```python
# 判断是否是闰年
print(calendar.isleap(2018))
```

```text
False
```

```python
# 显示两年之间的闰年数量
print(calendar.leapdays(2008,2011))
```

```text
1
```

```python
# 返回一个月中的天数列表，按周划分
print(calendar.monthcalendar(2018,8))
```

```text
[[0, 0, 0, 1, 2, 3, 4], [5, 6, 7, 8, 9, 10, 11], [12, 13, 14, 15, 16, 17, 18], [19, 20, 21, 22, 23, 24, 25], [26, 27, 28, 29, 30, 31, 0]]
```

```python
# 打印一个月的日历
calendar.prmonth(2018,8)
```

```text
    August 2018
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31
```

```python
# 打印一年的日历
calendar.prcal(2018, m=4)
```

```text
                                               2018

      January                   February                   March                     April
Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6                   1  2  3                   1  2  3       1  2  3  4  5  6  7
 7  8  9 10 11 12 13       4  5  6  7  8  9 10       4  5  6  7  8  9 10       8  9 10 11 12 13 14
14 15 16 17 18 19 20      11 12 13 14 15 16 17      11 12 13 14 15 16 17      15 16 17 18 19 20 21
21 22 23 24 25 26 27      18 19 20 21 22 23 24      18 19 20 21 22 23 24      22 23 24 25 26 27 28
28 29 30 31               25 26 27 28               25 26 27 28 29 30 31      29 30

        May                       June                      July                     August
Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa
       1  2  3  4  5                      1  2       1  2  3  4  5  6  7                1  2  3  4
 6  7  8  9 10 11 12       3  4  5  6  7  8  9       8  9 10 11 12 13 14       5  6  7  8  9 10 11
13 14 15 16 17 18 19      10 11 12 13 14 15 16      15 16 17 18 19 20 21      12 13 14 15 16 17 18
20 21 22 23 24 25 26      17 18 19 20 21 22 23      22 23 24 25 26 27 28      19 20 21 22 23 24 25
27 28 29 30 31            24 25 26 27 28 29 30      29 30 31                  26 27 28 29 30 31

     September                  October                   November                  December
Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa      Su Mo Tu We Th Fr Sa
                   1          1  2  3  4  5  6                   1  2  3                         1
 2  3  4  5  6  7  8       7  8  9 10 11 12 13       4  5  6  7  8  9 10       2  3  4  5  6  7  8
 9 10 11 12 13 14 15      14 15 16 17 18 19 20      11 12 13 14 15 16 17       9 10 11 12 13 14 15
16 17 18 19 20 21 22      21 22 23 24 25 26 27      18 19 20 21 22 23 24      16 17 18 19 20 21 22
23 24 25 26 27 28 29      28 29 30 31               25 26 27 28 29 30         23 24 25 26 27 28 29
30                                                                            30 31
```

```python
from calendar import Calendar
```

```python
# 返回一周的数字的迭代器
c = Calendar()
print(list(c.iterweekdays()))
```

```text
[0, 1, 2, 3, 4, 5, 6]
```

```python
from calendar import TextCalendar
```

```python
tc = TextCalendar()
```

```python
print(tc.formatmonth(2019,10))
```

```text
    October 2019
Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
```

```python
print(tc.prmonth(2019,10))
```

```text
    October 2019
Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
None
```

```python
print(tc.formatyear(2019))
```

```text
                                  2019

      January                   February                   March
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6                   1  2  3                   1  2  3
 7  8  9 10 11 12 13       4  5  6  7  8  9 10       4  5  6  7  8  9 10
14 15 16 17 18 19 20      11 12 13 14 15 16 17      11 12 13 14 15 16 17
21 22 23 24 25 26 27      18 19 20 21 22 23 24      18 19 20 21 22 23 24
28 29 30 31               25 26 27 28               25 26 27 28 29 30 31

       April                      May                       June
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7             1  2  3  4  5                      1  2
 8  9 10 11 12 13 14       6  7  8  9 10 11 12       3  4  5  6  7  8  9
15 16 17 18 19 20 21      13 14 15 16 17 18 19      10 11 12 13 14 15 16
22 23 24 25 26 27 28      20 21 22 23 24 25 26      17 18 19 20 21 22 23
29 30                     27 28 29 30 31            24 25 26 27 28 29 30

        July                     August                  September
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7                1  2  3  4                         1
 8  9 10 11 12 13 14       5  6  7  8  9 10 11       2  3  4  5  6  7  8
15 16 17 18 19 20 21      12 13 14 15 16 17 18       9 10 11 12 13 14 15
22 23 24 25 26 27 28      19 20 21 22 23 24 25      16 17 18 19 20 21 22
29 30 31                  26 27 28 29 30 31         23 24 25 26 27 28 29
                                                    30

      October                   November                  December
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6                   1  2  3                         1
 7  8  9 10 11 12 13       4  5  6  7  8  9 10       2  3  4  5  6  7  8
14 15 16 17 18 19 20      11 12 13 14 15 16 17       9 10 11 12 13 14 15
21 22 23 24 25 26 27      18 19 20 21 22 23 24      16 17 18 19 20 21 22
28 29 30 31               25 26 27 28 29 30         23 24 25 26 27 28 29
                                                    30 31
```

