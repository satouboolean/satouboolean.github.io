---
title: Live2D Tutorials
tags:
  - Live2D
categories: animation
---
# Blinking

[source](https://docs.live2d.com/cubism-editor-tutorials/eye-blink/?utm_source=L2Dmarcomm&utm_medium=youtube&utm_campaign=casual_tutorial)

## Meshing

1. Select your target object
2. Click the manual meshing button to enter meshing mode (Ctrl+E)

{% asset_img manualMeshing.png %}

3. Delete the default vertices by Ctrl+A → Delete
4. Change to the add vertex pencil

5. Add mesh by Manual or by Stroke

### Manual meshing

{% asset_img addVertex.png %}

Add vertices inside and surround the pictures and press Ctrl+R to connect the vertices

(Its recommand to add even amount of vertices with same offset when you add vertices outside)

{% asset_img manualMeshingSample.png %}

### Stroke meshing

{% asset_img StrokeAddVertice.png %}

{% asset_img strokeMeshingSample.png %}

{% asset_img strokeMeshingSample-2.png %}

Tune the details by setting offsets

{% asset_img strokeMeshingDetails.png %}

### Auto meshing

{% asset_img autoMeshing.png %}

{% asset_img autoMeshing-2.png %}

## Parameter

1. Select all moving object in folder
   (Don't include 瞳 in the keyframe when you making blind)
2. Click on the target parameter bar
3. Insert keys in to end of the bar

{% asset_img addKey.png %}

4. Select the key you want to edit (it will have red highlight on the target key)

5. Select, move and transform the end state of the components

### Moving

You can select and move by holding Shift to displace targets in only one axis

### Transform

#### Deform Path

1. Select to target component
2. Click deform path button

{% asset_img DeformPathButton.png %}

3. Add points for deformation

{% asset_img DeformPathSample.png %}

#### Deform Brush

1. Select to target component
2. Click deform brush button

{% asset_img DeformBrushButton.png %}

You can also edit the size and strength of the brush

{% asset_img DeformBrushDetails.png %}

### Clipping

In order to prevent some components protruding, we use clipping

1. Found the parent object which limit the components inside of itself
2. Copy the ID of it
3. Paste the ID into all child object in Clipping(クリッピング) and press Enter

# Mouth Movment

[source](https://docs.live2d.com/cubism-editor-tutorials/mouth-aiueo/)

{% asset_img mouthParamater.png %}
