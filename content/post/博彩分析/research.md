---
title: "彩票技術綜合研究"
date: "2022-11-11"
categories:
 - "bet"
tags:
 - "bet"
 - "math"
 - "sportslottery"
toc: true
---

# 彩票技術綜合研究

## 賠率表示法
項目     | items           | Team A  | Team B  | Draw
-------|-----------------|---------|---------|------
機率     | Probability     | 55%     | 25%     | 20%
小數賠率 | Decimal         | 1.82    | 4.0     | 5.0
分數賠率 | Fractional      | 4/5     | 3/1     | 4/1
美式賠率 | Moneyline       | -122    | 300     | 400
香港賠率 | Hong Kong Odds  | 0.8182  | 3       | 4
印尼賠率 | Indonesian Odds | -1.2222 | 3.0     | 4.0
馬來賠率 | Malay Odds      | 0.8182  | -0.3333 | -0.25

> 本文若無特殊說明，以小數賠率(Decimal)為參考

<!--more-->

## 分類遊戲
根據目標可控性與賠率可變動性

項目|目標可控|目標不可控
---|---|---
固定賠率|森林舞會,百家樂|固定賠率博彩
變動賠率|X|變動賠率博彩

## 目標可控的固定賠率遊戲

### 種類
自行開獎的彩票、百家樂、骰寶、森林舞會...等

### 控制原理
1. 開獎前的下注分布即可計算出此盤開各獎項的返回率
2. 藉由調節出各獎項的機率去開出符合要求的獎項

### 討論
為了玩家體感與實際體驗,需設計一些特殊技巧保證其感受  
且須根據遊戲特色作其開獎的體驗依據  
主要手段有
- 天險機制
- 返回率權重開獎機制
- 獎項太久未開的保底機制
- 人為提高長龍或交錯的體感機制

## 百家樂特殊討論
https://hackmd.io/@squarecho/baccarat




## 固定賠率博彩 Fixed-odds Betting

### 利潤 Margin 

#### 利潤公式
已知賠率計算利潤  
$Margin = \frac{1}{Odd_A}+ \frac{1}{Odd_B}+ \frac{1}{Odd_X}-1$

#### 賠率公式
已知隱含概率計算賠率，利潤可以自由設定  
$Odd_A = \frac{1}{P_A \times (1+Margin)}$  
$Odd_B = \frac{1}{P_B \times (1+Margin)}$  
$Odd_X = \frac{1}{P_X \times (1+Margin)}$  

### 分析與討論
{{< iframe "https://docs.google.com/spreadsheets/d/e/2PACX-1vQyzfjzye4LKdHtYIeO31nPJOi8LOu0tHYxucPhzSHFuZSlP_eLw7sR3ytsV6fh1oDCQvMZoxjUp0V8/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false" 400px 400px >}}


#### 從玩家角度分析
1. 盤口**開出某個賠率**選項組
2. 根據賠率倒數可以算出**帶利潤機率**
3. 同除**帶利潤機率**總額，即一般化後可得**開盤者認定機率**

#### 從盤口角度分析
1. 根據統計數據分析或各種來源，精算**開盤者認定機率**
2. 等量，等比例或根據風險程度計算**利潤量**
3. 每項機率增加**利潤量**，可得帶利潤機率
4. **帶利潤機率**的倒數即為**開出賠率**



## 通贏的研究

### 定義
通贏意味著在此下注分布下,不管結果開出哪個選項,盤口的收益都是正的
### 條件
1. 盤口必須要有**利潤(Margin)** 才有可能有通贏的可能
2. **利潤(Margin)** 越高,其通贏的範圍容忍度越大

### 範例
選項|賠率|下注量|開出該選項的賠付
---|---|---|---
1|3.5|100|5
x|1.95|175|13.75
2|4|80|35

### 計算驗證
$X = \frac{175}{100} = 1.75 \leq \frac{O_1}{O_2} = \frac{3.5}{1.95} = 1.794871795$  
$X = \frac{80}{100} = 0.8 \leq \frac{O_1}{O_3} = \frac{3.5}{4} = 0.875$  


### 兩個選項的通贏公式證明

#### 通贏公式
$O_2\leq \frac{B_1}{B_2} \leq \frac{1}{O_1}$

#### 參數定義
- $O_1=下注1可獲得的小數賠率$
- $O_2=下注2可獲得的小數賠率$
- $B_1=下注1總下注量$
- $B_2=下注2總下注量$

#### 證明過程

$$\begin{align\*}
B_1+B_2-O_1 \times B_1 \geq 0 \ \ \ \ \ \ \ win\ condition(1) \\\\\  
B_1+B_2-O_2 \times B_2 \geq 0 \ \ \ \ \ \ \ win\ condition(2) 
\end{align\*}$$


$$\begin{align\*}
\frac{B_1}{B_2}+1 \geq O_1 \times \frac{B_1}{B_2}  \\\\\  
\frac{B_2}{B_1}+1 \geq O_2 \times \frac{B_2}{B_1}
\end{align\*}$$

