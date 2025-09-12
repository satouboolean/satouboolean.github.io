---
title: Google App Script
tags:
  - Typescript
  - GoogleSpreadSheet
categories: programming
---

## SpreadsheetApp

| function       | example                                                |
| -------------- | ------------------------------------------------------ |
| getSheetByName | SpreadsheetApp.getActive().getSheetByName("sheetName") |

## onOpen()

Call functions when script is opened

### Create Menu item

```Javascript
  SpreadsheetApp.getUi().createMenu("Custom Filter")
    .addItem("Filter rows", "hideWeekEnd") // hideWeekEnd() is a function defined
    .addItem("Show all rows", "showAllRows") // showAllRows() is a function defined
    .addToUi();
```

or

```Javascript
var ss = SpreadsheetApp.getActiveSpreadsheet();
  var menuEntries = [ {name: "Option1", functionName: "FunctionToTrigger"},
                      null, // a null will produce a separater in the menu
                      {name: "Option2", functionName: "FunctionToTrigger2"},
                      {name: "Option3", functionName: "FunctionToTrigger3"},
                      null,
                      {name: "Option4", functionName: "FunctionToTrigger4"},
  ss.addMenu("MenuTitle", menuEntries);
```
