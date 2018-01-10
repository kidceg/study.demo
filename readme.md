# 一、JavaScript题目

### 1、求数组从小到大排序

```javascript
function func(a){
	for(var i=0;i<a.length;i++){
    for(var j = i + 1;j<a.length;j++){
        if(a[i]>a[j]){    //从大到小就改成<
            var temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
     }
  }
    return a;
}

var d=[9,2,33,66,55,56,34,1,91,88];
console.log(func(d));  //  [1, 2, 9, 33, 34, 55, 56, 66, 88, 91]
```
```javascript
var a=[9,2,33,66,55,56,34,1,91,88];
for(var i=0;i<a.length;i++){
    for(var j = i + 1;j<a.length;j++){
        if(a[i]>a[j]){    //从小到大就改成<
            var temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
    }
}
console.log(a);  //  [1, 2, 9, 33, 34, 55, 56, 66, 88, 91]
```

### 2.数组移除空元素
```javascript
function func(arr){
	for(var i = 0; i <= arr.length; i++){
		if(arr[i]===''){
		arr.splice(i,1);
		i = i - 1;
		}
	}	
	return arr;	
}
var arr = [1,99,'','',6,7,8,''];
var result = func(arr);
console.log(result); // 输出结果：[1,99,6,7,8];]
```
```javascript
function func(arr){
	var box = [];
	for(var i = 0; i < arr.length; i++){
		if(arr[i] !=='' ){
         box.push(arr[i]);
		}
	}	
	return box;	
}
var arr = [1,99,'','',6,7,8,'',''];
var result = func(arr);
console.log(result); // 输出结果：[1,99,6,7,8]
```
```javascript
function func(arr){
	for(var i = 0; i < arr.length; i++){
		if(arr[i] === ''){
			for(var j = i; j < arr.length - 1; j++){
				arr[j] = arr[j+1];
			}
			i-= 1;
			arr.length -=1;
		}
	}
	return arr;
}
var arr = [1,99,'','',6,7,8,'',''];
var result = func(arr);
console.log(result); // 输出结果：[1,99,6,7,8]
```

###  3.数组查找是否包含某些字符串

```javascript
Given two arrays of strings a1 and a2 return a sorted array r in lexicographical order of the strings of a1 which are substrings of strings of a2.

#Example 1: a1 = ["arp", "live", "strong"]
a2 = ["lively", "alive", "harp", "sharp", "armstrong"]
returns ["arp", "live", "strong"]

#Example 2: a1 = ["tarp", "mice", "bull"]
a2 = ["lively", "alive", "harp", "sharp", "armstrong"]
returns []
```
```javascript
测试用
var a2 = ["lively", "alive", "harp", "sharp", "armstrong"]
var a1 = ["xyz", "live", "strong"]
console.log(inArray(a1, a2));   //["live", "strong"])

var a1 = ["live", "strong", "arp"]
console.log(inArray(a1, a2));    //["arp", "live", "strong"])

var a1 = ["tarp", "mice", "bull"]
console.log(inArray(a1, a2));   // []
```
```javascript
function inArray(array1,array2){
	var array3 = [];
   for(var i = 0 ; i <array1.length ; i++){
   	 var pattern = RegExp(array1[i]);
   	 if(pattern.test(array2) ==true && array1[i]!==undefined){
   	 	array3.push(array1[i])
   	 }
   }
   return array3.sort();
}
```

```javascript
//arr.filter()检测数值元素，并返回符合条件所有元素的数组。
//arr.join()把数组的所有元素放入一个字符串
//arr.indexOf()搜索数组中的元素，并返回它所在的位置。
function inArray(arr1, arr2) {
  return arr1.filter(function(needle) {
    return arr2.some(function(haystack) {
      return haystack.indexOf(needle) > -1;
    });
  }).sort();
}
```
```javascript
function inArray(array1,array2){
    return array1.filter(function(value){return (array2.join('-').indexOf(value))!=-1}).sort();
}
```

###  4.将数组变成电话号码

```
createPhoneNumber([1, 2, 3, 4, 5, 6, 7, 8, 9, 0]) // => returns "(123) 456-7890"
```

```javascript
function createPhoneNumber(numbers){
   var pattern = /(\d{3})(\d{3})(\d{4})/
   pattern.test(numbers.join(''));
   return '('+ RegExp.$1 +')'+ ' ' + RegExp.$2 +'-'+RegExp.$3;
}

console.log(createPhoneNumber([1, 2, 3, 4, 5, 6, 7, 8, 9, 0]));
```

```javascript
function createPhoneNumber(numbers){
  return numbers.join('').replace(/(...)(...)(.*)/, '($1) $2-$3');
}
```

```javascript
function createPhoneNumber(numbers){
  var format = "(xxx) xxx-xxxx";  
  for(var i = 0; i < numbers.length; i++)
  {
    format = format.replace('x', numbers[i]);
  }  
  return format;
}
```

###  5. 找出特殊数字如135 = 1^1 + 3^2 + 5^3

 89 = 8^1 + 9^2 

  135 = 1^1 + 3^2 + 5^3

```javascript
console.log(sumDigPow(1, 10));    //[1, 2, 3, 4, 5, 6, 7, 8, 9]
console.log(sumDigPow(1, 200));   //[1, 2, 3, 4, 5, 6, 7, 8, 9, 89, 135, 175]
console.log(sumDigPow(99, 100));  //[]
```
```javascript
function sumDigPow(a, b) {
  var arr = [];
  for (var i = a; i <= b; i++) {
    var sum = 0;
    for (var j = 0; j <= String(i).length; j++) {
      sum += Math.pow(parseInt(String(i)[j]), j+1);  
      if (sum === i) arr.push(i);
    }
  }
  return arr;
}
```

* forEach方法
```javascript
function sumDigPow(a, b) {
  var c = a, result =[];
  while(c < b){
    var sum = 0;
    (c+'').split('').forEach(function(v, i){
      sum += Math.pow(v, i+1);
    });
    if(c === sum)result.push(c);
    c++;
  }
  return result;
}
```
* forEach方法中的function回调有三个参数：第一个参数是遍历的数组内容，第二个参数是对应的数组索引，第三个参数是数组本身


