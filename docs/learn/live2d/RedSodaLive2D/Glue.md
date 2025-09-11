---
title: Live2D Glue tool 
tags:
  - Live2D
categories: animation
---

## 膠水工具

{% asset_img gluePos.png %}

把兩個以上的物件各自的vertex連結起來，被連結的物件即使沒有建立keyframe影響也會被其他物件影響（視乎加權分佈，default 50-50）


## 實際操作

1. 決定兩個要連結的物件，然後複製其中一邊的vertices，貼到另一個物件上（目標應把範圍內的佈點刪除以免佈點過多）
2. 消除沒用的佈點（在物件之外過遠的）
3. 複選物件（Ctrl+click）（先選瞳孔/眼白 - 調整加權時不用轉mode）
4. 進入佈點編輯
5. 用投げ縄選取目標佈點（相同位置的有多個佈點的位置會有不同顏色）
{% asset_img glueInEditor.png %}
6. 按「バインド」綁定
7. 有綠色框的佈點表示已被綁定
8. パーツ視窗（Parts window）會出現新的物件（Glue_物件一_物件二）

### 調整加權
 
1. 按目標物件
2. 點編輯區內的標籤
{% asset_img tagButton.png %}
3. 按膠水工具
4. 畫加權分佈（按住Shift可以反轉mode）