## 编译

- TypeScript 编译的时候即使报错了，还是会生成编译结果，我们仍然可以使用这个编译之后的文件。

* 如果要在报错的时候终止 js 文件的生成，可以在 **tsconfig.json** 中配置 **noEmitOnError** 即可。

## 原始类型

1. boolean

- 使用构造函数 Boolean 创造的对象不是布尔值：

```JavaScript
let createdByNewBoolean: boolean = new Boolean(1);

// Type 'Boolean' is not assignable to type 'boolean'.
//   'boolean' is a primitive, but 'Boolean' is a wrapper object. Prefer using 'boolean' when possible.
```

事实上 new Boolean() 返回的是一个 Boolean 对象

直接调用 Boolean 也可以返回一个 boolean 类型：

```JavaScript
let createdByBoolean: boolean = Boolean(1);
```

2. number

- ES6 各进制数字表示方法

```JavaScript
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
// ES6 中的二进制表示法
let binaryLiteral: number = 0b1010;
// ES6 中的八进制表示法
let octalLiteral: number = 0o744;
let notANumber: number = NaN;
let infinityNumber: number = Infinity;
```

3. 字符串

没什么特别的的地方

4. 空值
   使用**void**表示没有返回值的函数

```JavaScript
function alertName(): void {
    alert('My name is Tom');
}
```

声明一个 void 类型的变量没有什么用，因为你只能将它赋值为 undefined 和 null

5. null 和 underfined
   与 void 的区别是，undefined 和 null 是所有类型的子类型。也就是说 undefined 类型的变量，可以赋值给 number 类型的变量：

```JavaScript
// 这样也不会报错
let u: undefined;
let num: number = u;

//而 void 类型的变量不能赋值给 number 类型的变量
let u: void;
let num: number = u;

// Type 'void' is not assignable to type 'number'.
```

## 任意值 **Any**

- 任意值（Any）用来表示允许赋值为任意类型
- 任意值上访问任何属性都是允许的，也允许调用任何方法 **声明一个变量为任意值之后，对它的任何操作，返回的内容的类型都是任意值。**
- 变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型

```JavaScript
let something;
something = 'seven';
something = 7;

something.setName('Tom');
```

## 类型推论

- 定义  
  TypeScript 会在没有明确的指定类型的时候推测出一个类型，这就是类型推论。  
  简单来说就是如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 any 类型而完全不被类型检查

```JavaScript
let myFavoriteNumber;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```

## 联合类型

联合类型（Union Types）表示取值可以为多种类型中的一种。

```JavaScript
let myFavoriteNumber: string | number;
```

## 接口

赋值的时候，变量的形状必须和接口的形状保持一致  
也就是说 实例变量内的属性数量和类型必须和接口一致 多了或者少了都不行

- 可选属性

```JavaScript
interface Person {
    name: string;
    age?: number;
}

let tom: Person = {
    name: 'Tom'
};
```

但是仍然不允许添加未定义的属性。

- 任意属性

```JavaScript
interface Person {
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};
```

**一旦定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集**

- 只读属性
  有时候我们希望对象中的一些字段只能在创建的时候被赋值，那么可以用 readonly 定义只读属性 如：

```JavaScript
readonly id: number
```

和 java 的 static 一样 不可更改

## 数组

三种实现方法：

1. []
2. 泛型  
   3.类数组

## 函数

- 可选参数必须接在必需参数后面  
  特殊情况：ES6 中，我们允许给函数的参数添加默认值，TypeScript 会将添加了默认值的参数识别为可选参数，此时就不受「可选参数必须接在必需参数后面」的限制了。

* 可实现重载
* 要在函数名后面定义类型

## 类型断言

类型断言（Type Assertion）可以用来手动指定一个值的类型。 用于判断联合类型中的某个类型

- 使用方法  
  **<类型>值**  
  **值 as 类型**（在 tsx 语法（React 的 jsx 语法的 ts 版）中必须用这种。）
- 类型断言不是类型转换，断言成一个联合类型中不存在的类型是不允许的
- 例子见：https://ts.xcatliu.com/basics/type-assertion