```javascript
var arr = [1,2,3,4];
arr.forEach(alert);
```
等价于：

```javascript
var arr = [1, 2, 3, 4];
for (var k = 0, length = arr.length; k < length; k++) {
 alert(array[k]);
}
```

比如：
```javascript
var arr = [1,2,3,4];
arr.forEach(function(value,index,array){
    array[index] == value;    //结果为true
    sum+=value;  
    });
console.log(sum);    //结果为 10
```

### 6 url关键字匹配
```javascript
console.log(domainName("http://github.com/carbonfive/raygun"));  //"github" 
console.log(domainName("http://www.zombie-bites.com"));  //"zombie-bites"
console.log(domainName("https://www.cnet.com"));   // "cnet"
console.log(domainName('mailto:user@foo.example''));  // "foo"
```
```javascript
function domainName(url){
    if (/www\./.test(url) == true) {
      url.match(/www\.([\w\-]+)/);
      return RegExp.$1;
    } else if (/\/\//.test(url) == true) {
      url.match(/\/\/([\w\-]+)/);
      return RegExp.$1;
    } else {
      url.match(/([\w\-]+)\./);
      return RegExp.$1;
    }
}
```
```javascript
function domainName(url){
  return url.match(/(?:http(?:s)?:\/\/)?(?:w{3}\.)?([^\.]+)/i)[1];
}
```
```javascript
function domainName(url){
  url = url.replace("https://", '');
  url = url.replace("http://", '');
  url = url.replace("www.", '');
  return url.split('.')[0];
};
```
```javascript
function domainName(url){
  return  url.replace('http://', '')
             .replace('https://', '')
             .replace('www.', '')
             .split('.')[0];
}
```
```javascript
function domainName(url){
  return url.replace(/(https?:\/\/)?(www\.)?/, '').split('.')[0]
}
```
```javascript
function domainName(url){  
  return url.replace(/.+\/\/|www.|\..+/g, '')
}
```
```javascript
function domainName(url){
  var cleanUrl = '';
  var restricted = ['de', 'br', 'fr', 'io', 'it', 'net', 'info', 'tv', 'name', 'users', 'pro', 'img', 'error', 'uk', 'warez', 'www', 'ru', 
  'http', 'https', 'com', 'co', 'jp', 'us', 'net', 'org', 'edu', 'biz', 'za', 'index', 'php', 'kata', 'default', 'html', 'archive', 'error'];
  var splitAddr = url.split(/[/.:]/);
  for(var i = 0; i < splitAddr.length; i++) {
    if(restricted.indexOf(splitAddr[i]) == -1) {
      cleanUrl += splitAddr[i];
    }
  }
  return cleanUrl;
}
```

### 7 数组去重，按大小排序

```javascript
console.log(noRepeat([-2, 1, -3, 4, -1, 2, 1, -5, 4]));
//[4, 2, 1, -1, -2, -3, -5]
console.log(noRepeat([-14, 10, -13, 4, -21, 2, 1, -5, 4])); 
//[10, 4, 2, 1, -5, -13, -14, -21]

//数组去重
function noRepeat(arr) {
  var arrnew = [];
  for (var i = 0; i <arr.length; i++){
    if (arrnew.indexOf(arr[i]) == -1) {
      arrnew.push(arr[i])
    } 
  }

//降序(从大到小)，如果改成升序把“b-a”改成‘a-b’
  function compare(a,b) {
    return b - a;
  }
  
//数组按从大到小排序
  arrnew.sort(compare);
  return arrnew;
}
```
```javascript
//  只是数组去重
var arr = [1,2,3,3,44,55,55,77,2,3,1];
  function noRepeat() {
      var arry = {};
      var j = 0;
      var arr2 = [];
      for (var i = 0;i < arr.length; i++) {
          if (arry[arr[i]] == undefined){ 
        arry[arr[i]] = 1;
        arr2[j++] = arr[i];
    } else if (arry[arr[i] == 1]) {
      continue;
    }
 }
  return arr2
 }
 console.log(noRepeat());
```
### 8 首字母大写，并去掉间隔符

```javascript

console.log(toCamelCase("the-stealth-warrior"));  //  theStealthWarrior (第二个单词开始首大写)
console.log(toCamelCase("The_Stealth_Warrior"))  //  TheStealthWarrior

function toCamelCase(str) {
  if (str == ''){
    return '';
  }
  var strnew = str.replace(/[^a-zA-Z]/g,'-');
  var b = strnew.split('-');
  for (var i = 1; i < b.length; i++) {    //如果从第一个单词开始首字母大写就改成 i=0；
    b[i] = b[i][0].toUpperCase()+b[i].slice(1);  //首字母大写

  }
  return b.join('');
}
```
```javascript
function toCamelCase(str){
      var regExp=/[-_]\w/ig;
      return str.replace(regExp,function(match){
            return match.charAt(1).toUpperCase();
       });
}
```
```javascript
function toCamelCase(str){
  return str.replace(/([-_])(\w)/g, function(match,dash,letter) { return letter.toUpperCase() });
}
```
```javascript
function toCamelCase(str) {
  return str.replace(/[_-][A-Za-z]/g, function(match) {return match[1].toUpperCase();});
}
```
```javascript
function toCamelCase(str){
  var strArray;
  if (str.indexOf('-') !== -1){ 
    strArray = str.split('-');
  } else {
    strArray = str.split('_');  
  }
  var camelCase = strArray[0];
  for (var i=1, len=strArray.length; i < len; i++){
    var capitalized = strArray[i].substr(0, 1).toUpperCase() + strArray[i].slice(1);
    camelCase += capitalized;
  }
  return camelCase;
  

}
```
```javascript
function toCamelCase(str){
 str = str.split(/[-_]/);
 for(var i = 1;i < str.length;i++){
 
   str[i] = str[i].charAt(0).toUpperCase().concat(str[i].slice(1));
 
 }
 return str.join("");
}
```