$$\begin{align\*}
\frac{B_1}{B_2} &\leq \frac{1}{O_1}\\\\\
\frac{B_2}{B_1} &\leq \frac{1}{O_2} \ \ (3)\\
\end{align\*}$$


$$\begin{align\*}
\because \frac{B_2}{B_1}&>0,(3)\\\\\
\therefore\frac{B_1}{B_2} &\geq O_2
\end{align\*}$$


$$\begin{align\*}O_2\leq \frac{B_1}{B_2} \leq \frac{1}{O_1} \ \  proven\end{align\*}$$


### 三個選項的通贏公式證明

#### 通贏公式
1. 同除其中一個下注量 $(B_1,B_2,B_3) => (1,X,Y)$
2. $X \leq \frac{O_1}{O_2}$
3. $Y \leq \frac{O_1}{O_3}$


#### 參數定義
- $O_1=下注1可獲得的小數賠率$
- $O_2=下注2可獲得的小數賠率$
- $O_3=下注3可獲得的小數賠率$
- $B_1=下注1總下注量$
- $B_2=下注2總下注量$
- $B_3=下注3總下注量$
- $X=\frac{B_2}{B_1}下注2與1總下注量比值$
- $Y=\frac{B_3}{B_1}下注3與1總下注量比值$

#### 證明過程
$$\begin{align\*}
B_1+B_2+B_3-O_1 \times B_1 &\geq 0 \  \ \ win\ condition(1) \\\\
B_1+B_2+B_3-O_2 \times B_2 &\geq 0 \  \ \ win\ condition(2) \\\\
B_1+B_2+B_3-O_3 \times B_3 &\geq 0 \  \ \ win\ condition(3) \\
\end{align\*}$$

$$\begin{align\*}
1+X+Y&-O_1 &\geq 0 \ \  (4)  \\\\
1+X+Y&-O_2 \times X &\geq 0 \  \ (5)\ \\\\
1+X+Y&-O_3 \times Y &\geq 0 \  \ (6)\ \\
\end{align\*}$$


$$\begin{align\*}
\because (4)  \therefore  x \geq O_1-y-1 \ \ (7)
\end{align\*}$$

$$\begin{align\*}
\because (6)(7)  \therefore  O_1-O_3 \times Y \geq 0\\\\
then \ \ \  Y \leq \frac{O_1}{O_3} \ \ proven \\\\ 
Similarly, \ \ \  Y \leq \frac{O_1}{O_2} \ \ proven
\end{align\*}$$



### N個選項的通贏公式證明

#### 通贏公式
1. 同除其中一個下注量 $(B_1,B_2,...,B_n) => (1,X_2,..,X_n)$
2. $X_2 \leq \frac{O_1}{O_2}$
3. $X_3 \leq \frac{O_1}{O_3}$
4. $...$
5. $X_n \leq \frac{O_1}{O_n}$


#### 參數定義
- $O_i=下注i可獲得的小數賠率$
- $B_i=下注i總下注量$
- $X_i=\frac{B_i}{B_1}下注i與1總下注量比值$

#### 證明方式
1. 根據數學歸納法證明
2. 根據一般化原則證明



## 固定利潤賠率調整公式

### 兩個選項
#### 公式
$Odd_B = \frac{1}{Margin+1-\frac{1}{Odd_A}}$
#### 證明
$\because\ 利潤公式:\ \frac{1}{Odd_{A}}+\frac{1}{Odd_{B}} = Margin$
移項整理後可得$Odd_B = \frac{1}{Margin+1-\frac{1}{Odd_A}} \ \  proven$


## 控盤損益表展示

根據已有的所有注單，統計後得出開出不同選項時的總損益。
下表為兩種選項時的損益表
{{< iframe "https://docs.google.com/spreadsheets/d/e/2PACX-1vQyzfjzye4LKdHtYIeO31nPJOi8LOu0tHYxucPhzSHFuZSlP_eLw7sR3ytsV6fh1oDCQvMZoxjUp0V8/pubhtml?gid=1446200542&amp;single=true&amp;widget=true&amp;headers=false" 800px 500px >}}


## 控盤+對沖盤損益表展示

根據已有的所有注單加上對沖的注單，統計後得出開出不同選項時的總損益。
下表為兩種選項時的損益表

{{< iframe "https://docs.google.com/spreadsheets/d/e/2PACX-1vQyzfjzye4LKdHtYIeO31nPJOi8LOu0tHYxucPhzSHFuZSlP_eLw7sR3ytsV6fh1oDCQvMZoxjUp0V8/pubhtml?gid=2082504842&amp;single=true&amp;widget=true&amp;headers=false" 1024px 500px >}}



## 同一項目多個盤口分析(待完成)



## 同一項目不同讓分的賠率分析(待完成)

