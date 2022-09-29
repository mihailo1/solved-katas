# [Simplifying multilinear polynomials](https://www.codewars.com/kata/55f89832ac9a66518f000118) - 4 kyu
#### Completed: Saturday, March 27, 2021
### JavaScript
```javascript
function simplify(poly) {
  return poly
    .replace(/-/g, "+-")
    .split("+")
    .filter((i) => i)
    .map((item) => ({
      negative: item.indexOf("-") !== -1,
      multiply: (item.match(/\d+/g) || ["1"])[0],
      value: item
        .match(/[a-zA-Z]+/g)[0]
        .split("")
        .sort((a, b) => a.localeCompare(b))
        .join(""),
    }))
    .filter(({multiply}) => multiply != 0)
    .reduce((acc, item) => {
      const duplicate = acc[acc.findIndex(({ value }) => value === item.value)];
      if (duplicate) {
        const getValue = (item) => item.multiply * (item.negative ? -1 : 1);
        const res = getValue(duplicate) + getValue(item);
        if (res === 0) {
          acc.splice(acc.indexOf(duplicate), 1);
        } else {
          duplicate.negative = res < 0;
          duplicate.multiply = Math.abs(res);
        }
        return acc;
      }

      return [...acc, item];
    }, [])
    .sort(function (a, b) {
      if (a.value.length === b.value.length)
        return a.value.localeCompare(b.value);
      return a.value.length > b.value.length ? 1 : -1;
    })
    .map(
      ({ multiply, value, negative }) =>
        (negative ? "-" : "") + (multiply > 1 ? multiply : "") + value
    )
    .reduce(
      (acc, val, i) =>
        `${acc}${
          i !== 0 ? (val.slice(0, 1)[0] === "-" ? val : "+" + val) : val
        }`,
      ""
    );
}
```

# [Complete Fibonacci Series](https://www.codewars.com/kata/5239f06d20eeab9deb00049b) - 6 kyu
#### Completed: Tuesday, March 9, 2021
### JavaScript
```javascript
function fibonacci(n) {
  //return fibonacci array of n elements
  const acc = [0];
  
  if(n < 1) return [];
  for (let i = 1; i < n; i++) {
    if (i === 1) acc.push(1);
    else acc.push(acc[i-2]+acc[i-1]);
  }
  return acc;
}
```

# [Roman Numerals Decoder](https://www.codewars.com/kata/51b6249c4612257ac0000005) - 6 kyu
#### Completed: Monday, March 8, 2021
### JavaScript
```javascript
function solution(roman){
 const translate = {I:1,V:5,X:10,L:50,C:100,D:500,M:1000};


  return roman.split('').reduceRight((acc, symbol, i, arr) => {
    const cur = translate[symbol];
    
    const prev = i === roman.length - 1 ? 0 : translate[arr[i + 1]];    
    
    const res = cur >= prev ? cur : -cur;
    
    return acc + res;
  }, 0)
}
```

# [Snail](https://www.codewars.com/kata/521c2db8ddc89b9b7a0000c1) - 4 kyu
#### Completed: Wednesday, March 11, 2020
### JavaScript
```javascript
snail = function(array, stack = []) {
  if (array.length !== 0) {
    stack.push(...array[0]);
    array.shift();
  }

  array =
    array.length !== 0
      ? array.map(el => {
          stack.push(el[el.length - 1]);
          el.pop();
          return el;
        })
      : array;

  if (array.length !== 0) {
    stack.push(...array[array.length - 1].reverse());
    array.pop();
  }

  if (array.length !== 0) {
    [...array].reverse().forEach(el => {
      stack.push(el[0]);
    });
    array = array.map(el => {
      el.shift();
      return el;
    });
  }

  if (array.length > 0) return snail(array, stack);

  return stack;
};

```

# [Sum of Intervals](https://www.codewars.com/kata/52b7ed099cdc285c300001cd) - 4 kyu
#### Completed: Tuesday, January 28, 2020
### JavaScript
```javascript
function sumIntervals(intervals){
const arr = [];
  intervals.forEach(interval => {
    for(let i=interval[0]; i < interval[1]; i++) arr.push(i);
  });
  const stack = [];
  arr.map(num => !stack.includes(num) ? stack.push(num) : null);
  return stack.length;
};
```

# [Last digit of a large number](https://www.codewars.com/kata/5511b2f550906349a70004e1) - 5 kyu
#### Completed: Tuesday, January 28, 2020
### JavaScript
```javascript
var lastDigit = function(str1, str2){  
return +!+str2 || Math.pow(str1.slice(-1), str2.slice(-2) % 4 || 4) % 10;
}
```

# [WeIrD StRiNg CaSe](https://www.codewars.com/kata/52b757663a95b11b3d00062d) - 6 kyu
#### Completed: Tuesday, January 28, 2020
### JavaScript
```javascript
function toWeirdCase(string){
 return string.split(' ').map(word => word.split('').map((letter,index) => index % 2 === 0 ? letter.toUpperCase() : letter.toLowerCase()).join('')).join(' ');
};
```

