---
title: "遊戲槓桿規則 Leverage Rule"
date: "2022-06-06"
categories:
 - " 數學分析"
tags:
 - "math"
 - "game"
toc: true
---

# 遊戲槓桿規則 Leverage Rule
包含**以小博大**與**不夠賠**的計算分析  

## 天條
* 以小博大-每個人最多贏本身攜帶的金額  
* 不夠賠-每個人最多輸本身攜帶的金額  

## 一般化(複數玩家贏錢且複數玩家輸錢)

### 實作邏輯 
總輸分 = 所有觸發不夠賠的輸家攜帶金額 + 正常輸家輸的金額  
總贏分 = 所有觸發以小搏大的贏家攜帶金額 + 正常贏家贏的金額  
<!--more-->
#### 如果總輸分>總贏分:
每個輸家輸掉的金額等比例減少(少輸一些)  
輸掉的金額若是有小數無條件**進位**成整數  


#### 如果總輸分<總贏分:
每個贏家贏得的金額等比例減少(少贏一些)  
贏取的金額若是有小數無條件**捨去**成整數  

### 程式碼分享
```go
// CalLeverage 計算槓桿
// @param profit []int 槓桿前的收益
// @param balance []int 收益前的餘額
// @return afterProfit []int 槓桿前的收益
func CalLeverage(profit []int, balance []int) []int {
	if len(profit) != len(balance) {
		return profit
	}
	afterProfit := make([]int, len(profit))
	copy(afterProfit, profit)
	loser := []int{}
	winner := []int{}
	// 計算輸贏家
	for i, p := range profit {
		if p < 0 {
			loser = append(loser, i)
		}
		if p > 0 {
			winner = append(winner, i)
		}
	}
	// 所有輸分
	allLose := 0
	for _, i := range loser {
		if balance[i]+profit[i] < 0 {
			allLose += balance[i]
			afterProfit[i] = balance[i] * -1
		} else {
			allLose -= profit[i]
		}
	}
	// 所有贏分
	allWin := 0
	for _, i := range winner {
		if profit[i] >= balance[i] {
			afterProfit[i] = balance[i]
			allWin += balance[i]
		} else {
			allWin += profit[i]
		}
	}

	// 如果所有輸分大於所有贏分
	if allLose > allWin {
		ratio := float64(allWin) / float64(allLose)
		for _, i := range loser {
			afterProfit[i] = int(math.Floor(float64(afterProfit[i]) * ratio))
		}
	}
	// 如果所有贏分大於所有輸分
	if allWin > allLose {
		ratio := float64(allLose) / float64(allWin)
		for _, i := range winner {
			afterProfit[i] = int(math.Ceil(float64(afterProfit[i]) * ratio))
		}
	}

	return afterProfit
}

```