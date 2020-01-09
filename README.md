# Personal-Bank-Account-Management-Program  
## Abstract  
A simple personal bank account management program
## treasure :  
>>1. 有用的计算时间的类data  
>>> 建立：Date date(2008, 11, 1);	//起始日期  
>>> 显示：date.show()  
>>> 间隔：date.distance(Date(2020, 1, 1));  

### date.h
```cpp
//date.h
#ifndef __DATE_H__
#define __DATE_H__

class Date {	//日期类
private:
	int year;		//年
	int month;		//月
	int day;		//日
	int totalDays;	//该日期是从公元元年1月1日开始的第几天

public:
	Date(int year, int month, int day);	//用年、月、日构造日期
	int getYear() const { return year; }
	int getMonth() const { return month; }
	int getDay() const { return day; }
	int getMaxDay() const;		//获得当月有多少天
	bool isLeapYear() const {	//判断当年是否为闰年
		return year % 4 == 0 && year % 100 != 0 || year % 400 == 0;
	}
	void show() const;			//输出当前日期
	//计算两个日期之间差多少天	
	int distance(const Date& date) const {
		return totalDays - date.totalDays;
	}
};

#endif //__DATE_H__

```

### date.cpp
```cpp
//date.cpp
#include "date.h"
#include <iostream>
#include <cstdlib>
using namespace std;

namespace {	//namespace使下面的定义只在当前文件中有效
	//存储平年中某个月1日之前有多少天，为便于getMaxDay函数的实现，该数组多出一项
	const int DAYS_BEFORE_MONTH[] = { 0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 334, 365 };
}

Date::Date(int year, int month, int day) : year(year), month(month), day(day) {
	if (day <= 0 || day > getMaxDay()) {
		cout << "Invalid date: ";
		show();
		cout << endl;
		exit(1);
	}
	int years = year - 1;
	totalDays = years * 365 + years / 4 - years / 100 + years / 400
		+ DAYS_BEFORE_MONTH[month - 1] + day;
	if (isLeapYear() && month > 2) totalDays++;
}

int Date::getMaxDay() const {
	if (isLeapYear() && month == 2)
		return 29;
	else
		return DAYS_BEFORE_MONTH[month]- DAYS_BEFORE_MONTH[month - 1];
}

void Date::show() const {
	cout << getYear() << "-" << getMonth() << "-" << getDay();
}

```

>>2. 四舍五入的方法    

```cpp

#include <cmath>
amount = floor(amount * 100 + 0.5) / 100;	//保留小数点后两位

```

>>3. 构造函数的执行顺序  
>>> 函数实际调用时，函数原型开始，实参赋值形参，然后形参赋值给参数表中的类的数据成员。  

```cpp
Line::Line( double len): length(len)
{
    cout << "Object is being created, length = " << len << endl;
}

// 等价于下面的写法
Line::Line( double len)
{
    length = len;
    cout << "Object is being created, length = " << len << endl;
}

```
