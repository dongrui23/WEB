
### ES6开发环境搭建

创建文件dist(保存转化的es5代码)，src(es6代码)，index.html(引入文件为dist下的js文件)

在vsc终端上运行(ctrl+~)

`npm init -y`  生成package.json文件，-y是默认设置

`npm install -g babel-cli`  全局安装babel

安装两个包：babel-preset-es2015 & babel-cli

`npm install --save-dev babel-preset-es2015 babel-cli`

在根目录上创建文件.babelrc

```
{
  "presets":[
    "es2015"
  ],
  "plugins":[]
}
```

`babel src/index.js -o dist/index.js`  转换为es5，-o为输出的意思

转换完成

简化命令package.json里面的代码

```
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"

改为

"scripts": {
  "build": "babel src/index.js -o dist/index.js"
```

### 新的声明方式

**var 全局声明**

```javascript
var a = 1;
console.log(a);//1

var a = 1;
window.onload = function () {
   console.log(a);//1
 }

var a = 1;
{
  var a = 'hello'
}
console.log(a)//hello 会污染到外面的声明

for (var i=0;i<10;i++) {
  console.log('里面'+i);//0到9
}
console.log('外面'+i);//10,被污染了
```

**let 局部声明**

```javascript
var a = 1;
{
  let a = 'hello';//不会污染到外面
}
console.log(a);//1

for (let i=0;i<10;i++) {
  console.log('里面'+i);//0到9
}
console.log('外面'+i);//未定义undefined
```

**const 常量**

```javascript
const a = '007';
var a = '009';
console.log(a);//报错
```

### 变量的解构赋值

**数组的解构赋值**

```javascript
let[a,b,c]=[0,1,2];//顺序一一对应
console.log(a);
console.log(b);
console.log(c);

let[foo='true']=[];
console.log(foo);//true,默认值可用

let[a,b='haha']=[0,undefined];//0haha,如为null，则0null
console.log(a+b);
```

**对象的解构赋值**

```javascript
let {foo,bar} = { foo:'WWW',bar:'OOO'};//key值对应
console.log(foo+bar)

let foo;
({foo}={foo:'999'});//要加括号,语法
console.log(foo)
```

**字符串的解构赋值**

```javascript
const [a,b,c]='555';//应用于权限有关
console.log(a);
console.log(b);
console.log(c);
```

### 扩展运算符和rest运算符

**对象扩展运算符（…）**

传入的参数是不确定的

```javascript
function dongrui(...arg){
  console.log(arg[0]);//1
  console.log(arg[1]);//3
  console.log(arg[2]);//2
}
dongrui(1,3,2);
```

对内存堆栈的引用

```javascript
let arr1 = ['number','string','object'];
let arr2 = arr1;
console.log(arr2);//["number", "string", "object"]
arr2.push('boolean');
console.log(arr1);//["number", "string", "object", "boolean"]


let arr1 = ['number','string','object'];
let arr2 =[...arr1];
arr2.push('boolean');
console.log(arr2);//["number", "string", "object", "boolean"]
console.log(arr1);// ["number", "string", "object"]
```

**rest运算符**

```javascript
function aa(first,...arg) {
  console.log(arg.length);//7
}
aa(0,1,2,3,4,5,6,7);


function aa(first,...arg) {

  //es5
  for(let i=0;i<arg.length;i++){
    console.log(aa[i]);//1-7
  }

  //es6 for…of循环,可以避免我们开拓内存空间
  for(let val of arg){
    console.log(val);//1-7
  }
}
aa(0,1,2,3,4,5,6,7)
```

### 字符串模板

>技术胖说编译麻烦，就重新新建文件

```
npm init之后

运行npm install -g live-server   // 全局安装live-server，作为前端服务器，实时更新

启动程序命令：live-server
```

```javascript
// 换行
let dr = 'dongrui23';
let lal = `${dr}<br/>
唯一的方法就是--<b>口头确认</b>--发email到责任人确认--通知上级`;
document.write(lal);
```