### 9 求一个数能否开方

```javascript
console.log(isPP(4));   // [2,2], "4 = 2^2"
console.log(isPP(9)); //  [3,2], "9 = 3^2"
console.log(isPP(5)); // null
console.log(isPP(81)); //[3,4]

function isPP(n){
  for (var m = 2; m <= Math.floor(Math.sqrt(n)); ++m) {
    var k = Math.round(Math.log(n) / Math.log(m))
    if (Math.pow(m, k) == n) return [m, k];
  }
  return null;
}
```
```javascript
function isPP(n) {
  for (var m = 2; m * m <= n; ++ m)
    for (var k = 2; Math.pow(m, k) <= n; ++ k)
      if (Math.pow(m, k) == n) return [m, k];
  return null;
}
```
```javascript
var isPP = function(n){
  var x=Math.sqrt(n);
  if (x%1==0) return [x,2];
  for (var i=2;i<x;i++) {
    if (n%i==0){
      for (var j=0,tmp=i;tmp<=n;tmp*=i,j++){
        if (tmp==n) return [i,j+1];
      }
    }
  }
  return null;
}
```
```javascript
var isPP = function(n){
  for(var i = Math.floor(Math.log(n)/Math.log(2)); i > 1; i--) {
    var rt = Math.round(Math.pow(n, 1/i));
    if(Math.pow(rt, i) === n) {
      return [rt, i];
    }
  }
  return null;
}
```

### 10 将数组里的0放到数组后面

```javascript
console.log(moveZeros([false,10,0,1,2,0,1,3,"a"])); 
// returns[false,1,1,2,1,3,"a",0,0]

function moveZeros(arr) {
  var j = 0;
  for (var i = 0; i < arr.length; i++) {
    if(arr[i] === 0) {
      arr.splice(i,1);
      j += 1;
      i = i - 1;
    }
  }
  for (var k = 0; k < j; k++){
    arr.push(0);
  }
  return arr;
}
```

```javascript
function moveZeros(arr) {
  return arr.filter(function(x) {return x !== 0}).concat(arr.filter(function(x) {return x === 0;}));
}
```
```javascript
function moveZeros(arr) {
  var filtedList = arr.filter(function (num){return num !== 0;});
  var zeroList = arr.filter(function (num){return num === 0;});
  return filtedList.concat(zeroList);
}
```
```javascript
function moveZeros(arr) {
  var zeroes = [];
  var withoutZeros = arr.filter(function(value){
    if(value === 0) {
      zeroes.push(0);
      return false;
    }
    return true;
  });
  
  return withoutZeros.concat(zeroes);
}
```
```javascript
function moveZeros(arr) {
  return arr.reduceRight(function(prev, curr) {
    if (curr !== 0) {
      prev.unshift(curr);
    }
    else {
      prev.push(curr);
    }
    return prev;
  }, []);
}
```
```javascript
function moveZeros(arr) {
  var result = [];
  var zeros = [];
  for (var i in arr) {
    if (arr[i] === 0) {
      zeros.push(arr[i]);
    } else if (arr[i] !== 0) {
      result.push(arr[i]);
    }
  }
  return result.concat(zeros);
}
```
### 11  add(2)(3)(4) //输出9

```javascript
function add(x) {
    var sum = x;
    var tmp = function (y) {
        sum = sum + y;
        return tmp;
    };
    tmp.toString = function () {
        return sum;
    };
    return tmp;
}
console.log(add(1)(2)(3));  //6
console.log(add(1)(2)(3)(4));   //10
```
### 12 two sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

```javascript
console.log(twoSum([2, 7, 11, 15],22));//[1, 3]
console.log(twoSum([2, 7, 11, 15],9));//[0, 1]
```
```javascript
function twoSum(nums, target) {
  var len = nums.length
  var sum;
  var result;
    for(var i = 0; i <len; i++ ){
       for(var j = i+1 ; j < len ; j++){
        sum = nums[i] + nums[j]
        if ( sum === target) {
          result = [i,j]
          return result;
        }
       }
    }
};
```
```javascript
var twoSum = function(nums, target) {
    var len = nums.length;
    var exist = {}
    for(var i = 0; i < len; i++){
       if (exist[target - nums[i]] !== undefined){
           return [exist[target-nums[i]], i];
       }
       exist[nums[i]] = i
    }
};
```
### 13 将数组里的0放到数组后面

Write an algorithm that takes an array and moves all of the zeros to the end, preserving the order of the other elements.

```javascript
console.log(moveZeros([false,10,0,1,2,0,1,3,"a"])); 
// returns[false,1,1,2,1,3,"a",0,0]

function moveZeros(arr) {
  var j = 0;
  for (var i = 0; i < arr.length; i++) {
    if(arr[i] === 0) {
      arr.splice(i,1);
      j += 1;
      i = i - 1;
    }
  }
  for (var k = 0; k < j; k++){
    arr.push(0);
  }
  return arr;
}
```

```javascript
function moveZeros(arr) {
  return arr.filter(function(x) {return x !== 0}).concat(arr.filter(function(x) {return x === 0;}));
}
```
```javascript
function moveZeros(arr) {
  var zeroes = [];
  var withoutZeros = arr.filter(function(value){
    if(value === 0) {
      zeroes.push(0);
      return false;
    }
    return true;
  });
  
  return withoutZeros.concat(zeroes);
}
```
```javascript
function moveZeros(arr) {
  return arr.reduceRight(function(prev, curr) {
    if (curr !== 0) {
      prev.unshift(curr);
    }
    else {
      prev.push(curr);
    }
    return prev;
  }, []);
}
```
```javascript
function moveZeros(arr) {
  var result = [];
  var zeros = [];
  for (var i in arr) {
    if (arr[i] === 0) {
      zeros.push(arr[i]);
    } else if (arr[i] !== 0) {
      result.push(arr[i]);
    }
  }
  return result.concat(zeros);
}
```
```javascript
function moveZeros(arr) {
  return arr.reverse().reduce(function(ret,v){
    return v === 0 ? ret.push(v) : ret.unshift(v), ret;
  },[]);
}
```
```javascript
function moveZeros(arr) {
  var ret = [[], []];
  arr.forEach(function (item) {
    ret[+(item === 0)].push(item);
  });
  return ret[0].concat(ret[1]);
}
```
### 14 把0放到后面