# [Highest Scoring Word](https://www.codewars.com/kata/57eb8fcdf670e99d9b000272) - 6 kyu
#### Completed: Thursday, December 19, 2019
### JavaScript
```javascript
function high(str){
let x = 'abcdefghijklmnopqrstuvwxyz';
x = x.split('');
const grades = {};
x.forEach((letter,index) => grades[letter] = index);
let c = 0;
let finalWord;
str = str.split(' ').filter(word => {
   let temp = 0;
   word.split('').forEach(l => {
      for(let prop in grades) {
      if(l === prop) temp += grades[prop];
      };
   });
  if(temp > c) {
    c = temp;
    finalWord = word;
};
  // u b u d
});

return finalWord;
}
```

# [Tribonacci Sequence](https://www.codewars.com/kata/556deca17c58da83c00002db) - 6 kyu
#### Completed: Tuesday, December 17, 2019
### JavaScript
```javascript
function tribonacci(arr,n){
  for(i=0;i<n;i++) {
     arr.push(arr[i] + arr[i+1] + arr[i+2]);
  }
return arr.splice(0,n)
}
```

# [Extract the domain name from a URL](https://www.codewars.com/kata/514a024011ea4fb54200004b) - 5 kyu
#### Completed: Tuesday, December 17, 2019
### JavaScript
```javascript
function domainName(url){
const urlX = url.split('');
if(urlX[0] === 'h') {
urlX.splice(0,4);
if(urlX[0] === 's') urlX.splice(0,4);
if(urlX[0] === ':') urlX.splice(0,3);
};
if(urlX[0] === 'w') urlX.splice(0,4);

const urlStack = [];

for(let el of urlX) {
  if(el === '.') break;
  urlStack.push(el)
}

return urlStack.join('');

}
```

# [Take a Ten Minute Walk](https://www.codewars.com/kata/54da539698b8a2ad76000228) - 6 kyu
#### Completed: Monday, December 16, 2019
### JavaScript
```javascript
function isValidWalk(arr) {
console.log(arr);
  let SNcounter = 0;
  let WEcounter = 0;
  arr.forEach(el => {
  el === 's' ? ++SNcounter : null;
  el === 'n' ? --SNcounter : null;
  el === 'w' ? ++WEcounter : null;
  el === 'e' ? --WEcounter : null;
  });
  return arr.length === 10 && SNcounter === 0 && WEcounter === 0 ? true : false;
}
```

# [Array Helpers](https://www.codewars.com/kata/525d50d2037b7acd6e000534) - 6 kyu
#### Completed: Sunday, December 8, 2019
### JavaScript
```javascript
// TODO
Array.prototype.square = function() { return this.map(el => el*el)};
Array.prototype.cube = function() { return this.map(el => el*el*el)};
Array.prototype.average = function() {return this.length > 0 ? this.reduce((acc,el) => acc+el) / this.length : NaN};
Array.prototype.sum = function() {return this.reduce((acc,el) => acc+el)};
Array.prototype.even = function() {return this.filter(el => el%2 === 0)};
Array.prototype.odd = function() {return this.filter(el => el%2 === 1)};
```

# [Directions Reduction](https://www.codewars.com/kata/550f22f4d758534c1100025a) - 5 kyu
#### Completed: Friday, November 29, 2019
### JavaScript
```javascript
function dirReduc(arr){
console.log(arr)
 const x = () => {
    for(i=1;i<arr.length;i++){
        if ((arr[i] === 'SOUTH' && arr[i-1] === 'NORTH')||(arr[i] === 'NORTH' && arr[i-1] === 'SOUTH')) {
          del();
        } else if ((arr[i] === 'EAST' && arr[i-1] === 'WEST')||(arr[i] === 'WEST' && arr[i-1] === 'EAST')) {
          del();
        };
    };
  };
  const del = () => {
    arr.splice(i,1);
    arr.splice(i-1,1);
    x();
  };
  x();
  return arr;
}
```

# [Two Sum](https://www.codewars.com/kata/52c31f8e6605bcc646000082) - 6 kyu
#### Completed: Thursday, November 28, 2019
### JavaScript
```javascript
function twoSum(numbers, target) {
  const sum = [];
  for(i=0;i<numbers.length;i++) {
   for(j=i+1;j<numbers.length;j++) {
    if(numbers[i] + numbers[j] === target) {
     sum.push(i,j);
     return sum;
    }
   }
  }
}
```

# [Sum ALL the arrays!](https://www.codewars.com/kata/5594463eaf1701909c0000d4) - 7 kyu
#### Completed: Thursday, November 28, 2019
### JavaScript
```javascript
function arraySum(arr) {
 return arr.toString().split(',').map(el => isNaN(parseFloat(el)) ? 0 : parseFloat(el)).reduce((acc,el) => acc + el);
}
```