```javascript
// 运算
let dr = 1;
let lal =2;
let result = `${dr+lal}`;
document.write(result);
```

```javascript
// 查找
let dr = 1;
let lal = '<br/>
唯一的方法就是--<b>口头确认</b>--发email到责任人确认--通知上级';
document.write(lal.indexOf(dr)>0);// es5语法

es6
document.write(lal.includes(dr));// 记得s
document.write(lal.startsWith(dr));// 查找开头
document.write(lal.endsWith(dr));// 查找开头
```

```javascript
// 复制
document.write('sting'.repeat(3));// string打印三次
```

### ES6数字操作

```javascript
//二进制声明 Binary
let binary = 0B010101;
console.log(binary);//21

//八进制声明 Octal
let octal = 0o666;
console.log(octal);//438
```

```javascript
判断是否是数字
let a = 99/8;
console.log(Number.isFinite(a));//T
console.log(Number.isFinite('a'));//F
console.log(Number.isFinite(NaN));//F
console.log(Number.isFinite(undefined));//F
```

```javascript
//NaN
console.log(Number.isNaN(NaN));//T
```

```javascript
//Number.isInteger,是否为整数
let a = 3.14;
console.log(Number.isInteger(a)); //F

//！Number.isInteger,是否为浮点型
let a = 3.14;
console.log(!Number.isInteger(a));//T
console.log(Number.parseFloat(a));//转化为浮点型
```

```javascript
// es5最大数
let a = Math.pow(2,53)-1;
console.log(a);

// es6最大数
console.log(Number.MAX_SAFE_INTEGER);
console.log(Number.isSafeInteger(a));//是否超过最大安全值
```

### ES6中新增的数组知识（1）

```javascript
// Array.from()方法
// json数组格式
let json = {
  "0" : "dongrui23",
  "1" : "los",
  "2" : "lakers",
  length : 3
}
```

```javascript
//es6 ,json转换为 Array
let arr = Array.from(json);
console.log(arr);
```

```javascript
// Array.of方法,转化为数组格式
let arr = Array.of('[1,2,4,3,2,9],aa,sd,4');
console.log(arr);
```

```javascript
// find() 实例方法,数组元素查找方法
// value:当前查找的值，index:这个值得索引，arr:当前数组
let arr = [1,9,7,3,6];
console.log(arr.find(function(value,index,arr){
  return value > 5;
}))
```

### ES6中新增的数组知识（2）

```javascript
// fill 填充,替换
let arr = ['dongrui','los','12']; 
arr.fill('web',2,3);// fill('替换的内容','start'，'end')
console.log(arr);
```

```javascript
// 数组循环
let arr = ['dongrui','los','12']; 
for(let item of arr.keys()){
  console.log(item);//输出下标
}

let arr = ['dongrui','los','12']; 
for(let [value,index] of arr.entries()){
  console.log(value+':'+index);
}
```

```javascript
// 自定义循环
// 数组循环
let arr = ['dongrui','los','12']; 
let list=arr.entries();
console.log(list.next().value);// 第一个值
console.log('---------------');
console.log(list.next().value);
console.log('~~~~~~~~~~~~~~~');
console.log(list.next().value);
```

### ES6中的箭头函数和扩展

主动抛出错误

`throw new Error('This is error')`

```javascript
// es5
function add(a,b) {
  return a+b 
}
console.log(add(1,8));

// es6
var add =(a,b) => a+b;//var add =(a,b) =>{return a+b;}
console.log(add(1,81));

// 延时器 
setTime(() => {
  console.log('dongrui23')
},1000)
```

### ES6中的函数和数组补漏

```javascript
//对象的函数解构json
let json = {
  a:'dongrui',
  b:'los'
}
function ff({a,b='wwn'}){
  console.log(a,b)
} 
ff(json);
```

