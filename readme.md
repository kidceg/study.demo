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
 return url.replace("www.","").match(/[\w-]+(?=\.)/)[0];
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