# [Factorial](https://www.codewars.com/kata/54ff0d1f355cfd20e60001fc) - 7 kyu
#### Completed: Thursday, November 28, 2019
### JavaScript
```javascript
function factorial(n) {
if (n < 13 && n > -1) {
let temp = 1;
for (i=1;i<=n;i++) temp *= i;
return temp;
} else if ( n === 0) {
return 1;
} else throw new RangeError();
}
```

# [Odd or Even?](https://www.codewars.com/kata/5949481f86420f59480000e7) - 7 kyu
#### Completed: Tuesday, November 19, 2019
### JavaScript
```javascript
function oddOrEven(arr) {
   return arr.length === 0 ? 'even' : arr.reduce((el, acc) => el + acc) % 2 === 0 ? 'even' : 'odd';
}
```

# [The Hashtag Generator](https://www.codewars.com/kata/52449b062fb80683ec000024) - 5 kyu
#### Completed: Thursday, November 14, 2019
### JavaScript
```javascript
function generateHashtag (str) {
if(str === '' || str.match(/\w+/g) === null) {
return false
} else {
let x = str.match(/\w+/g).map(el => {
   el = el.split('');
   el[0] = el[0].toUpperCase();
   return el.join('');
 });
 x.unshift('#');
 return x.join('').length < 141 ? x.join('') : false;
 }
}
```

# [Count the smiley faces!](https://www.codewars.com/kata/583203e6eb35d7980400002a) - 6 kyu
#### Completed: Thursday, November 14, 2019
### JavaScript
```javascript
//return the total number of smiling faces in the array
function countSmileys(arr) {
let c = 0;
arr.forEach(el => {
  el = el.split('');
  if (el[0] === ':' || el[0] === ';') {
     if (['-', '~'].includes(el[1])) {
        if([')', 'D'].includes(el[2])) {
            el.length === 3 ? c++ : null;
        }
     } else if ([')', 'D'].includes(el[1])) {
        el.length === 2 ? c++ : null;
     }
  }
});

return c;
}
```

# [Count the Monkeys!](https://www.codewars.com/kata/56f69d9f9400f508fb000ba7) - 8 kyu
#### Completed: Wednesday, November 13, 2019
### JavaScript
```javascript
function monkeyCount(n) {
let arr = [];
for(i=1;i<n+1;i++) arr.push(i)
 return arr;
}
```

# [Jaden Casing Strings](https://www.codewars.com/kata/5390bac347d09b7da40006f6) - 7 kyu
#### Completed: Tuesday, November 12, 2019
### JavaScript
```javascript
String.prototype.toJadenCase = function () {
    return this.split(' ').map(el => {
el = el.split('');
console.log(el)
el[0]= el[0].toUpperCase();
return el.join('');
    }).join(' ')
}

```

# [Your order,  please](https://www.codewars.com/kata/55c45be3b2079eccff00010f) - 6 kyu
#### Completed: Tuesday, November 12, 2019
### JavaScript
```javascript
function order(words){
if (words) {
  wordsPlace = words.split(' ').map(el => {
    return el.split('').find(x => !!parseInt(x));
  });



  words = words.split(' ').map((el, i) => {
   el = el.split('');
   el.unshift(wordsPlace[i]);
   return el.join('');
  });
 
  words.sort();

  words = words.map(el => {
   el = el.split('');
   el.shift(0);
   return el.join('');
  });
  
  return words.join(' ');
  
} else {
return words
};
}
```

# [Friend or Foe?](https://www.codewars.com/kata/55b42574ff091733d900002f) - 7 kyu
#### Completed: Sunday, November 10, 2019
### JavaScript
```javascript
function friend(friends){
  return friends.filter(el => el.length === 4 && isNaN(parseInt(el)))
}
```

# [You're a square!](https://www.codewars.com/kata/54c27a33fb7da0db0100040e) - 7 kyu
#### Completed: Tuesday, September 17, 2019
### JavaScript
```javascript
var isSquare = function(n){
let temp = false;
if (n >= 0) {
for(i = 0; i <= n; i++) {
if (i*i == n) {
temp = true;
break
} else {
temp = false;
}
}
}
return temp
}
```

# [Create Phone Number](https://www.codewars.com/kata/525f50e3b73515a6db000b83) - 6 kyu
#### Completed: Tuesday, September 17, 2019
### JavaScript
```javascript
function createPhoneNumber(numbers){
let x;

  numbers.forEach( function(item, i) {
  if (i == 0) {
  x = '('
}

x += item;

if (i == 2) {
x += ') ';
}
 if (i == 5) {
x += '-';
}
})

return x;
}
```

# [Multiply](https://www.codewars.com/kata/50654ddff44f800200000004) - 8 kyu
#### Completed: Tuesday, September 17, 2019
### JavaScript
```javascript
function multiply(a, b){
 return a * b
}

```