```
//数组解构
let arr = ['dongrui','los','lakers'];
function ff(a,b,c){
  console.log(a,b,c)
}
ff(...arr);
```

```javascript
//in的用法
//判断对象
let obj = {
  a:'dongrui23',
  b:'los'
}
console.log('a' in obj);
```

```javascript
//判断数组
let arr = ["aa",,,];
console.log(arr.length);//这方法不用，容易产生业务逻辑错误
console.log(0 in arr);//true,index
```

```javascript
//数组遍历 
//forEach
let arr = ['dongrui23','los','lakers',35,23]
arr.forEach((val,index) =>{
  console.log(index,val);
})
//filter
arr.filter(x =>console.log(x));
//some
arr.some(x =>console.log(x));
//map
console.log(arr.map(x =>'web'));//替换为web
//1
for(let item of arr){
  console.log(item);
}
//2
for(var i=0;i<arr.length;i++){
  console.log(arr[i])
}
```

```javascript
//arr转换为String
let arr = ['dongrui23','los','lakers']
console.log(arr.toString());
console.log(arr.join('-'));
```

### ES6中对象

```javascript
//赋值
let name ='dongrui';
let obj = {name};
console.log(obj)

//key值的构建
let key = 'skill'
var obja = {
  [key]:'web'
}
console.log(obja)

//自定义对象方法
//es5
let objb={
  add:function(a,b){
    return a+b;
  }
}
console.log(objb.add(3,8))
```

```javascript
//is
let obj1={name:'shenz'};
let obj2={name:'shenz'};
console.log(obj1.name===obj2.name);//es5，True
console.log(Object.is(obj1.name,obj2.name));//es6
console.log(Object.is(+0,-0));//es6,False
console.log(Object.is(NaN,NaN));//es6,True
//ps: ===同值相等，is严格相等
```

```javascript
//assign合并对象
let a={a:'dongrui23'};
let b={b:'view'};
let c={c:'web'};
let d = Object.assign(a,b,c);
console.log(d);
```

### Symbol在对象中的作用

```javascript
//Symbol
let a = Symbol();
console.log(typeof(a))
let b = Symbol('dongrui23');
console.log(b)
```

```javascript
//key值构建
let dongrui23 = Symbol();
let obj = {
  [dongrui23]: 'okokok'
}
console.log(obj[dongrui23]);//要用方括号，点是没用的
```

```javascript
let obj3 = {name:'dongrui23',address:'los'}
let age = Symbol();
obj3[age]=25;
for(let item in obj3){
  console.log(obj3[item]);
}
// console.log(obj3[age]);//对age的保护
```

### Set和WeakSet数据结构

**Set**

Set增删查

```javascript
//Set
let setArr = new Set(['dongrui23','los','web']);

setArr.add('lol');//增加
console.log(setArr);
//has,查找
console.log(setArr.has('los'));
//删除
setArr.clear();
console.log(setArr);
//只删除一项
setArr.delete('web');
```

遍历

```javascript
let setArr = new Set(['dongrui23','los','web']);
//for..of
for(let item of setArr){
  console.log(item);
}
//forEach
setArr.forEach((val) => console.log(val));
//size
console.log(setArr.size);//3
```

**WeakSet**

```javascript
//WeakSet
let weakObj = new WeakSet();//直接加是不行的  
let obj = {a:'dongrui',b:'los'};
let obj1=obj;//不会重复

weakObj.add(obj);
weakObj.add(obj1);

console.log(weakObj);
```

### map数据结构

```javascript
//map
  let json={
    name:'dongrui23',
    skill:'web'
  };
console.log(json.name);

//=>
var map = new Map();
map.set(json,'iam');
console.log(map);
map.set('dongrui23',json);
console.log(map);

//map增删查
//get
console.log(map.get(json));
console.log(map.get('dongrui23'));

//delete
// map.delete(json);
// console.log(map);
// map.clear();
console.log(map.size);//2

//has查找
console.log(map.has('dongrui23'));
```

