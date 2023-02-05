---
title: "尾牙時,抽100份獎項給40人,竟然三年都有人沒抽到"
date: "2021-03-12"
categories:
 - "math"
tags:
 - "math"
 - "paradox" 
toc: true
---

# 尾牙時,抽100份獎項給40人,竟然三年都有人沒抽到

公司尾牙共計要發出100份獎項，參與抽獎的人數共40人，可重複中獎。有人沒拿到獎項的機率是多少？

## 解題

### 某人都沒中的機率
$(39/40)^{100} \approx 7.951$%

### 40個人裡有人沒中的機率
#### 數學模型
根據數學排容原理：有一個沒中的機率－有兩人沒中的機率＋有三人沒中的機率．．．

$C_1^{40}(39/40)^{100}-C_2^{40}(38/40)^{100}+C_3^{40}(37/40)^{100}...C_{39}^{40}(1/40)^{100} \approx 97.686$%

<!--more-->


#### 模擬模型
根據蒙地卡羅法進行快速估算  $\approx 97.3$%
```golang
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	rand.Seed(time.Now().UnixNano())
	count := 0
	times := 100000
	for i := 0; i < times; i++ {
		if getDev() {
			count++
		}
	}
	fmt.Println(float64(count) / float64(times))
}

func getDev() bool {
	stat := map[int]int{}
	for i := 0; i <= 100; i++ {
		a := rand.Intn(40)
		stat[a]++
	}

	for i := 0; i < 40; i++ {
		if stat[i] == 0 {
			return true
		}
	}
	return false
}

```


## 小評

可以發現有人沒中的機率很高，高達97%，據聞該公司已經連三年都有人沒中！