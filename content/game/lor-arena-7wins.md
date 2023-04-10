---
title: "LoR遠征 - 雙淘汰賽制分析"
date: 2021-03-15
categories:
 - "遊戲分析"
tags:
 - "math"
 - "game"
toc: true
---

# LoR遠征 - 雙淘汰賽制分析

![lor-arena-7wins](/post/遊戲分析/imgs/lor-arena-7wins.jpg "LoR遠征展示")

## 規則

1. 七勝出場  
2. 連續兩敗出場  
3. 挑戰第七勝時僅有一次敗局機會  
4. 每枚代幣共可參加兩場  
5. 兩場中成績較優者為獎勵發放條件  

## 隱含條件
實力表示每一局勝利的概率(期望勝率)  

## 命題
求實力要多高才能有一半的機率用一枚代幣獲得七勝獎勵

<!--more-->
## 解題

### 每場可能性
```
敗敗:0勝
敗勝敗敗:1勝    
敗勝敗勝敗敗:2勝
敗勝敗勝敗勝敗敗:3勝
敗勝敗勝敗勝敗勝敗敗:4勝
敗勝敗勝敗勝敗勝敗勝敗敗:5勝
敗勝敗勝敗勝敗勝敗勝敗勝敗:6勝
敗勝敗勝敗勝敗勝敗勝敗勝勝:7勝
...
勝勝勝勝勝勝勝:7勝
```

### 機率公式
$$ \begin{align}
P_{win0}&=(1-p)^2 \cr
P _ {winN} &= \sum _ {i=0} ^ n C _ i^n p^n \times (1-p) ^ {2+i} \cr
P _ {win6} &= \sum _ {i=0} ^ 6 C _ i^6 p^6 \times (1-p) ^ {1+i} \cr
P _ {win7} &= \sum _ {i=0} ^ 6 C _ i^6 p^7 \times(1-p) ^ {i}
\end{align} $$

### 數學模型展示
| 勝率 | 0勝   | 1勝   | 2勝   | 3勝   | 4勝  | 5勝  | 6勝   | 7勝   |
|------|-------|-------|-------|-------|------|------|-------|-------|
| 10%  | 81.0% | 15.4% | 2.9%  | 0.6%  | 0.1% | 0.0% | 0.0%  | 0.0%  |
| 20%  | 64.0% | 23.0% | 8.3%  | 3.0%  | 1.1% | 0.4% | 0.2%  | 0.0%  |
| 30%  | 49.0% | 25.0% | 12.7% | 6.5%  | 3.3% | 1.7% | 1.2%  | 0.5%  |
| 40%  | 36.0% | 23.0% | 14.7% | 9.4%  | 6.0% | 3.9% | 4.1%  | 2.7%  |
| 50%  | 25.0% | 18.8% | 14.1% | 10.5% | 7.9% | 5.9% | 8.9%  | 8.9%  |
| 60%  | 16.0% | 13.4% | 11.3% | 9.5%  | 8.0% | 6.7% | 14.1% | 21.1% |
| 70%  | 9.0%  | 8.2%  | 7.5%  | 6.8%  | 6.2% | 5.6% | 17.0% | 39.8% |
| 80%  | 4.0%  | 3.8%  | 3.7%  | 3.5%  | 3.4% | 3.3% | 15.7% | 62.6% |
| 90%  | 1.0%  | 1.0%  | 1.0%  | 1.0%  | 1.0% | 1.0% | 9.4%  | 84.7% |

### 模擬模型

```go
func getWinProbability(p float64, n int) float64 {
	if n == 0 {
		return (1 - p) * (1 - p)
	}
	ans := 0.0
	if n == 6 {
		for i := 0; i <= 6; i++ {
			ans += float64(combin.Binomial(6, i)) * math.Pow(p, float64(6)) * math.Pow(1-p, float64(1+i))
		}
		return ans
	}
	if n == 7 {
		for i := 0; i <= 6; i++ {
			ans += float64(combin.Binomial(6, i)) * math.Pow(p, float64(7)) * math.Pow(1-p, float64(i))
		}
		return ans
	}
	for i := 0; i <= n; i++ {
		ans += float64(combin.Binomial(n, i)) * math.Pow(p, float64(n)) * math.Pow(1-p, float64(2+i))
	}
	return ans
}
```

### 兩場擇優效應
\\begin{align}
P^\*_0&=P_0^2 \cr
P^\*_1&=P_1^2+2\times P_1\times P_0 \cr
P^\*_2&=P_2^2+2\times P_2\times (P_0+P_1) \cr 
P^\*_n&=P_n^2+2\times P_n\times \sum _ {i=0} ^ {n-1} (P_i) \cr 
P^\*_7&=1-(1-P_7)^2
\\end{align}

勝率 | 0勝   | 1勝   | 2勝   | 3勝   | 4勝   | 5勝  | 6勝   | 7勝
-----|-------|-------|-------|-------|-------|------|-------|------
10%  | 65.6% | 27.3% | 5.7%  | 1.1%  | 0.2%  | 0.0% | 0.0%  | 0.0%
20%  | 41.0% | 34.8% | 15.1% | 5.8%  | 2.1%  | 0.8% | 0.3%  | 0.1%
30%  | 24.0% | 30.7% | 20.5% | 11.7% | 6.3%  | 3.3% | 2.4%  | 1.1%
40%  | 13.0% | 21.9% | 19.6% | 14.8% | 10.4% | 7.1% | 7.8%  | 5.4%
50%  | 6.2%  | 12.9% | 14.3% | 13.3% | 11.4% | 9.4% | 15.4% | 17.0%
60%  | 2.6%  | 6.1%  | 7.9%  | 8.6%  | 8.6%  | 8.2% | 20.2% | 37.7%
70%  | 0.8%  | 2.1%  | 3.1%  | 3.8%  | 4.3%  | 4.5% | 17.6% | 63.7%
80%  | 0.2%  | 0.5%  | 0.7%  | 0.9%  | 1.1%  | 1.3% | 9.3%  | 86.0%
90%  | 0.0%  | 0.0%  | 0.0%  | 0.1%  | 0.1%  | 0.1% | 2.0%  | 97.7%


## 小結
實力(勝率)需要接近七成,在兩次的機會裡面拿到七勝的機率超過一半

> 能把握的只有自己的實力，其他都浮雲