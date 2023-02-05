---
title: "賠率設計模式"
date: "2022-11-22"
categories:
 - "博彩分析"
tags:
 - "bet"
 - "math"
 - "sportslottery"
toc: true
---

# 賠率設計模式

## 單訊號源
{{< mermaid >}}
graph LR
原始訊號 --> 盈利模組AdjustMargin --> Client
{{< /mermaid >}}

## 多訊號源
`設計重點： 權重分配`

{{< mermaid >}}
graph LR
原始訊號A --> 盈利模組AdjustMargin --> 同利潤之訊號A --權重A-->權重計算器
原始訊號B --> 盈利模組AdjustMargin --> 同利潤之訊號B --權重B-->權重計算器
原始訊號C --> 盈利模組AdjustMargin --> 同利潤之訊號C --權重C-->權重計算器--> Client
{{< /mermaid >}}

<!--more-->

## 考量目前注單之動態調整賠率機制

```
設計重點： 要使下注越平均越佳
若此選項下注越少，增加其賠率吸引賭客下注
若此選項下注越多，降低其賠率阻卻賭客下注
```

細節請參照 [運彩動態調整賠率機制](dynamic_bet_adjust.md)