You are NOT allowed to use any temporary arrays or objects. You are also not allowed to use any Array.prototype or Object.prototype methods.

要求不能使用array prototype的方法

```JavaScript
console.log(removeZeros([7, 2, 3, 0, 4, 6, 0, 0, 13, 0, 78, 0, 0, 19, 14]));
//[7, 2, 3, 4, 6, 13, 78, 19, 14, 0, 0, 0, 0, 0, 0]
```
```JavaScript
function removeZeros(array) {
    var end = array.length;
    for (var i = 0; i < end; i++) {
        if (array[i] === 0 || array[i] === "0") {
            arrayShiftToEnd(array, i);
            i--;
            end--;
        }
    }
    return array;
}

function arrayShiftToEnd(array, n) {
    var end = array[n]
    for(var i = n; i <  array.length; i++) {
        array[i] = array[i + 1]
    }
    array[array.length - 1] = end;

    return array
}
```
```JavaScript
function removeZeros(array) {
    if (array.length === 0) return array;
    var zeroCount = 0; //keeps track of zeros so we know when to exit for loop
    for (var i = 0, len = array.length; i < len; i++) {
        if (array[i] === 0 || array[i] === '0') { //shuffle numbers back one space and put zero at end
            zeroCount += 1;

            for (var j = i + 1; j < len; j++) {//this looks for non-zero after i of array
                var itemToMoveUp = array[j]; //non-zero number at end to swap places with zero num
                array[j] = array[j-1]; //set index of num we will move up to zero
                array[j-1] = itemToMoveUp; //now the zero has been swapped for a non-zero
            }

            i -= 1; //move index back one because next item is now one index lower
        }
        if (i + 1 + zeroCount >= len){ //if only zeros that were moved are left -> end
            return array;
        }
    }
}
```
```JavaScript
function removeZeros(array) {
  const head = []
  const tail = []
  for (const e of array) {
    if (e === 0 || e === "0") {
      tail[tail.length] = e
    } else {
      head[head.length] = e
    }
  }
  return [...head, ...tail]
}
```
```JavaScript
function removeZeros(array) {
    var limit = array.length;
    var tmp;
    for (var i = 0; i < limit; i++) {
        if (array[i] === 0 || array[i] === '0') {
            tmp = array[i];
            for (var j = i--; j < array.length-1; j++) {
                array[j] = array[j+1];
            }
            array[array.length-1] = tmp;
            limit--;
        }
    }
    return array;
}
```
```JavaScript
function removeZeros(arr) {
  for(var jmax=arr.length, i=jmax-2; i>-1; --i)
    if(''+arr[i] === '0')
      for(var j=(--jmax, i+1); j<=jmax; j++)
        arr[j-1] = [ arr[j], arr[j]=arr[j-1] ][0]
  return arr;
}
```
```JavaScript
function removeZeros(arr) {
    for (var i = 0, s = false, c = 0; i < arr.length - 1; i++)
        ("" + arr[i] == "0" && "" + arr[i + 1] != "0") &&
        (c=arr[i], arr[i]=arr[i + 1], arr[i + 1]=c, i = 0, s = true);
    return !s ?arr :removeZeros(arr);
}
```
```JavaScript
function removeZeros(array) {
  var zeros = [];
  var normal = [];
  for(var i = 0 ; i <= array.length-1; i++){
    if(array[i] === '0' || array[i] === 0) zeros[zeros.length] = array[i];
    else normal[normal.length] = array[i];
  }
  for(var i = 0 ; i <= zeros.length-1; i++){
    normal[normal.length] = zeros[i];
  }  
  
  return normal;
}
```
```JavaScript
function isZero (n) {
  return n === 0 || n === '0';
}
function removeZeros(array) {
  var i, j, tmp;
  for (i = array.length-1; i > 0; i--)
    for (j = 1; j <= i; j++)
      if (isZero(array[j-1]) && !isZero(array[j])) {
        tmp = array[j-1];
        array[j-1] = array[j];
        array[j] = tmp;
      }
  return array;
}
```
```JavaScript
function removeZeros(array) {
  function zero(e) {
    return String(e) === '0';
  }
  
  for (var i = array.length - 1; i --> 0;) {
    var e = array[i];
    if (!zero(e)) continue;
    for (var j = i + 1; j < array.length; j++) {
      var f = array[j];
      if (zero(f)) break;
      array[j - 1] = f;
      array[j] = e;
    }
  }
  return array;
}
```

### 15 字符串变成数字相加，包括大数字

```javascript
console.log(sumStrings('712569312664357328695151392', '8100824045303269669937')); 
 // '712577413488402631964821329'
console.log(sumStrings('1', '2')); 
 // '3'
```

