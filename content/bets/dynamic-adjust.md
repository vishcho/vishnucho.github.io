---
title: "彩票動態調整賠率機制"
date: "2022-11-21"
categories:
 - "博彩分析"
tags:
 - "bet"
 - "math"
 - "sportslottery"
toc: true
---
# 彩票動態調整賠率機制



## 賠率操作機制
狀態|描述
---|---
手動狀態|由操盤手控管，完全不觸發風險控管。
自動狀態|忽略操盤手的控制。

## 手動狀態

{{< mermaid >}}
graph LR
原始訊號 -->  盈利模組AdjustMargin --> 操盤手控管 --> Client
{{< /mermaid >}}
## 自動狀態


- 原始訊號賠率異動
- 新增注單導致風險異動


{{< mermaid >}}
graph LR
原始訊號或新增注單 --> 風險控管AdjustRisk --> A{賠率調整大小}--"不超過調整百分比"--> 盈利模組AdjustMargin --> Client
A{賠率調整大小}--"超過調整百分比"-->排程器--"第1週期"--> 盈利模組AdjustMargin
排程器--"第2週期"--> 盈利模組AdjustMargin
排程器--"第3週期"--> 盈利模組AdjustMargin
排程器--"..."--> 盈利模組AdjustMargin
{{< /mermaid >}}

<!--more-->

### 操作參數
參數名稱|命名|描述
---|---|---
天險|maxCompensation| 該選項的風險超過天險值就封掉這個選項。
控制門檻|Threshold|低於控制門檻的選項不控制，數值越小控制力越強。
上調百分比|UpperRatio|最多不能超過百分比，達到這個百分比就停止上調。
下降百分比|LowerRatio|最多不能低於百分比，達到這個百分比就停止下降。
賠率調整周期|ChangeDuration|時間多久跳一次
賠率調整百分比|ChangePrecentage|每次跳的百分比。
控制函式|ControlFunction|線形、平方、指數、對數函式，預設：風險對賠率調整率為平方根反比


### 自動狀態基本設定
- 跳到一半遇到訊號修改賠率，從訊號源給的賠率從新開始處理。
- 假設賽事剩下十秒，調整需要 30 秒才能達到，也不需要真的調整到定位，賽事應該結束就直接結束。
- 自動跟手動互切的時候，先不考慮變動太大的問題。

### 情境討論

{{< iframe "https://docs.google.com/spreadsheets/d/e/2PACX-1vQyzfjzye4LKdHtYIeO31nPJOi8LOu0tHYxucPhzSHFuZSlP_eLw7sR3ytsV6fh1oDCQvMZoxjUp0V8/pubhtml?gid=1722496610&amp;single=true&amp;widget=true&amp;headers=false" 800px 500px >}}





## 風險定義 Risk
Risk_A: 開這個選項(A)系統的虧損    
開A所要賠付的金額 - 此盤口的所有下注收入   
風險>0表示系統虧錢, 風險<0表示系統賺錢    

### 考慮一盤口 A勝 2.85 B勝 1.25
### 僅有A下注
項目|A|B
---|---|---
賠率|2.85|1.25
下注量|100|0
風險量|-185|100

### 僅有B下注
項目|A|B
---|---|---
賠率|2.85|1.25
下注量|0|100
風險量|100|-25

### 一致下注
項目|A|B
---|---|---
賠率|2.85|1.25
下注量|100|100
風險量|-85|75

### 平均下注
項目|A|B
---|---|---
賠率|2.85|1.25
下注量|125|285
風險量|53.75|53.75


### 小結
- 越平均下注對系統越有利
- 與賠率反比下注為最佳情況