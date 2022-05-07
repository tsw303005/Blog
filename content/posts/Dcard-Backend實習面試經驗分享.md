---
title: "Dcard Backend實習面試經驗分享"
date: 2022-04-20T19:50:29+08:00
draft: true
author: "Ivan"
description: "Dcard Backend intern 的面試心得"
readingTime: "Three-minute"
type: "post"
tags:
    - Dcard
    - interview
    - intern
    - 面試
    - 實習
summary: "分享 2022 Dcard backend intern 的面試心得"
keywords:
    - Dcard
    - interview
    - intern
    - 面試
    - 實習
---

## 前言
&ensp;&ensp;這是我面試 2022 Dcard backend intern 所被問到的題目跟得到的心得，但是很遺憾的這個實習我在中途就被刷掉，所以一直很猶豫到底要不要寫這一篇 blog，最後想想還是分享一下關於這次面試中我發現自己哪裡不足的地方跟一些個人建議，如果想要看完整的心得流程，建議可以參考[這篇](https://blog.justin0u0.com/2021-Dcard-Web-Backend-Intern-%E9%9D%A2%E8%A9%A6%E7%B6%93%E9%A9%97%E5%88%86%E4%BA%AB/)。

</br>

&ensp;&ensp;Dcard 面試階段主要有履歷審查、一面、二面，而我是在一面完被刷掉，所以下面就分成履歷審查跟一面兩部分，分別說明我在每一階段做了什麼以及自己在這一階段中學了什麼。

## 履歷審查階段
&ensp;&ensp;大家都知道，Dcard 的履歷審查階段會需要你完成一份作業跟繳交你的個人履歷，繳交個人履歷是為了讓面試官知道你的經歷跟做過哪些 project，好讓他們可以根據你的履歷問你問題，而作業的部分我的理解是，不是只有完成他們要求就好，一定要能做多好就做多好，因為這同時也表現出了你對於這份實習的態度。

### 履歷
&ensp;&ensp;可以在 [Resume](https://blog.ivanouo.one/resume.pdf) 參考我的履歷，面試完 Dcard 跟其他幾間後，其實我覺得履歷上最重要的就只有 work experience 跟 selected project 兩個部分，下面是個人建議。

</br>

&ensp;&ensp;首先第一個是自己真的做了什麼才放上履歷，因為 Dcard 面試官問得非常仔細，會先問你說你在這個 project 中做了什麼跟學了什麼技術，然後再根據你回答請你更詳細的解釋(越細越好)，舉例來說，我說我某個 project 中負責處理 observability 三要件中 metrics 的部分，所以有用到 Prometheus 跟 OpenTelemetry，他就會請你介紹一下 Prometheus、為什麼需要用到這個東西以及他的優點在哪裡。所以自己必須熟悉在履歷上寫的任何一個 project 跟技術，個人認為如果在這邊被問爆了基本上就沒救了，所以請把乖乖的把躺分的 project 拿掉。

</br>

&ensp;&ensp;再來是 project 跟你面試單位的相關性，舉例來說，如果你面試的是 backend，那麼建議請盡量放跟 backend 技術有相關的 project，這點應該不需要多作解釋。

</br>

&ensp;&ensp;最後就是面試前複習一下自己寫的履歷，盡可能的把各種你寫的東西做延伸，思考他可能會問你什麼問題，為了就是在面試中問你履歷上各種問題時，你都不需要花很多時間去想當初這樣做的理由，避免自己因為突然卡住而開始緊張，打亂了自己面試的節奏。

### 作業
&ensp;&ensp;說到作業，今年的作業是請你 implement 一個 URL shortener，也就是給你一串網址，你的服務要可以產生一個 shortened URL，並且對你的服務打這個 shortened URL，如果沒有過期，要可以支援 redirect 到原本的 URL 網站，如果過期了，就回傳 error。這個作業看起來很簡單啊 (一開始看到我是這麼想的)，但是你仔細思考一下就會越想越不對。

</br>

&ensp;&ensp;首先先來討論如何縮短 URL 這個部分，要怎樣才能做到 shorten 這一件事、有沒有考慮到 shortened URL 碰撞的情況、如果真的碰撞了有沒有辦法處理、有沒有考慮到可能淺在的資安問題、過期的 shortened url 有沒有辦法繼續使用、同個 URL 能不能有兩個以上的 shortened URL、超大流量的話要怎麼辦、DB 要選擇用 SQL 還是 NoSQL、DB schema 要怎麼設計 (歡迎留言繼續補充)，以上是我一開始想到的各種可能需要考慮到的問題。

</br>

&ensp;&ensp;開始實作前，應該就要考慮到這份 project 架構要怎麼 design、怎麼維護你的 project，確保之後可以更好的做 extension、有沒有 lint、version control、註解、實作中 service 要放在哪裡、schema 要放在哪裡、toolkit 要放哪裡、會用到哪些 component，以上盡量都要想好再開始實作。

</br>

&ensp;&ensp;開發中，要怎麼確定你寫的東西是正確的，那就是 testing 啊，這裡就要考慮說你有沒有把 test 寫好、寫到什麼程度、各種情況都測試到了嗎、有沒有正確的 response client 正確的結果、testing 架構是使用哪一個撰寫。會考慮到這麼多是因為 testing 是開發中非常重要的一環，不僅可以幫助測試 bug，也確保未來新功能的增加時，舊功能依然可正常運作。

</br>

&ensp;&ensp;最後幾點，有沒有 CI/CD、是不是部署到 K8S 上、用了哪些雲服務、選擇了這個平台的理由，個人認為上面實作完後，應該要提供 demo，也是個可以加分的地方。

</br>

&ensp;&ensp;這是我實作的 [repo](https://github.com/tsw303005/Dcard-URL-Shortener)，頂多只有完成上面提到的七成而已，明顯有許多的進步空間，其實這邊就可以反思一下，自己目前實力到底到什麼程度、實作中遇到問題的時候，自己有沒有解決問題的能力、能不能立刻想到解決辦法、能不能靠自己 google 到想要的答案、自己的知識量到底夠不夠讓你判斷錯誤訊息來源是什麼。這次很顯然自己還有很多需要學習的地方。

## 一面
&ensp;&ensp;這一關就很單純，對方瘋狂地問你問題，下面就直接列出我這次被問到的所有問題。
</br>

### 問答
1. 有沒有寫 blog，blog 是用什麼寫的。
2. 以前 project 都用了哪些技術，請說出最近做了什麼 project。
3. (延伸) 介紹一下什麼是 Prometheus。
4. 請你介紹 Golang 的 channel。
5. 有沒有聽過 view。
6. 請說出 TCP、UDP、HTTP 的差別，越詳細越好。
7. 用過哪些 K8S 的 components，分別介紹一下。
8. 在你這次作業的實作中，能不能解釋為什麼你想要這樣實作。
9. 在你作業實作中，有沒有想到什麼 future work(或是你一些可以做更好的點)，說明一下你想要怎麼實作。

### 實作
1. 請你選擇用 Golang 或是 JavaScript 去 implement 一個 function (題目不難，在看你對語言的熟悉度跟邏輯思考)。
2. 給你兩個 table 的 schema，只下一個 SQL 去得到他們想要回傳的結果。

## 心得
&ensp;&ensp;老實說，大概問題問到一半的時候我心態就有點崩了，也大概知道自己已經涼了，但同時也體會到自己還有哪些不足的地方。
首先第一個就是對於一些基本的東西了解的不夠熟悉，一昧想要追求新技術卻忽略了這些技術的根本，就像上面 TCP、UDP、HTTP 比較中，我在實作時候用到了框架其實就是建立在這些基礎知識上，只是框架的包裝讓我忘記了整個架構的就是因為建立在這些基礎上才得以做延伸。第二個對於 SQL 的熟悉度，其實這也是很基礎的能力，現在哪個服務沒有 DB，所以我認為這也是一個自己該反省的地方需要加強的地方。最後一個就是知識量太少，這就是需要時間去累積的了 QQ

</br>

雖然跟這次的 Dcard 實習無緣，但是最大的收穫就是知道自己哪個部分需要加強，哪邊需要改進，希望未來的自己可以持續學習，分享更多有用的東西 xd