```javascript
String.prototype.reverse = function() {
  return this.split('').reverse().join('');
}

function sumStrings(a,b) {
  a = a.reverse(); b = b.reverse();
  var carry = 0;
  var index = 0;
  var sumDigits = [];
  while (index < a.length || index < b.length || carry != 0) {
    var aDigit = index < a.length ? parseInt(a[index]) : 0;
    var bDigit = index < b.length ? parseInt(b[index]) : 0;
    var digitSum = aDigit + bDigit + carry;
    sumDigits.push((digitSum % 10).toString());
    carry = Math.floor(digitSum / 10);
    index++;
  }
  sumDigits.reverse();
  while (sumDigits[0] == '0') sumDigits.shift();
  return sumDigits.join('');
}
```
```javascript
function sumStrings(a, b) {
  var res = '', c = 0;
  a = a.split('');
  b = b.split('');
  while (a.length || b.length || c) {
    c += ~~a.pop() + ~~b.pop();
    res = c % 10 + res;
    c = c > 9;
  }
  return res.replace(/^0+/, '');
}
```
```javascript
function sum(n1, n2) {
  return (parseInt(n1) || 0) + (parseInt(n2) || 0);
}

function sumStrings(a,b) { 
  a = a.split("").reverse();
  b = b.split("").reverse();
  total = [];
  var length = (a.length > b.length) ? a.length : b.length;
  
  //make the sum digit by digit
  for (var i = 0; i < length; i++) {
    s = sum(a[i], b[i]);
    total[i] = sum(total[i], s);
    if (total[i]>9) {
      total[i] -= 10;
      total[i+1] = 1;
    }
  }
  
  //remove fruitless zero
  if (total[total.length-1] == 0) 
    total[total.length-1] = "";
    
  //reverse the array and return the string
  return total.reverse().join("");
}
```
```javascript
function sumStrings(a, b) {
  a = "0" + a.replace(/\D/g,"");
  b = "0" + b.replace(/\D/g,"");
  var c = 0;
  var result = "";

  for(var i=b.length-a.length; i>0; --i) a = "0" + a;
  for(var i=a.length-b.length; i>0; --i) b = "0" + b;

  for(var i=a.length-1; i>-1; --i) {
    c = +a[i] + +b[i] + c;
    result = (c%10) + result;
    c = Math.floor(c/10);
  }
  
  return result.replace(/^0+/,"");
}
```
```javascript
function sumStrings(a,b) { 
  var res="",c=0;
  a=a.split("");b=b.split("");
  while(a.length||b.length||c){
    c=+(a.length>0?a.pop():0) + +(b.length>0?b.pop():0)+c;
    res=(c%10).toString()+res;
    c=Math.floor(c/10);
  }
  res=res.replace(/^[0]*/g,"");
  return res;
}
```
```javascript
var sumStrings = function addIntStrings(a, b){
   var nal = 15, //native addition limit
       max = Math.max(a.length, b.length),
       to,
       from = -nal,
       overflow = '',
       result = '',
       temp;
   function nativeAdd(o, a, b){
      var val = (+o + +a + +b).toString();
      return [ val.slice( 0, -nal ) , val.slice( -nal ) ];
   }
   while(!(-to > max)){
      temp = nativeAdd(overflow, a.slice( from, to ), b.slice( from , to ));
      overflow = temp[0], result = temp[1] + result;
      to = from;
      from = from - nal;
   }
   return result;
}
```
```javascript
function sumStrings(a, b) {
  a = a.split('').reverse(), b = b.split('').reverse();
  return Array.apply(null, new Array(1 + Math.max(a.length, b.length))).reduce(function (acc, _, i) {
    var n = (parseInt(a[i], 10) || 0) + (parseInt(b[i], 10) || 0) + acc[1];
    return [(n % 10) + acc[0], Math.floor(n / 10)];
  }, ['', 0])[0].replace(/^0+/, '');
}
```
```javascript
function sumStrings(a,b) { 
   var A = a.replace(/^0*/, "").split("").reverse();
   var B = b.replace(/^0*/, "").split("").reverse();
   var res = "";
   var tenths = 0;
   while (A.length>0 || B.length>0) {
     var a0 = A.length==0 ? 0 : +A[0];
     var b0 = B.length==0 ? 0 : +B[0];
     var d = a0 + b0 + tenths;
     tenths = d>9 ? 1 : 0;
     res = (d%10) + res;
     A = A.slice(1);
     B = B.slice(1);
   }
   if (tenths) res = "1"+res
   return res;
}
```
### 16  [1, 3, 4, 7, 9, 10, 13, 15, 19, 21, 22, 27, ...]

1. The number `u(0) = 1` is the first one in `u`.
2. For each `x` in `u`, then `y = 2 * x + 1` and `z = 3 * x + 1` must be in `u` too.
3. There are no other numbers in `u`.

Ex: `u = [1, 3, 4, 7, 9, 10, 13, 15, 19, 21, 22, 27, ...]`

1 gives 3 and 4, then 3 gives 7 and 10, 4 gives 9 and 13, then 7 gives 15 and 22 and so on..

```javascript
console.log(dblLinear(10)); // 22
console.log(dblLinear(11)); // 27
```
```javascript
function dblLinear(n) {
  var ai = 0, bi = 0, eq = 0;
  var sequence = [1];
  while (ai + bi < n + eq) {
    var y = 2 * sequence[ai] + 1;
    var z = 3 * sequence[bi] + 1;
    if (y < z) { sequence.push(y); ai++; }
    else if (y > z) { sequence.push(z); bi++; }
    else { sequence.push(y); ai++; bi++; eq++; }
  }
  return sequence.pop();
}
```
```javascript
function dblLinear(n) {
  
    var u = [1], pt2 = 0, pt3 = 0; //two pointer
    
    for(var i = 1;i<=n;i++){
      u[i] = Math.min(2* u[pt2] + 1, 3*u[pt3] + 1);
      if(u[i] == 2 * u[pt2] + 1) pt2++;
      if(u[i] == 3 * u[pt3] + 1) pt3++;
    }

    return u[n];
  
}
```

### 17.两个数字，一字符（+，-，*，/，分别代表加、减、乘、除）

// 调用函数举例：func(2, 6, '+'); //传入一个整数, 输出结果：8

    function func(a,b,c){
    	if(c === '+'){
    		return a + b;
    	}else if(c === '-'){
    		return a - b;
    	}else if(c ==='/'){
    		return (a/b).toFixed(2);
    	}else if(c === '*'){
    		return a*b;
    	}else{
    		return false;
    	}
    }
    console.log( func(10,3,'/') ); // 3.33
    console.log( func(20,2,'*') ); // 40
    
    function func(a,b,c){
    	switch(c){
    		case '+':
    			return a+b;
    			break;
    		case '-':
    			return a-b;
    			break;
    		case '/':
    			return (a/b).toFixed(2);
    			break;
    		case '*':
    			return a*b;
    			break;
    		default:
    			return false;
    	}
    }
    console.log( func(10,3,'/') ); // 3.33
    console.log( func(20,2,'*') ); // 40

