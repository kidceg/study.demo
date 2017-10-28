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





