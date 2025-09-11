---
title: Live2D Eye
tags:
  - Live2D
categories: animation
---

## Steps
1. 素材準備
2. 佈點
3. [Glue](Glue)
4. Set masking
5. Adjust rendering order
6. Set animation frames
7. 鏡射


### 素材準備

眼球Mask
眼白Mask

7. Create a square as the mask base (fill with some color)
8. Ctrl + click the layer of target (眼球/眼白)
9. Switch to the layer of mask
10. delete to remove the area of target (眼球/眼白)

### 佈點

Meshing for 眼球、眼白

眼球 - copy square vertices / stroke meshing
眼白 - you know the drill

Copy the vertices for 眼球 and paste to 眼球Mask
Copy the vertices for 眼白 and paste to 眼白Mask

### Glue
11. Multi-select 眼球and 眼球Mask
12. バインド
13. Adjust weighting (100% for 眼球)
14. Turn the mask into 0% alpha
15. Repeat same step for **眼白**


### Set Masking

瞳孔 - 眼白
Things inside eye ball - 眼白+眼球
Highlights - 眼白

### Adjust rendering order

Adjust the rendering order
E.g. Highlight should be below eyebrows

## Animation frames

1. Open / Close eye（開閉Keyframe）
	- 閉眼被開眼時眼距較短
	  {% asset_img EyeReference.png %}
2. Smile（笑顏Keyframe）
	- 做完開閉眼後全選並在笑顏上開key frame
	- 從上眼瞼開始
3. 眼球彈跳曲面
	- 物理演算用
4. 眼球移動（眼球XY移動曲面）作為眼球彈跳曲面的父層
	- 建議把眼球XY移動曲面調整成方形
	- 盡量把兩極的距離設定相等
	- 四角生成後把複製四角的sin45°數值（**0.7071**）
5. 眼球球體變形（眼球球體曲面）（Week2Day2-1, 01:13:57）
	1. Copy眼球XY移動曲面
	2. 在被copy的曲面上生成新的曲面
	3. 分割數15×15
	4. 不影響子物件原地放大（Ctrl+Alt+Shift+Drag放大）- 放大至子物件移動時也能包括在內
	5. Brush選取工具點中間（圓最好放含所有點）
	6. 原地放大（Alt+Shift+Drag放大）
	7. 重複步驟4-6幾次（逐漸把選擇範圍縮小）
	8. 全體縮小
	9. 這樣把子層曲面變成近球體形狀
	10. 把本來的球眼XY移動曲面內的物件移到新的XY移動曲面內
	    {% asset_img AfterStep5.png %}
6. 虹膜XY位差曲面（Week2Day2-1, 01:20:00）
	1. 在目玉XY移動時留一點虹膜的慣性會比較有立體感
7. 眼晴亮光曲面
	1. 把亮光的跟隨目玉XY的位移調小
8. 眼眶隨眼球曲面 （Week2Day2-1, 01:28:40）
	1. 像是眼晴轉觀察方向時眼皮會騰出點點空間
9. 眉毛變形
	1. For 心情變化
10. 眉毛位移（眉面位移曲面）
	1. 眉毛位移
11. 眉毛角度曲面（眉毛位移曲面的子層）
12. 眉毛隨眨眼曲面（眉面位移曲面的父層）
	1. 在眨眼時把眉毛位移及變形
13. 驚訝開關
	1. 在眼眶曲面外層加上眼眶驚訝曲面 - 驚訝時撐大眼眶
	2. 在眼球曲面外層加上眼球驚訝曲面 - 驚訝時縮小瞳孔

## 曲面
- 右眼隨貶眼曲面(5)
	- 眼球球體曲面 - 影響眼球XY曲面變球體狀用（看[上面](#Animation frames)第五點）(3)
		- 眼球XY曲面 - 眼球XY移動用(2)
			- 眼球驚訝曲面(5)
				- 眼球曲面 - 物理眼球全體晃(1)
					- 眼球遮罩（鏡射時才放也可）
					- 瞳孔	
					- 虹膜XY位差曲面(4)
						- 虹膜
					- 反光位差曲面(4)
						- 虹膜反光
						- 眼球反光
- 眼眶驚訝曲面(3)
	-  眼眶曲面 - 物理眼眶晃(1)
		- 眼尾
		- 眼皮線
		- 眼頭線
		- 眼影
		- 眼皮影
		- 眼眶隨眼球曲面 - （看[上面](#Animation frames)第八點）(2)
			- 眼白遮罩（鏡射時才放也可）
			- 眼白
			- 睫毛
			- 眼瞼
- 眉毛隨貶眼曲面(3)
	- 眉毛上下曲面(2)
		- 眉毛角度曲面(1)
			- 眉毛
## 鏡射
1. 把眼球mask放進眼球曲面內
2. 把眼白mask放進眼眶曲面內
3. 在幾個最頂層曲面上加一個全體曲面
4. 確定所有東西都放左同一曲面後
5. 圈選所有有關眼晴的東西（包括膠水及遮罩）
6. 點選被新增的所有物件→右鍵→反転
7. 位置對好「參考位置用」
8. 把被反轉的物件全選起來
	-  {% asset_img selectObjectsUnderFolder.png %}
9. 只顯示被選擇物件相關的參數
	 - {% asset_img displayOnlySelectedItemParam.png %}
10. 目玉X→反転
11. 把所有有左右的參數変更成反方向的參數（例如︰左目關關→変更→右目開關）
