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



