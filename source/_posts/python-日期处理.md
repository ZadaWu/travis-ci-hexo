---
title: python 日期处理
date: 2018-12-24 16:07:21
tags: python
---
作为一个python新手，我真的记不住，因此纪录夏利

import datetime
import time

current_date = datetime.date.today().replace(day=1)
previous_date = (current_date - datetime.timedelta(1)).replace(day=1)
current_date_time_stamp = int(time.mktime(current_date.timetuple())) # 当月第一天的时间戳
previous_date_time_stamp = int(time.mktime(previous_date.timetuple())) # 前月第一天的时间戳
print(current_date, previous_date, current_date_time_stamp, previous_date_time_stamp)

