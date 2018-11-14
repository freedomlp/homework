# 自顶向下，逐步求精
自顶向下设计是一种分析问题的方法，可以被应用在面向过程的编程中。简单的说，自顶向下就是将一个大问题先分解为若干个小问题，在将每个小问题继续分解，直到不能再分解或者可以轻易实现为止。应用在计算机领域的编程过程中，则是将主程序分为若干个模块，实现了这些模块，就可以实现整个程序，然后再用同样的方法对待每一个模块，这样，实现每一个小模块就意味着实现最终的大模块。

# 洗衣机
首先将洗衣分为以下**七个步骤**：

1、注水（添加洗衣液）

2、浸泡

3、洗衣

4、换水

5、二次洗衣

6、出水

7、甩干

---

然后**分而治之**

**注水**
```
water_in_switch(open)
get_water_volume
IF 水位达到设置高度 THEN
	water_in_switch(close)
ENDIF
```
**浸泡**
```
time_counter()
IF 达到设置时间 THEN
	准备洗衣
ENDIF
```
**洗衣**
```
motor_run(left)
motor_run(right)
time_counter()
IF	达到预设时间 THEN
	motor_run(stop)
ENDIF
```
**换水**
```
water_out_switch(open)
water_out_switch(close)
water_in_switch(open)
get_water_volume
IF 水位达到设置高度 THEN
	water_in_switch(close)
ENDIF
```
**二次洗衣**
```
motor_run(left)
motor_run(right)
time_counter()
IF	达到预设时间 THEN
	motor_run(stop)
ENDIF
```
**出水**
```
water_out_switch(open)
water_out_switch(close)
```
**甩干**
```
motor_run(left)
motor_run(right)
time_counter()
IF	达到预设时间 THEN
	motor_run(stop)
ENDIF
halt(returncode)
```

