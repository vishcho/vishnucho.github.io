---
title: "達達特攻聖誕三次大獎?　歐皇都抽六次的！"
date: "2022-12-24"
categories:
 - "遊戲分析"
tags:
 - "game"
 - "math"
 - "survivor.io"
toc: true
---

# 達達特攻聖誕三次大獎?　歐皇都抽六次的！
## 遊戲規則
- 5x5賓果連線遊戲,共25格可以抽
- 三連線就會刷新盤面,共11條連線

![](https://i.imgur.com/dgYZACk.png)
<!--more-->

## 1000萬次模擬結果
連線數|次數|機率
---|---|---
三連線|7882826|78.83%
四連線|1943527|24.66%
五連線|168610|8.68%
六連線|5037|2.99%
總和|10000000|100%


大獎分布|出現分布
---|---
直線大獎(5,11)|8.40%	
斜線大獎(0~4 6~10)|8.03%


## 盤面定義
bingo|column0|column1|column2|column3|column4|bonus
---|---|---|---|---|---|---
row0|0,0|0,1|0,2|0,3|0,4|bonus0
row1|1,0|1,1|1,2|1,3|1,4|bonus1
row2|2,0|2,1|2,2|2,3|2,4|bonus2
row3|3,0|3,1|3,2|3,3|3,4|bonus3
row4|4,0|4,1|4,2|4,3|4,4|bonus4
bonus5|bonus6|bonus7|bonus8|bonus9|bonus10|bonus11

> 數學不會騙人，他它就是不會
## 模擬程式碼分享
```golang
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {

	rand.Seed(time.Now().Unix())
	measure_time := 10000000

	hitMap := make(map[int]int)
	hitCountMap := make(map[int]int)
	for i := 0; i < measure_time; i++ {
		b := NewBingo()

		for {
			bonus := b.Roll()
			if len(bonus) >= 3 {
				hitCountMap[len(bonus)]++
				for _, b := range bonus {
					hitMap[b]++
				}
				break
			}
		}
	}
	fmt.Println(hitCountMap)
	fmt.Println(hitMap)

}

type Bingo struct {
	board [5][5]int
}

func NewBingo() *Bingo {
	return new(Bingo)
}

func (b *Bingo) Roll() []int {

	for {
		lucky := rand.Intn(25)
		x := lucky / 5
		y := lucky % 5
		if b.board[x][y] == 0 {
			b.Mark(x, y, 1)
			return b.Check()
		}
	}
}

func (b *Bingo) Mark(x, y, marker int) {
	b.board[x][y] = marker
}

func (b *Bingo) Check() []int {
	ans := make([]int, 0, 11)
	for row := 0; row < 5; row++ {
		hit := func() bool {
			for c := 0; c < 5; c++ {
				if b.board[row][c] == 0 {
					return false
				}
			}
			return true
		}()
		if hit {
			ans = append(ans, row)
		}
	}

	for column := 0; column < 5; column++ {
		hit := func() bool {
			for r := 0; r < 5; r++ {
				if b.board[r][column] == 0 {
					return false
				}
			}
			return true
		}()
		if hit {
			ans = append(ans, column+6)
		}
	}

	if b.board[0][4]*b.board[1][3]*b.board[2][2]*b.board[3][1]*b.board[4][0] == 1 {
		ans = append(ans, 5)
	}

	if b.board[0][0]*b.board[1][1]*b.board[2][2]*b.board[3][3]*b.board[4][4] == 1 {
		ans = append(ans, 11)
	}

	return ans
}

```