### 18.数组逆序排序
```javascript
var arr_1 = [1,2,3,4,5,6,7,8];
function reversal( good ){
	var happy = [];
	var j = good.length - 1;
	for(var i = 0; i < good.length; i++){
		happy[j] = good[i];
		j--;
	}
	return happy;
}
var arr_2 = reversal(arr_1);
console.log(arr_2);   //[8, 7, 6, 5, 4, 3, 2, 1]
```
```javascript
var arr =['a','b'];
arr.reverse();//reverse用于将数组逆序
console.log(arr);  //['b','a']
```
###  19.DNAStrand（A-T,C-G） < key,value >键值对

Examples

```
DNAStrand ("ATTGC") // return "TAACG"
DNAStrand ("GTAT") // return "CATA"
```

方法一:使用正则配对

```javascript
function DNAStrand(dna){
  return dna.replace(/A/g, 't').replace(/T/g, 'a').replace(/C/g, 'g').replace(/G/g, 'c').toUpperCase();
}

console.log(DNAStrand("ATTGC"));//TAACG
console.log(DNAStrand("GTAT"));//CATA
```

方法二：使用 < key,value >键值对

```javascript
var pairs = {'A':'T','T':'A','C':'G','G':'C'};
function DNAStrand(dna) {
  return dna.replace(/./g, function(y) {
    return pairs[y];
  });
}

console.log(DNAStrand("ATTGC"));//TAACG
console.log(DNAStrand("GTAT"));//CATA
```

方法三