### 用Proxy进行预处理

```javascript
//proxy 代理 ES6增强 对象和函数(方法) 生命周期 预处理

let obj = {
  add:function(val){
    return val+100;
  },
  name:'los lakers'
}
let pro = new Proxy({
  add:function(val){
    return val+100;
  },
  name:'los lakers'
},{
  //get set apply
  //get
  get:function( target,key,property){
    console.log('come in you');
    // console.log(target);
    return target[key];
  },
  set:function(target,key,value,receiver){
    console.log(`setting ${key}= {value}`);
    return target[key] = value;
  }
});
console.log(pro.name);
pro.name = 'lololo'
console.log(pro.name);//记得返回值return
```

```javascript
let target =function(){
  return 'okko';
}
let handler = {
  apply(target,ctx,args){
    console.log('do it');
    return Reflect.apply(...arguments);
  }
}
let pro = new Proxy(target,handler);
console.log(pro());
```

### promise对象的使用

```javascript
//promise es5 回调地狱
let state=1;
 
function step1(resolve,reject){
    console.log('1.开始-洗菜做饭');
    if(state==1){
        resolve('洗菜做饭--完成');
    }else{
        reject('洗菜做饭--出错');
    }
}
 
 
function step2(resolve,reject){
    console.log('2.开始-坐下来吃饭');
    if(state==1){
        resolve('坐下来吃饭--完成');
    }else{
        reject('坐下来吃饭--出错');
    }
}
 
 
function step3(resolve,reject){
    console.log('3.开始-收拾桌子洗完');
     if(state==1){
        resolve('收拾桌子洗完--完成');
    }else{
        reject('收拾桌子洗完--出错');
    }
}
 
new Promise(step1).then(function(val){
    console.log(val);
    return new Promise(step2);
 
}).then(function(val){
     console.log(val);
    return new Promise(step3);
}).then(function(val){
    console.log(val);
    return val;
});
```

### class类的使用

class声明

```javascript
//class
class Coder{
  name(val){
    console.log(val);
    return val;
  }//不用逗号
  skill(val){
    console.log(this.name('dongrui23')+':'+ val);
    
  }
}
let dongrui23 = new Coder;
// dongrui23.name('ad');
dongrui23.skill('adc');
```

类的传参

```javascript
class Coder{
  name(val){
    console.log(val);
    return val;
  }//不用逗号
  skill(val){
    console.log(this.name('dongrui23')+':'+ val);
  }
  constructor(a,b){
    this.a=a;
    this.b=b;
  }
  add(){
    return this.a + this.b
  }
}
let dongrui23 = new Coder(1,2);
console.log(dongrui23.add());
```

class继承

```javascript
class Coder{
  name(val){
    console.log(val);
    return val;
  }//不用逗号
  skill(val){
    console.log(this.name('dongrui23')+':'+ val);
  }
  constructor(a,b){
    this.a=a;
    this.b=b;
  }
  add(){
    return this.a + this.b
  }
}
//继承
class htmler extends Coder{

}
let ok = new htmler;
ok.name('dongrui23')
```
### 模块化操作

新建文件->src/temp.js

`export var name = 'dongrui23';`

src目录下命令行`babel-node index.js`

index.js

```javascript
//export 输出
//import 引入
import {name} from './temp';
console.log(name);
```

----------------------------

temp.js

```javascript
var name = 'dongrui23';
var b = 'lololo';
var c = 'web';
// export function add(a,b){
//   return a+b;
// }

export{
  name as a,
  cname as b,
  skill as c
}
```

index.js

```javascript
import {name,cname,skill} from './temp';
console.log(name,cname,skill);
```

=========================

//export default && export

```javascript
export var name = 'dongrui23';
var c = 'web';
export function add(a,b){
  return a+b;
}
import {name,add} from './temp';

export defalut var a = 'dongrui23';
import shh(自己起的) from './temp';
```