---
title: playwright
tags:
  - playwright
  - Typescript
  - Testing
categories: programming
---
 
## Setup and run [Playwright](https://playwright.dev/)

### Install playwright

```Powershell
npm init playwright@latest
```

### Run playwright in UI Mode

```Powershell
npx playwright test --ui
```

### Run test
```Powershell
npx playwright test `filename`.spec.ts --config=`config file name`.config.ts --workers=4 --retries=3 --project="mschromium" --trace on -g "(?=.\*zh_CN)" --headed
```


```Powershell
npx playwright test merchant-directory.spec.ts --config=playwright.monocart.config.ts --workers=4 --retries=3 --project="mschromium" --trace on -g "(?=.*zh_CN)" --headed
```

## Basic Syntax

test Describer - group tests

```Typescript
test.describe("GroupName", () => {
    test.beforeEach(async ({ page }) => {
    //reload target page for each test
    await page.goto("https://playwright.dev");
  });
  test("testName", async ({ page }) => {
  });
});
```

| Element Retriver        | Explaination                                                              | Example                                                  |
| ----------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------- |
| page.locator()          | [React locator](https://playwright.dev/docs/other-locators#react-locator) | await page.locator('\_react=ComponentName[enabled=true]) |
| page.locator()          | [xPath](https://playwright.dev/docs/other-locators#xpath-locator)         | await page.locator('//div[@class="className"]')          |
| page.locator()          | id                                                                        | await page.locator('#targetId')                          |
| page.locator()          | class name                                                                | await page.locator('.className > div > a')               |
| page.locator()          | css                                                                       | await page.locator('div:text("innerText")')              |
| page.getByRole()        | role                                                                      | await page.getByRole('button', { name: 'Submit' })       |
| page.getByText()        | text                                                                      | await page.getByText('Text')                             |
| page.getByLabel()       | label                                                                     | await page.getByLabel('Label')                           |
| page.getByPlaceholder() | placeholder                                                               | await page.getByPlaceholder('Placeholder')               |
| page.getByAltText()     | alt text                                                                  | await page.getByAltText('AltText')                       |
| page.getByTitle()       | title                                                                     | await page.getByTitle('Title')                           |
| page.getByTestId()      | test id                                                                   | await page.getByTestId('TestId')                         |
| locator.nth(index)      | n-th element                                                              | await page.locator('.className').nth(1)                  |

### locator iteration

```Typescript
  // selectedBrand = xpath locator with multiple results

  let brands = new Set(); //in case you want to get value
  for (const item of await selectedBrand.all()) {
    if (item) brands.add(item.getAttribute("value"));
  }
```

### xPath Conditions

| Conditions                             | Explaination              | Example                                                               |     |
| -------------------------------------- | ------------------------- | --------------------------------------------------------------------- | --- |
| Raw xPath                              | start by // or .. is same | await page.locator('..div[@class="className"]')                       |     |
| followed by child                      |                           | await page.locator('//div[@class="className"]/div/a')                 |     |
| select parent                          | use /.. to select parent  | await page.locator('//div\[@class="className"\]/..')                  |     |
| only select the nth child of same type |                           | await page.locator('//div[@class="className"]/div[1]')                |     |
| attribute cotains                      |                           | await page.locator('//span\[contains(@class, "keyword")\]             |     |
| xPath union                            |                           | await page.locator('//div(@class="className")] \| //div\[@id="id"\]') |     |
| filter by inner text                   |                           | await page.locator('//div\[contains(text(),"keyword")\]')             |     |
| following sibling                      | /following-sibling::      | {xpath}//following-sibling::div                                       |     |


### CSS Conditions

| Conditions     | Explaination                                  | Example                                                           |
| -------------- | --------------------------------------------- | ----------------------------------------------------------------- |
| div            | tag like \<div\>, \<p\>                       | await page.locator('div')                                         |
| \#id           | id attribute                                  | await page.locator('div#id1')                                     |
| .class         | .class<br>div.class                           | await page.locator('.class1')<br>await page.locator('div.class1') |
| .class1.class2 | element with multiple class                   | await page.locator('.class1.class2')                              |
| :has(>)        | element with matching child                   | await page.locator('.class1:has(> .class2)')                      |
| :has-text      | find children<br>contains<br>case-insensitive | await page.locator('div:has-text("innerText")')                   |
| :is-text       | find children<br>exact text<br>case-sensitive | await page.locator('div:is-text("innerText")')                    |
| :text          | exact text<br>case-insensitive                | await page.locator('div:text("innerText")')                       |
| :text-matches  | regex                                         | await page.locator('div:text-matches("reg?ex", "i")')             |
| :nth-match     | nth match 1-based                             | await page.locator(':nth-match(:text("innerText"), 1)')           |

### locator actions
| Actions         | Explaination                                                                | Example                             |
| --------------- | --------------------------------------------------------------------------- | ----------------------------------- |
| .click(option?) | optional to specify position of element<br>x,y where 0,0 is top-left corner | await page.locator.click({x:1,y:1}) |
## [Fixture](https://www.youtube.com/watch?v=2O7dyz6XO2s)

Create a custom `test` object which extend the original `test()` function from playwright

- setup duplicated action
- setup action after `use`

```Typescript
const myTest = test.extend({
  webApp: async({page},use) => {
    console.log('setup')
    await use(page)
    console.log('finished')
  }
})

myTest("Test Description", async ({webApp}) => {
  await expect(webApp.getByTestId("TestID")).toBeVisible() //action
})
```

What it does is: 'setup' > the action > 'finished'

For the predefined Fixture across multiple ts use,
`setup.ts`

```Typescript
const {test, expect} = require{"@playwright/test"}
const {ac, pw} = process.env // take login details from .env

exports.expect = expect // export the original expect from original playwright
exports.test = test.extends({
  webApp: async ({page},use)=>{
    // do all the login things here
    await use(page)
  },
})
```

and import the custom test and expect from other ts

```
const { test , expect } = require("./setup")
```

## Test mode
- serial
- parallel
- default
```Typescript
test.describe.configure({ mode: "serial" });
```

## Dialog
Playwright default to dismiss dialog automatically. So if we want to handle the dialog, we need to setup a dialog listener before the action which trigger dialog
```Typescript
aiPage.page.on('dialog', (dialog) => dialog.accept());
```