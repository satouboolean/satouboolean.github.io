---
title: Scaffold
tags:
  - Flutter
---

# Scaffold

The Scaffold is designed to be a top level container for a flutter app.

## Properties

| Property name       | class               | Explaination                     |
| ------------------- | ------------------- | -------------------------------- |
| appBar              | PreferredSizeWidget | Defines the top bar of the page  |
| backgroundColor     | Color               |
| body                | Widget              | The body to be shown in the page |
| bottomNavigationBar | Widget              |
| drawer              | Widget              |

## Example

```Dart
Scaffold(
      appBar: AppBar(
        title: Text('AppBar Title'),
        titleTextStyle: TextStyle(color: Colors.white, fontSize: 20),
        backgroundColor: DarkThemeColor.chocolate,
      ),
      body: MainPage()
      bottomNavigationBar: NavbarWidget(),
      drawer: CustomDrawer(),
    );
```
