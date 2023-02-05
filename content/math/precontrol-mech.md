---
title: "遊戲期望RTP動態調整 - 事前控制 preControl"
date: "2022-12-07"
categories:
 - "math"
tags:
 - "math"
 - "game"
 - "rtp"
toc: true
---
# 遊戲期望RTP動態調整 - 事前控制 precontrol

設計原生遊戲時, RTP與HitRate要足夠高  
在玩遊戲的時候, 根據期望RTP事先骰出此局要玩原生遊戲或必不中獎遊戲  
RTP可動態範圍 [0,basisRTP]

{{< mermaid >}}
graph LR
A["指定某個expectRTP"]--"有expectRTP/basisRTP機率"--->B("原生遊戲 RTP=basisRTP")
A--"有1-expectRTP/basisRTP機率"-->C["必不中遊戲 RTP=0"]
{{< /mermaid >}}

<!--more-->

## 原理闡述
- 原生遊戲觸發機率= expectRTP/basisRTP
	- 原生遊戲觸發機率 玩 原生遊戲(basis Game)
	- (1-原生遊戲觸發機率) 玩 必不中獎遊戲(Nohit Game)
- 期望遊戲的中獎率 為 原生遊戲的expectRTP/basisRTP倍
- 期望遊戲的進入免費遊戲機率 為 原生遊戲的expectRTP/basisRTP倍
- 期望遊戲的進入免費遊戲頻率 為 原生遊戲的basisRTP/expectRTP倍

## 例子
一個原生遊戲其根據滾輪表與玩法有下列性質
- 主遊戲RTP = basisBaseGameRTP = 140%
- 主遊戲中獎率 = basisHitRate = 40%
- 進入免費遊戲頻率 = basisEnterFGFrequecy = 200
- 免費遊戲進入一次可獲得倍數 = basisFreeGameOnceRatio = 50
- 原生RTP = basisRTP = 主遊戲RTP + 免費遊戲進入一次可獲得倍數/進入免費遊戲頻率
= 1.4+50/200 = 165%

若期望RTP要設定成 96%
- 有58.18%機率 玩 原生遊戲(basis Game)
- 有41.82%機率 玩 必不中獎遊戲(Nohit Game)
- expectHitRate = 23.272%
- basisEnterFGFrequecy = 343.76

## 相關連結
- [遊戲殺率控制理論 Game RTP Control Theory](../rtp_control_theory)
- [遊戲期望RTP動態調整 - 重擲控制 Reroll](../reroll-mech)
- [遊戲期望RTP動態調整 - 事前控制 preControl](../precontrol-mech)