- split() 方法用于把一个字符串分割成字符串数组( 如："2:3:4:5".split(":") //将返回["2", "3", "4", "5"])
- map() 方法返回一个新数组，数组中的元素为原始数组元素按顺序依次调用函数处理后的值

```javascript
var pairs = {'A':'T','T':'A','C':'G','G':'C'};
function DNAStrand(dna){
  return dna.split('').map(function(y){ return pairs[y] }).join('');
}

console.log(DNAStrand("ATTGC"));//TAACG
console.log(DNAStrand("GTAT"));//CATA
```

### 20.阶乘5! = 5x4x3x2x1
```javascript
function func(num){
  if(num <0){
    return -1;
  }
  if(num == 0){
    return 1;
  }
  return num*(func(num-1));
}
console.log(func(5));
```
```javascript
function func(n){
	var temp = 1;
	for(var i = n; i >= 1; i--){
        temp = temp * i;
	}
	return temp;
}
console.log(func(1));
```
```javascript
var factorial = function(num){
  if(num <= 1){
    return 1;
  }else {
    return num * factorial(num-1);
  }
}
console.log(factorial(3)); //6
```
```javascript
//递归法
function func(n){
    if(n===1){
    	return 1;
    }
     return func(n-1)*n;   
}
console.log(func(5));
```
### 21.费波那契数列
已知faibonacai(费波那契)数列的前几个数分别为1,1,2,3,5,8,13,……,编程求此数列的前n（n＞＝５）项。
输入说明：一个整数n（>=5 and <=22），表示数列的前n个数。
输出样例 ：
1
1
2
3
5
```javascript
 function fn(n){

	if(n===1 || n===2){
		return 1;
	}	
	return fn(n-1)+fn(n-2);   
}
function func(n){
	for(var i = 1; i <=n; i++){
		document.write(fn(i)+'</br>');
	}
}
console.log(func(8));   //递归算法
```
```javascript
function func(n){
  var n1 = 1;
  var n2 = 1;
  var n3 = 0;
  document.write(n1+'</br>'+n2+'</br>');
  for (i = 1; i <=n-2; i++){
       n3 = n1 + n2;
      document.write(n3+'</br>');
        i += 1;
        if(i<=n-2){
          n1 = n3 + n2;  
	       document.write(n1+'</br>');   
           i += 1; 	
        }
         if(i<=n-2){      
       n2 = n3 + n1;
	       document.write(n2+'</br>');   
        }
  }
}
console.log(func(8));
```
```javascript
//如果是用数组来表示而不是每行输出一个，就可以用下面的算法
function func(n){
	var arr = [1,1];
   for(var i = 1; i <= n-2; i++){
   	arr.push((arr[i]) + (arr[i-1]));
   }
   return arr;
}
console.log(func(7));// [1, 1, 2, 3, 5, 8, 13]
```
```javascript
function func(n){
   if(n=1||n=2){
      return 1;     
    } else {
     return func(n-1)+func(n-2);
    }
}
```
### 22.求随机数

*求随机数
*求1-10随机一个整数
```javascript
var num = Math.floor(Math.random()*10+1);
console.log(num);
```
* 求2-10随机一个整数
```javascript
var num = Math.floor(Math.random()*9+2);
console.log(num);
```
* 求lowerValue-upperValue随机一个整数
```javascript
function selecFrom(lowerValue,upperValue){

	var choices = upperValue - lowerValue + 1;
	return Math.floor(Math.random() * choices + lowerValue);
}
var num = selecFrom(2,10)//介于2-10之间的整数，包括2、10
console.log(num);
//求数组中随机取出一个项
var colors = ['red','blue','green','orange','yellow','black'];
var color = colors[selecFrom(0, colors.length-1)];
console.log(color);
```
### 23. 四位数abcd ,  ( ab + cd )( ab + cd ) = abcd 

其中，ab代表两位数字组成整数，即10*a+b，而abcd代表四位数字的4位整数，即1000*a+100*b+10*c+1*d ,两个括号是乘积的关系。

没有输入，输出abcd，从小到大，一行一个。

```javascript
function func(){
    var j = 0, a = 0 , b = 0, c = 0, d = 0;
	for(var i = 1000; i <= 9999; i++){
           j = i.toString();
           a = parseInt(j[0]);
           b = parseInt(j[1]);
           c = parseInt(j[2]);
           d = parseInt(j[3]);
     var temp = Math.pow(((a*10+b)+(c*10+d)),2); 
        if(temp ===i){              //Math.pow(2,4),相当2^4=16;
           document.write(temp+'</br>');
        }
    }
}
func();  
```

2025
3025
9801

###  24.蛇形数字三角
**内容：**

输入行数，如3输出如下图形
4
2 5
1 3 6

**示例：** 

```javascript
func(3);
```

**输出样例 ：**

```
4
2 5
1 3 6
```

```javascript
// 代码
function func(n){
  for(var i = n-1; i >=0; i--){
	var a = 1;
	var b = 1;
    var c = ''; 
	for(var j = 1; j <= i; j++){
        a = a + j;
	}
	 b = b + a -1;
	for(var k = i + 1; k <= n-1; k++){	
     b = b + k + 1;
     c = c + b +'&nbsp';
	}
	document.write(a +'&nbsp'+ c + '</br>');
  }
}
	console.log(func(8));
```

```
//输出
29 
22 30 
16 23 31 
11 17 24 32 
7 12 18 25 33 
4 8 13 19 26 34 
2 5 9 14 20 27 35 
1 3 6 10 15 21 28 36
```
### 25.键入一个自然数 ，求这个自然数的所有约数之和
```javascript
function func(num1){
	var temp =0;
	for(var i = 1; i <=num1;i++){
		if(num1 % i == 0){
	       temp = temp + i;
		}
	}
    return temp;
}
console.log( func(6) );// 输出结果：12
```
### 26.  计算数组元素中字母‘a'或‘A’出现的次数。

输出：一个整数，为a或者A字符出现次数和。

```javascript
function func(arr){
	var temp = 0;
	for(var i = 0 ; i < arr.length; i++){
		if(arr[i] === 'A'|| arr[i] === 'a'){
             temp = temp + 1;
		}
	}
	return temp;
}
var num = ['f','a','c','c','d','A','a','d'];
console.log( func(num) );  //  3
```
注意，如下如果想计算多少个1，不能用 ==，1和true能相互转换，就会输出4，本来应该是3，把  arr[i] === 1 ,则正确输出3
```javascript
function func(arr){
	var temp = 0;
	for(var i = 0 ; i < arr.length; i++){
		if(arr[i] == 1){
	         temp = temp + 1;
		}
	}
	return temp;
}
var num = ['f','a','c',true,1,1,1,0,0];
console.log( func(num) );    //  4
```

注意，===里面 ‘1’和1是有区别的，无法全等
```javascript
function func(arr){
	var temp = 0;
	for(var i = 0 ; i < arr.length; i++){
		if(arr[i] === '1'){
	         temp = temp + 1;
		}
	}
	return temp;
}
var num = ['f','a','c',true,1,1,1,0,0,0,0];
console.log( func(num) );   //   0
```
### 27.求输入的一个整数的各位数字之和。

比如输入一个：3334，那么得到的结果是 3+3+3+4 = 13
```javascript
function func(num){
	var sum = 0;
	var temp = 0;
	while(num>0){
		temp = num % 10;
		num = Math.floor(num / 10);
		sum += temp;
	}
	return sum;
}
var sum = func(2147483646);
console.log(sum); // 45
```

```javascript
function func(num){
	var arr = num.toString();          //转换为字符串
	var temp = 0;
    var box = 0;
	for( var i = 0; i < arr.length ; i++){
	    box = parseInt(arr[i]，10); //转换为整数，10代表是十进制
                            //parseFloat就是转换小数,只解析十进制
		  temp = temp + box; 
	}
     return temp; 
}
var sum = func(2147483646);
console.log(sum); // 45
```
###  28.减肥数字

每个体重数字，按各个数位数字之和，从小到大排列

```JavaScript
console.log(orderWeight("56 65 74 100 99 68 86 180 90"));//100 180 90 56 65 74 68 86 99
```
```JavaScript
function orderWeight(strng) {
  return strng
    .split(" ")
    .map(function(v) {  
      return {
        val: v,
        key: v.split("").reduce(function(prev, curr) {
          return parseInt(prev) + parseInt(curr);
        }, 0)
      };
    })
    .sort(function(a, b) {
      return a.key == b.key 
        ? a.val.localeCompare(b.val)
        : (a.key - b.key);
    })
    .map(function(v) {
      return v.val;
    })
    .join(" ");
}
```
```JavaScript
function orderWeight(s) {
  return s.split(' ').sort((a,b) => sum(a) - sum(b) || a.localeCompare(b)).join(' ');
}
function sum(s) { return s.split('').reduce((s,v) => s + +v, 0); }
```
```JavaScript
function orderWeight(strng) {
  return strng.split(" ").sort(function f(a, b){ 
    return eval(a.split("").join("+")) - eval(b.split("").join("+")) + ([a, b].sort()[1] == a ? 0.1 : -0.1);
  }).join(" ");
}
```
```JavaScript
function orderWeight(strng) {
    
    var w = function(n) {
      
        var s = 0;

        n.toString().split('').forEach(function(v, k) {
            s += +v;  
        });
        
        return s;
  
    };

    return strng.split(' ').sort(function(a, b) {
          
        return w(a) == w(b) ? (a > b ? 1 : -1 ) : w(a) - w(b);

    }).join(' ');

}
```
```JavaScript
function digitSum(str) {
  return str.split('').reduce(function(s, e) { 
    return s + parseInt(e); 
  }, 0);
}

function orderWeight(str) {
    return str.split(' ').sort(function(a, b) {
      return digitSum(a) - digitSum(b) || a.localeCompare(b);
    }).join(' ');
}
```
###  29.  Pig latin is cool

#### Description:

Move the first letter of each word to the end of it, then add 'ay' to the end of the word.

将每个单词第一个字母放到该单词后面，后面再加ay，得到新句子。

``` JavaScript
console.log(pigIt('Pig latin is cool')); // igPay atinlay siay oolcay
```

方法一：使用正则

```JavaScript
function pigIt(str){
  return str.replace(/(\w)(\w*)(\s|$)/g, "\$2\$1ay\$3")
}
```

方法二：

```JavaScript
function pigIt(str){
  return str.split(' ').map(function(el){
    return el.slice(1) + el.slice(0,1) + 'ay';
  }).join(' ');
}
```
```JavaScript
function pigIt(str){
  var words = str.split(" ");
  for (w in words) {
    words[w] = words[w].slice(1) + words[w].slice(0,1) + "ay"
  }
  return words.join(" ");
}
```
```JavaScript
function pigIt(str) {
    return str.split(" ").map(function (e) {return e.slice(1) + e.charAt(0) + 'ay'}).join(' ');
}
```
### 30.画出一个星罗密布
```javascript
func(3);
*****$
***$$$
*$$$$$
func(4);
*******$
******$$
*****$$$
****$$$$
***$$$$$
**$$$$$$
*$$$$$$$
```
```javascript
function func(b){
	var n = 2*b-1;
	var x = '';
	var y = '';
 for(var k = n; k >0; k--){
 		var x = '';
	    var y = '';
	for( i = k; i >0; i--){
		x = x + '*';
	}
	for( j = 0; j <= n-k; j++){
		y = y + "$";
	}
	document.write(x + y + '</br>');
 } 
}
func(5);
```
###  31.判断一个数是否能开方得到整数，若不能返回-1，若能则返回该整数大1的整数的平方值，
```javascript
function findNextSquare(sq) {
  return Math.sqrt(sq)%1? -1 : Math.pow(Math.sqrt(sq)+1,2);
}
```

```javascript
function findNextSquare(sq) {
  var number = Math.sqrt(sq);
  if(Math.round(number) === number) {  //四舍五入得到的书是否是它本身
    return Math.pow(++number, 2)
  }
  return -1;
}  
```
### 32.将数组[a,b,c,d,e],变成a-b-c-d-e
```javascript
var box = [4,6,7,4,56,43,];
var pox = box.join('-');
var vox = box.join('||');
console.log(pox);
console.log(vox);
```
### 33.  [1, 3, 4, 7, 9, 10, 13, 15, 19, 21, 22, 27, ...]

1. The number `u(0) = 1` is the first one in `u`.
2. For each `x` in `u`, then `y = 2 * x + 1` and `z = 3 * x + 1` must be in `u` too.
3. There are no other numbers in `u`.

Ex: `u = [1, 3, 4, 7, 9, 10, 13, 15, 19, 21, 22, 27, ...]`

1 gives 3 and 4, then 3 gives 7 and 10, 4 gives 9 and 13, then 7 gives 15 and 22 and so on..

```javascript
function dblLinear(n) {
  var ai = 0, bi = 0, eq = 0;
  var sequence = [1];
  while (ai + bi < n + eq) {
    var y = 2 * sequence[ai] + 1;
    var z = 3 * sequence[bi] + 1;
    if (y < z) { sequence.push(y); ai++; }
    else if (y > z) { sequence.push(z); bi++; }
    else { sequence.push(y); ai++; bi++; eq++; }
  }
  return sequence.pop();
}
```
```javascript
function dblLinear(n) {
  
    var u = [1], pt2 = 0, pt3 = 0; //two pointer
    
    for(var i = 1;i<=n;i++){
      u[i] = Math.min(2* u[pt2] + 1, 3*u[pt3] + 1);
      if(u[i] == 2 * u[pt2] + 1) pt2++;
      if(u[i] == 3 * u[pt3] + 1) pt3++;
    }

    return u[n];
  
}
```
```javascript
function dblLinear(n) {
      var h = [];
      var x2 = 1, x3 = 1;
      var i = 0, j = 0;
      for (var index = 0; index < n+1; index++)
      {
          h[index] = x2 < x3 ? x2 : x3;
          if (h[index] == x2) x2 = 2 * h[i++] + 1;
          if (h[index] == x3) x3 = 3 * h[j++] + 1;
      }
      return h[n];
    
}
```
```javascript
var cache = [1], [i2,i3] = [0,0];
function dblLinear(n) {
  while (cache.length <= n) {
    while (calc2(i2) <= cache[cache.length - 1]) i2++;
    while (calc3(i3) <= cache[cache.length - 1]) i3++;
    cache.push(Math.min(calc2(i2), calc3(i3)));
  }
  return cache[n];
}
function calc2(n) { return 2 * cache[n] + 1; }
function calc3(n) { return 3 * cache[n] + 1; }
```
```javascript
function dblLinear(n) {
  var u = [1],
      bases = [2, 3],
      indexes = [0, 0],
      next;
  while (u.length <= n) {
    next = Math.min.apply(Math, indexes.map((index, i) => bases[i] * u[index] + 1));
    u.push(next);
    indexes = indexes.map((index, i) => index + (bases[i] * u[index] + 1 === next));
  }
  return u[n];
}
```
```javascript
var dpArray = [1];
var lastProcessed = 0;

function dblLinear(n) {
  var x = 0;
  var y = 0;
  var i = 0;
  while (lastProcessed <= n) {
    x = dpArray[lastProcessed] * 2 + 1;
    y = dpArray[lastProcessed] * 3 + 1;
    for (i = dpArray.length - 1; i >= 0; i--) {
      if (dpArray[i] === x) {
        break;
      }
      else if (dpArray[i] < x) {
        dpArray.splice(i + 1, 0 , x);
        break;
      }
    }
    for (i = dpArray.length - 1; i >= 0; i--) {
      if (dpArray[i] === y) {
        break;
      }
      else if (dpArray[i] < y) {
        dpArray.splice(i + 1, 0 , y);
        break;
      }
    }
    lastProcessed++;
  }
  return dpArray[n];
}
```
```javascript
function Heap(){
  this.level = -1;
  this.nums = [];
  this.push = function(num){
    for(var i = this.nums.length - 1; i >= 0; i--){
      if(this.nums[i] <= num)
        break;
    }
    if(this.nums[i] == num)
      return;
    this.nums.splice(i + 1, 0, num);
  };
  this.get = function(i){
    return this.nums[i];
  };
}

heap = new Heap();
heap.push(1);
heap.level++;

function dblLinear(n){
  var level = heap.level;
  for(var i = level; i < n; i++){
    var num = heap.get(i);
    heap.push(2 * num + 1);
    heap.push(3 * num + 1);
    heap.level++;
  }
  return heap.get(n);
}
```