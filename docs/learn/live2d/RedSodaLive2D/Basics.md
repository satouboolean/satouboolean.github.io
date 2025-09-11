---
title: Redsoda Live2D Basics
tags:
  - Live2D
categories: animation
---
Warp35
Meshing
{% asset_img ToolBar1.png %}
テクスチャトラス編集 - Make texture sheet
メッシュの手動編集 - Manual meshing
メッシュの自動生成 - Auto meshing

Grouping
{% asset_img ToolBar2.png %}
ワープデフォーマの作成 - 曲面工具
回転デフォーマの作成 - 回轉工具
回転デフォーマ作成ツール - 回轉工具連續建立

調整位置用
{% asset_img ToolBar3.png %}
矢印ツール - 普通點選
投げ縄選択ツール - 套索
ブラシ選択ツール - Brush Selection

変形パスツール - 變形曲線
変形ブラシツール - 變形Brush

## Layer
Every object have a 絵描き順 - default 500
If 絵描き順 same, object above on top
If 絵描き順 not same, object with bigger number on top

## Meshing
### Meshing a Circle
1. Remove the default 4 lines
2. Select the default 4 vertices
3. Copy and paste → rotate
4. Repeat 3 until the amount reached
5. Create 4 vertices on 4 corner and 「自動接続」
6. Remove the 4 vertices and remove 余分 lines
7. Copy and paste → transform size for inner
7. Add a center vertex →「自動接続」→ Adjustment

### Meshing face line
鏡射 + ストローク


## 曲面工具
### ベジェ編集のタイプ
Default - コントロールの関係を維持 (只更改特定點)

- Smooth1 影響其他點
- Smooth2 影響其他點 比Smooth1強
- Smooth3 影響其他點 比Smooth2強

## Edit tool bar
{% asset_img editToolBar.png %}
### Solo
選取目標（可複選）然後按Solo → 突出目標

## Others
moc3 file should not be larger than 96MB, otherwise it is not able to be imported in VTS

Snap to keyframe - right click

Deform copy - Ctrl + Shift + C
Deform paste - Ctrl + Shift + V
Displace border - X + Drag

## 參考線
1. Right click on campus →ガイド
2. 水平線追加/垂直線追加

## Deformer smoothen
{% asset_img smoothen.png %}

建議把分割數降低才使用