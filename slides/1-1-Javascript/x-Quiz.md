```js
[] == ![];
```
Note: <>(Output is...  true because it converts it to 0 == false which is 0 == 0 which is true )
---
```js
true == []; 
true == ![]; 

false == []; 
false == ![]; 
```
Note: <>(Output is...  false, false, true, true because toNumber(true) = 1, toNumber([]) = 0, ![] = false )
---
```js
true == []; 
true == ![]; 

false == []; 
false == ![]; 
```
Note: <>(Output is...  false, false, true, true because toNumber(true) = 1, toNumber([]) = 0, ![] = false )
---
```js
NaN === NaN;
```
Note: <>(NaN is always false. It's crazy but always returns false when you compare to it.)
---
```js
Object.is(NaN, NaN);
NaN === NaN;

Object.is(-0, 0);
-0 === 0;

Object.is(NaN, 0 / 0); 
NaN === 0 / 0; 
```
Note: <>(Output is true, false, false, true, true, false)
---
```js
parseInt(0.000001); 
parseInt(0.0000001);
parseInt(1 / 1999999);
```
Note: <>(Output is 0 correct, 1 because the value converts into a string "1e-7" which becomes 1, 5 goes to "5.00000250000125e-7" )
---
```js
0.1 * 0.2
```
Note: <>(Output is 0.020000000000000004. Some decimal numbers can't be represented in IEEE 754, the mathematical representation used by JavaScript. If you want to perform arithmetic with these numbers in your question, it would be better to multiply them until they are whole numbers first, and then divide them.)
