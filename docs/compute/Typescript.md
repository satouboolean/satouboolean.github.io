---
title: Typescript
tags:
  - Typescript
categories: programming
---

## Object

### interface

``` Typescript
interface NewInterface {
    s : string;
    n : number;
}
```
### type
```Typescript
type newType = {
	s : string;
	n : number;
}
```

## Array
| **property**                                           | **return**                     | **usage**                                                                                  |
| ------------------------------------------------------ | ------------------------------ | ------------------------------------------------------------------------------------------ |
| pop(), shift()                                         | Array element                  | pop() and dequeue()                                                                        |
| push(), unshift()                                      |                                | add item to first / last element                                                           |
| includes(target)                                       | Boolean                        | check if the array have a element match target                                             |
| every((item)=>statment)                                | boolean                        | check if every element match the statement inside                                          |
| join(separator?)                                       | string                         | combine all string into one string with separator                                          |
| slice(start?,end?)                                     | Array                          | extract and start to end elements from an array<br>(can use negative to inverse direction) |
| splice(start?,end?)                                    | Array                          | deleting the start to end elements from an array and return the deleted item               |
| \[...array\]                                           |                                | (spread) fill content of the array                                                         |
| filter(item=>statement return true)                    | array                          | filter the element of array into array of element only fit the specified condition         |
| reduce((acc,cur)=statement with acc and cur,initValue) | non-array                      | process all elements in the array and return a final result of it                          |
| flatMap((item)=>item.child)                            | Array\<element in the object\> | extract element in the original array\<object\> into array\<child of object\>              |
| isArray(targetArray)                                   | boolean                        | check if targetArray is a array                                                            |
## Map
```Typescript
const value = 1;
const map : Map<string,number> = new Map<string,number>();
Map.set('key',value);
Map.get('key') //return 1
```

To initialize, can use `Object.entries`
```Typescript
const obj = { name: 'Bobby Hadz', country: 'Chile' };
const map1 = new Map<string, string>(Object.entries(obj));

// 👇️ Map(2) { 'name' => 'Bobby Hadz', 'country' => 'Chile' }
console.log(map1);

```

## Record
```Typescript
type objectTypeWithDynamicNames = Record<string,any>;
const example: objectTypeWithDynamicNames = {
	key1: 1,
	key2: '2'
};
```

To specify the keys in the object

```Typescript
type keyofTheObject = 'key1' | 'key2' | 'key3'

type objectWithSpecifiedKey =  Record <keyofTheObject,any>;

const example: objectWithSpecifiedKey = {
	key1: 'a',
	key2: 1,
}

const example2: objectWithSpecifiedKey = {
	key3: true,
}
```
The object is not forced to have all the key specified

To make sure the object have all non-optional keys
```Typescript
type keyofTheObject = 'key1' | 'key2' | 'key3'

type objectWithSpecifiedKey =  Record <keyofTheObject,any>;

const example = {
	key1: 'a',
	key2: 1,
} satisfies objectWithSpecifiedKey; //return compile error Property 'key' is missing in type '{ 	key1: 'a',	key2: 1, }' but required in type 'objectWithSpecifiedKey'.

const example2: objectWithSpecifiedKey = {
	key1: 'a',
	key2: 1,
	key3: true,
} satisfies objectWithSpecifiedKey; // correct
```

## Operator

### ??

Operator `??` is similar to `||`,
it take the right hand side if left hand side is undefined or null.

Difference:
`??` → use RHS when LHS is `null` or `undefined`
`||` → use RHS when LHS is `null` or `undefined` or `False` or `0`

### ??= 
```Typescript
let foo = null;
foo ??= 'foo'
foo ??= 'bar'
console.log(foo) //return 'foo'
```
### keyof

keyof object, used as type
```Typescript
Obj = {
	one: '1',
	two: '2',
	three: '3'
}
```

keyof typeof Obj is equal to 
```Typescript
type A = 'one'|'two'|'three'
```
### typeof

typeof object, used as type

### Unary Operator
#### +
Attempt to convert the operand into number
```Typescript
console.log(+"") // return 0
console.log(+true) //return 1
console.log(+false) // return 0
console.log(+"24") // return 24
console.log(+"31C") // return NaN
```

#### -
Attempt to convert the operand into number and negate it
```Typescript
console.log(-"24") // return -24
```

## Promise

### race
```Typescript
  const funcs: Promise<any>[] = [asyncFunction1, asyncFunction2];
  await Promise.race(funcs); // see tither of them resolve first
```

## To decide if property in a custom object
```Typescript
if ('propertyName' in CustomObject){
	//do sth
}
```

## For loop write style
```Typescript
for (const index of [...Array(maxNumber).keys()]){
	do things with index
}

for (const [index, { item }] of arrayOfSth.entries()) {
do things with index and item
}
```

## Array to union
```typescript
const possibleValue = ["Yamawaki", "Wakki", "Satouburian"]

type yamawaki = typeof possibleValue[number]; //"Yamawaki" | "Wakki" | "Satouburian"
``` 