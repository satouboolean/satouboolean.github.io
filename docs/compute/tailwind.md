---
title: Tailwind
tags:
  - Tailwind
categories: programming
---

## Layout

### Aspect ratio

| value         | equals             |
| ------------- | ------------------ |
| aspect-auto   | aspect-ratio: auto |
| aspect-square | aspect-ratio: 1/1  |
| aspect-video  | aspect-ratio: 16/9 |

### container

example: `<div class="container sm">`

| value  | equals            |
| ------ | ----------------- |
| `None` | width: 100%       |
| sm     | max-width: 640px  |
| md     | max-width: 768px  |
| lg     | max-width: 1024px |
| xl     | max-width: 1280px |
| 2xl    | max-width: 1536px |

### Box Shadow
| value  | equals            |
| ------ | ----------------- |
| shadow-sm | box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05)       |
| shadow     | box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);  |
| shadow-md     | box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);  |
| shadow-lg     | 	box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1); |
| shadow-xl     | 	box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1); |
| shadow-2xl    |box-shadow: 0 25px 50px -12px rgb(0 0 0 / 0.25); |
| shadow-inner    | box-shadow: inset 0 2px 4px 0 rgb(0 0 0 / 0.05); |
| shadow-none    | box-shadow: 0 0 #0000; |

## [Conditional apply](https://tailwindcss.com/docs/hover-focus-and-other-states)

| condition | example                     | explain                          |
| --------- | --------------------------- | -------------------------------- |
| hover     | text-sm **hover:**text-base | apply in hover                   |
| focus     |                             |                                  |
| active    |                             |                                  |
| first     |                             | apply when it is the first-child |
| last      |                             | apply when it is the last-child  |
| odd       |                             | apply when it is the odd-child   |
| even      |                             | apply when it is the even-child  |

## Spacing

### Pixel value

| value | equals         |
| ----- | -------------- |
| 0     | 0px            |
| px    | 1px            |
| 0.5   | 2px = 0.125rem |
| 1     | 4px = 0.25rem  |
| 1.5   | 6px = 0.375rem |
| 2     | 8px = 0.5rem   |

### [padding](https://tailwindcss.com/docs/padding)

| class          | translation                   |
| -------------- | ----------------------------- |
| p              | padding                       |
| pt, pb, pl, pr | padding-top/bottom/left/right |
| px             | padding-left + right          |
| py             | padding-top + bottom          |
| ps, pe         | padding-inline-start / end    |

### [margin](https://tailwindcss.com/docs/margin)

| class          | translation                  |
| -------------- | ---------------------------- |
| m              | margin                       |
| mt, mb, ml, mr | margin-top/bottom/left/right |
| mx             | margin-left + right          |
| my             | margin-top + bottom          |

### space

| class   | translation |
| ------- | ----------- |
| space-y | margin-top  |
| space-x | margin-left |

## Text

### text (font-size + line-height)
| value     | equals                                 |
| --------- | -------------------------------------- |
| text-xs   | font-size:  12px <br>line-height: 16px |
| text-sm   | font-size:  14px <br>line-height: 20px |
| text-base | font-size:  16px <br>line-height: 24px |
| text-lg   | font-size:  18px <br>line-height: 28px |
| text-xl   | font-size:  20px <br>line-height: 28px |
| text-2xl  | font-size:  24px <br>line-height: 32px |
| text-3xl  | font-size:  30px <br>line-height: 36px |

## border

### border width
| value    | equals                 |
| -------- | ---------------------- |
| border-0 | border-width: 0px;<br> |
| border-2 | border-width: 2px;<br> |
| border-4 | border-width: 4px;<br> |
## Responsive design

only apply when width reach requirement

| condition | example | explain        |
| --------- | ------- | -------------- |
| sm        | sm:p-8  | width > 640px  |
| md        | md:p-8  | width > 768px  |
| lg        | lg:p-8  | width > 1024px |

