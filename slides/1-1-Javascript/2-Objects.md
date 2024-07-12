# Objects & Arrays

Our two main types for representing data in JavaScript are Object and Array.

The main difference between the two is that Arrays ensure order, Objects do not.

---
# Types - Objects

To access and set properties in an Object, we can use auto assignment, dot notation or bracketed notation

```js
const assignToMe = {name1: "I'm auto assigned"};

assignToMe.name2 = "I'm a dot assignment";
assignToMe["name" + 3] = "I'm a bracket assignment";

console.log(assignToMe);
```
Note: <https://carbon.now.sh/efCTijMM7DgtATJEWBOo> ({name1: "I'm auto assigned",name2:"I'm a dot assignment",name3: "I'm a bracket assignment"})
---
# Types - Arrays

As mentioned in the last section, Arrays are actually implemented as types of object. The main difference is that Arrays ensure their order.
Generally you’d access an Array using the bracketed notation
```js [1|2|3|4-5|6-7]
const horses = ["Clydesdale", "Shire", "Unicorn"];
console.log(horses.length);
console.log(horses[0]);
horses.reverse();
console.log(horses[0]);
horses.concat(["Pegasus"])
console.log(horses.length)
```
---
### in-place 
```js
- sort()
- reverse()
- splice()
```
### out-of-place <!-- .element: class="fragment" data-fragment-index="1" -->
```js
- toSorted()
- toReversed()
- toSpliced()
- concat()
``` 
<!-- .element: class="fragment" data-fragment-index="1" -->
### Which is the best technique? <!-- .element: class="fragment" data-fragment-index="2" -->
