---
title: "Golang 技術懶人包"
date: 2025-06-01T11:30:03+00:00
# weight: 1
# aliases: ["/first"]
# tags: ["first"]
author: "Vish"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: true
draft: false
hidemeta: false
comments: false
description: "常用連結整理與社群分享"
canonicalURL: "https://www.forevergame.org/golang"
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: false
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: true
UseHugoToc: true
images: ["https://www.forevergame.org/images/golang_cover.png"]
cover:
  image: "/images/golang_cover.png" # image path/url
  alt: "" # alt text
  caption: "" # display caption under cover
  relative: false # when using page bundles set this to true
  hidden: true # only hide on current single page
editPost:
  URL: "https://github.com/vishcho/vishnucho.github.io/edit/main/content"
  Text: "edit" # edit text
  appendFilePath: true # to append file path to Edit link
---

以下懶人包依「學習階段 ➜ 範例實作 ➜ 進階深讀 ➜ 中文資源 ➜ 社群互動 ➜ 影音教學」六大區塊整理。建議先從官方文件快速破冰，再搭配範例與練習鞏固概念，最後用部落格與設計模式補強實務經驗。

---

## 1. 入門必讀（官方文件）

| 資源                  | 說明                                                                                             |
| --------------------- | ------------------------------------------------------------------------------------------------ |
| **A Tour of Go**      | 互動式導覽，邊看邊執行程式碼，3 – 4 小時可完成。<https://go.dev/tour/>                           |
| **Effective Go**      | 官方「寫出慣用 Go」指南，涵蓋命名、錯誤處理、併發等最佳實踐。<https://go.dev/doc/effective_go>   |
| **Generics Tutorial** | 官方範例講解泛型語法與型別推論，Go 1.22 後先看這篇最省力。<https://go.dev/doc/tutorial/generics> |
| **Go Playground**     | 雲端沙盒，隨貼即編譯執行，並可分享連結。<https://go.dev/play/>                                   |

---

## 2. 範例導向教學

| 資源                | 說明                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------- |
| **Go by Example**   | 以「最小可執行程式」展示語法，讀一段貼一段動手改。<https://gobyexample.com/>          |
| **Go Web Examples** | Router、Middleware、WebSocket 等 Web 專題範例。<https://gowebexamples.com/>           |
| **Gophercises**     | 20+ 實戰練習（CLI 工具、照片轉檔、URL 短縮…），附講解影片。<https://gophercises.com/> |

---

## 3. 練習平台 & 專案模板

| 資源                           | 說明                                                                                               |
| ------------------------------ | -------------------------------------------------------------------------------------------------- |
| **Exercism Go Track**          | 140+ 題目，免費真人導師 code review。<https://exercism.org/tracks/go>                              |
| **Standard Go Project Layout** | 社群共識的專案目錄結構範本，避免「每人一套」。<https://github.com/golang-standards/project-layout> |

---

## 4. 進階閱讀 & 實務心得

| 資源                    | 說明                                                                   |
| ----------------------- | ---------------------------------------------------------------------- |
| **Dave Cheney Blog**    | 資深 Gopher 的效能、併發、測試深度文章。<https://dave.cheney.net/>     |
| **Gopher Academy Blog** | 年度 Advent Calendar 與 Go 社群專欄。<https://blog.gopheracademy.com/> |
| **Go Patterns**         | GitHub 精選設計模式範例與說明。<https://github.com/tmrts/go-patterns>  |

---

## 5. 中文資源

| 資源                        | 說明                                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------------------- |
| **Go 語言中文網**           | 官方文件與標準庫中文化、討論區。<https://studygolang.com/>                                        |
| **awesome-golang-cn**       | GitHub 蒐羅中文書籍／文章／投影片索引。<https://github.com/wolfhong/awesome-golang-cn>            |
| **《Go 入門指南》中文翻譯** | 《The Way to Go》開源中文版，適合零基礎循序閱讀。<https://github.com/unknwon/the-way-to-go_ZH_CN> |

---

## 6. 社群互動 & 問答

| 資源                | 說明                                                                                                  |
| ------------------- | ----------------------------------------------------------------------------------------------------- |
| **Go Forum**        | 官方 Discourse 論壇，適合貼程式碼求助。<https://forum.golangbridge.org/>                              |
| **Gopher Slack**    | 10 萬+ 開發者即時討論，頻道多元（#beginner、#performance…）。<https://invite.slack.golangbridge.org/> |
| **Reddit r/golang** | 社群新聞與實務問答，追蹤新版本動態。<https://www.reddit.com/r/golang/>                                |

---

## 7. 影音教學

| 資源                                | 說明                                                                                                                          |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **JustForFunc – Programming in Go** | 前 Google 開發者 Francesc Campoy 的 YouTube 頻道，深入淺出講解模組、併發、測試等主題。<https://www.youtube.com/c/justforfunc> |

---

### 建議學習路線

1. **官方 Tour → Effective Go → Generics**
2. **Go by Example / Gophercises** 交替練習，遇到問題就上 **Playground** 或 **Exercism**。
3. 扎實後再閱讀 **Dave Cheney Blog**、**Go Patterns**，同步參與 **Slack / Forum** 交流。
4. 若想用中文補強，可對照 **Go 語言中文網** 與 **《Go 入門指南》**，減少語言障礙。

> 以上資源皆免費且長期維護，收藏後即可離線慢慢研讀。祝學習順利，早日寫出又快又乾淨的 Go 程式！

## 社群連結

**入群請回答此二十五個關鍵字之一**

```golang
break/case/chan/const/continue/
default/defer/else/fallthrough/
for/func/go/goto/if/import/
interface/map/package/range/
return/select/struct/switch/type/var
```

[Line 社群 Golang 技術分享 <- 請點我](https://line.me/ti/g2/87Affh8Js_Zh2-1-2ZeK_4Qck-5H0iCoyymbIw?utm_source=invitation&utm_medium=link_copy&utm_campaign=default)

![Line 社群 Golang 技術分享](/images/golang_line.jpg)
