---
title: QRcode
categories: dsp
---

[Reference](https://www.youtube.com/watch?v=w5ebcowAJD8)

### Quiet Zone

Outside of the QR code, without any infos

### Position Squares

3 8x8 sqaures on top-left, top-right and bottom-left corners.

Formed by a 7x7 black squres, 5x5 white squares and a filled 3x3 black sqaure and outlined by white.

{% asset_img position_squares.png 300 300 QRcode_PositionSquares %}

### Alignment Pattern (the bottom right square)

Formed by 5x5 black squares, 3x3 white squares and a filled 1x1 black square.

Offset by 4 from the bottom and 4 from the right

{% asset_img alignment_pattern.png 300 300 QRcode_AlignmentPattern %}

### Timeing Strips

Generated along the 7x7 black squares of position squares. In alternating black and white patterns.

{% asset_img timeing_strip.png 300 300 QRcode_TimeingStrip %}

### Format Strips

Around the position squares. Shown in red in picture.

Which stores the following infos:

1. level of correction
2. mask pattern

{% asset_img format_strip.png 300 300 QRcode_FormatStrip %}

## Data

The content of QR code is starting at the bottom right of the QR code, in a zigzag pattern.

There are 3 parts of the data,

1. data format (reserved as 4 bits)
2. data size (reserved as 8 bits)
3. data
4. 4 bits of 0s to fill the half byte

{% asset_img zigzag.png 300 300 QRcode_Zigzag %}

### data format

The bottom right 4 bit defines the data format.

The bit position \
43\
21

| bit  | data         |
| ---- | ------------ |
| 0001 | Numeric      |
| 0010 | Alphanumeric |
| 0100 | Binary       |
| 1000 | Kanji        |

### data size

The 8 bits following the data format defines the data size.

### level of correction

L: 7%
M: 15%
Q: 25%
H: 30%

the percentage means the tolerance of damage.
