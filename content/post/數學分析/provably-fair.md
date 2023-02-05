---
title: "公正雜湊驗證機制"
date: "2022-05-28"
categories:
 - "math"
tags:
 - "math"
 - "hash"
 - "game"
toc: true
---

# 公正雜湊驗證機制


根據雜湊不可逆原理達成的玩家信任機制。
## 玩家驗證角度看流程圖

{{< mermaid >}}
sequenceDiagram
  Client->>Server: Client_Seed_A
  Server->>Client: Hashed_Server_Seed_A
  loop Client Nonce++
      Client->>Client: Playing
  end
  Client->>Server: new Client_Seed_B
  Server->>Client: Server_Seed_A, Hashed_Server_Seed_B
  
  Note left of Client: Check "Server_Seed_A" & "Hashed_Server_Seed_A"
  loop Client Nonce++
      Client->>Client: Verify By Server_Seed_A, Client_Seed_A
  end
{{< /mermaid >}}

## 機制概述
根據 **伺服器種子(Server_Seed)** 與 **玩家種子(Client_Seed)** 產生雜湊字串(SHA512)，根據其字串上取得該遊戲結果。  
並於是前給予玩家 **已經雜湊的伺服器種子(Hashed_Server_Seed)** ，使玩家可以事後與 **伺服器種子(Server_Seed)** 做雜湊驗證，讓玩家確保沒有作弊的可能性。  

## 驗證需求

欄位|意義
---|---
Hashed_Server_Seed|於下注前給玩家
Server_Seed|玩家更換 Client Seed 的時候再給玩家
Client_Seed|玩家可以自行更新
Nonce|隨下注次數增加(從"1"開始)  
  
  

<!--more-->
## 參考競品: Bitsler provably-fair
https://www.bitsler.com/en/provably-fair

## 技術細節
1. Hashed_Server_Seed Server_Seed 的雜湊函數使用 SHA256 
2. 取得遊戲結果的雜湊字串 的雜湊函數使用 SHA512
3. 取得遊戲結果的雜湊字串 由 Server_Seed, Client_Seed, Nonce這三個字串決定
4. 雜湊字串如何計算成遊戲結果的邏輯會公告


## 玩家驗證重點
1. 遊戲項目事先給予的Hashed_Server_Seed與事後Server_Seed是否符合SHA256的驗證
2. 是否可以根據SServer_Seed, Client_Seed, Nonce正確計算出遊戲結果


## 雜湊字串如何計算成遊戲結果的邏輯

### Dice遊戲展示

#### 公告程式碼(PHP)
```php
$seed=hash_hmac('sha512',$clientSeed .','. $nonce, $serverSeed);


$offset=0;
do{
  $number=substr($seed,$offset,5);
  $number=hexdec($number);
  $offset+=5;
}
while($number > 999999);


$luckyNumber = ($number % 10000) / 100;
echo $luckyNumber;
```
#### hash_hmac
```php
$seed=hash_hmac('sha512',$clientSeed .','. $nonce, $serverSeed);
```
seed為取得遊戲結果的雜湊字串  
其為一十六進制的制字串,其每個字符的值域為[0,1,2,...e,f]  

#### do while決定number
```php
$offset=0;
do{
  $number=substr($seed,$offset,5);
  $number=hexdec($number);
  $offset+=5;
}
while($number > 999999);
```

每五個字符取一單位，故每個單位的值域為$[0,16^5)$  
為了在十進制可以無偏誤(unbias)，故 number > 999999時，取下五個字符為單位  
SHA512長度共128個字符，若取完所有單位後皆 number > 999999，則 number會視為預設值0，  
取完所有單位的概率極低
$(\frac{16^5-999999}{16^5})^{rounddown(128/5)} \approx 4.4235346e-34$，故可視其無顯著影響。  

#### 轉換遊戲結果並回傳
```php
$luckyNumber = ($number % 10000) / 100;
echo $luckyNumber;
```