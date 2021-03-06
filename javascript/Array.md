
## 变异

```
push()	数组的新长度 = 数组.push(元素);

---向数组的最后面插入一个或多个元素
```

```
pop()	  被删除的元素 = 数组.pop(); 

---删除数组中的最后一个元素
```

```
unshift()	数组的新长度 = 数组.unshift(元素);

---在数组最前面插入一个或多个元素
```


```
shift()	被删除的元素 = 数组.shift();

---删除数组中的第一个元素
```

## 遍历

```
数组/boolean/无 = 数组.every/filter/forEach/map/some(function(element,index,arr){程序和返回值；}
```

```
every()、对数组中每一项运行回调函数，如果都返回true，every就返回true；如果有一项返回false，则停止遍历，此方法返回false。
```

```
filter()、Array.prototype.filter(function(item, index){})，对数组中每一项运行回调函数，返回该函数的结果，组成的新数组return
```

```
forEach()、需要兼容IE8，参数1，就是当前正在遍历的元素，参数2，就是当前正在遍历的元素的索引，参数3，就是正在遍历的数组
```

```
map()、对数组中每一项运行回调函数，返回该函数的结果，组成的新数组return
```

```
some()、对数组中每一项运行回调函数，只要有一项返回true，则停止遍历，此方法返回true。
```

**数组的常见方法**

将伪数组转化成真数组

```
array = Array.from(arrayLike)
```

```
slice()	新数组 = 原数组.slice(开始位置的索引, 结束位置的索引);
```

从数组中提取指定的一个或多个元素，返回结果为新的数组

```
splice()新数组 = 原数组.splice(起始索引index, 需要删除的个数, 第三个参数, 第四个参数...);
```

从数组中删除指定的一个或多个元素，返回结果为新的数组

```
concat()新数组 = 数组1.concat(数组2, 数组3 ...);
```

连接两个或多个数组，返回结果为新的数组

```
join()新的字符串 = 原数组.join(参数); // 参数选填
```

将数组转换为字符串，返回结果为转换后的字符串

```
reverse()反转后的数组  =  数组.reverse();
```

反转数组，返回结果为反转后的数组

`sort()`对数组的元素,默认按照Unicode编码

浏览器根据回调函数的返回值来决定元素的排序：

如果返回一个大于0的值，则元素会交换位置

如果返回一个小于0的值，则元素位置不变

如果返回一个0，则认为两个元素相等，则不交换位置

```javascript
	var result = arr3.sort(function(a, b) {
				return a - b; // 升序排列
		// return b - a; // 降序排列
		});
```

**数组的其他方法**

```
indexOf(value)

索引值 = 数组.indexOf(value);从前往后索引，获取 value 在数组中的第一个下标	
```

```
lastIndexOf(value)

索引值 = 数组.lastIndexOf(value);从后往前索引，获取 value 在数组中的最后一个下标	
```

```
find(function())

find(function(item, index, arr){return true});找出第一个满足「指定条件返回true」的元素。
```

```
findIndex(function())

findIndex(function(item, index, arr){return true});找出第一个满足「指定条件返回true」的元素的index	
```

```
Array.from(arrayLike)  

array = Array.from(arrayLike);将伪数组转化为真数组	
```

```
Array.of(value1, value2, value3)

Array.of(value1, value2, value3)将一系列值转换成数组。
```

```
isArray()：判断是否为数组

布尔值 = Array.isArray(被检测的值) ;
```

```
toString()：转换数组

字符串 = 数组.toString();
```

```
array = []; //清空数组
```

![](https://github.com/dongrui23/WEB/blob/master/javascript/%E6%95%B0%E7%BB%84.png)