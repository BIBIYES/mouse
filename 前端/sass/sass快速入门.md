# Sass快速入门

## 1 什么是 `sass`

Sass 是一款强化 CSS 的辅助工具，它在 CSS 语法的基础上增加了变量 (variables)、嵌套 (nested rules)、混合 (mixins)、导入 (inline imports) 等高级功能，这些拓展令 CSS 更加强大与优雅。使用 Sass 以及 Sass 的样式库（如 [Compass](http://compass-style.org/)）有助于更好地组织管理样式文件，以及更高效地开发项目。

---

## 2 嵌套规则

Sass 允许将一套 CSS 样式嵌套进另一套样式中，内层的样式将它外层的选择器作为父选择器，嵌套功能避免了重复输入父选择器，而且令复杂的 CSS 结构更易于管理

```scss
#main p {
  color: #00ff00;
  width: 97%;

  .redbox {
    background-color: #ff0000;
    color: #000000;
  }
}
```

编译为

```css
#main p {
  	color: #00ff00;
	width: 97%; 
}
#main p .redbox {
    background-color: #ff0000;
    color: #000000;
}
```

---

### 2.1 父选择器 `&`

在嵌套 CSS 规则时，有时也需要**直接使用嵌套外层的父选择器**，例如，当给某个元素设定 `hover` 样式时，或者当 `body` 元素有某个 classname 时，可以用 `&` 代表嵌套规则外层的**父选择器**。

```scss
a {
  font-weight: bold;
  text-decoration: none;
  &:hover { text-decoration: underline; }
  body.firefox & { font-weight: normal; }
}
```

编译为

```css
a {
  font-weight: bold;
  text-decoration: none; 
}
a:hover {
    text-decoration: underline; 
}
body.firefox a {
    font-weight: normal; 
}
```

### 2.2 复合选择

通过 `&` 引用父选择器并添加后缀（如 `-`、`_` 等合法字符），生成**单一的组合选择器**，编译后选择器名称直接拼接（无空格），表示**同一层级元素的变体或组合**

**组件变体或状态**  
用于描述同一元素的不同类型或状态，例如按钮的不同样式（主按钮、禁用按钮）。

```scss
.button {
	&-primary { background: blue; } 
	&-disable { opacity: 0.5; }
}
```

**编译为**

```css
.button-primary { background: blue; }
.button-disabled { opacity: 0.5; }
``` 

### 2.3 属性嵌套

有些 CSS 属性遵循相同的命名空间 (namespace)，比如 `font-family, font-size, font-weight` 都以 `font` 作为属性的命名空间。为了便于管理这样的属性，同时也为了避免了重复输入，Sass 允许将属性嵌套在命名空间中

```scss
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```

编译为

```css
.funky {
  font-family: fantasy;
  font-size: 30em;
  font-weight: bold;
}
```

## 3 SassScript

在 CSS 属性的基础上 Sass 提供了一些名为 SassScript 的新功能。 SassScript 可作用于任何属性，允许属性使用变量、算数运算等额外功能。

### 3.1 变量 `$`

SassScript 最普遍的用法就是变量，变量以美元符号开头，赋值方法与 CSS 属性的写法一样

```scss
$width: 5em;
```

变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量），不在嵌套规则内定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加 `!global` 声明：

```scss
#main {
  $width: 5em !global;
  width: $width;
}

#sidebar {
  width: $width;
}
```

**编译为**

```css
#main {
  width: 5em;
}

#sidebar {
  width: 5em;
}
```

#### 3.1.1 变量定义 `!default`

可以在变量的结尾添加 `!default` ，如果**变量已经被赋值**，**不会再被重新赋值**，但是如果变量还没有被赋值，则会被赋予新的值。

```scss
$content: "First content";
$content: "Second content?" !default;
$new_content: "First time reference" !default;

#main {
  content: $content;
  new-content: $new_content;
}
```

**编译为**

```css
#main {
  content: "First content";
  new-content: "First time reference"; }
```

变量是 null 空值时将视为未被 `!default` 赋值。

```
$content: null;
$content: "Non-null content" !default;

#main {
  content: $content;
}
```

编译为

```
#main {
  content: "Non-null content"; }
```

### 3.2 数据类型 (Data Types)

- 数字，`1, 2, 13, 10px`
- 字符串，有引号字符串与无引号字符串，`"foo", 'bar', baz`
- 颜色，`blue, #04a3f9, rgba(255,0,0,0.5)`
- 布尔型，`true, false`
- 空值，`null`
- 数组 (list)，用空格或逗号作分隔符，`1.5em 1em 0 2em, Helvetica, Arial, sans-serif`
- maps, 相当于 JavaScript 的 object，`(key1: value1, key2: value2)`

### 3.3 运算 (Operations)

SassScript 支持数字的加减乘除、取整等运算 (`+, -, *, /, %`)，如果必要会在不同单位间转换值。

```scss
p {
  width: 1in + 8pt;
}
```

**编译为**

```css
p {
  width: 1.111in; }
```

#### 3.3.1 除法运算

`/` 在 CSS 中通常起到**分隔数字**的用途，SassScript 作为 CSS 语言的拓展当然也支持这个功能，同时也赋予了 `/` **除法运算**的功能。也就是说，如果 `/` 在 SassScript 中把两个数字分隔，编译后的 CSS 文件中也是同样的作用。

以下三种情况 `/` 将被视为除法运算符号：

- 如果值，或值的一部分，是变量或者函数的返回值
- 如果值被圆括号包裹
- 如果值是算数表达式的一部分

```scss
p {
  font: 10px/8px;             // Plain CSS, no division
  $width: 1000px;
  width: $width/2;            // Uses a variable, does division
  width: round(1.5)/2;        // Uses a function, does division
  height: (500px/2);          // Uses parentheses, does division
  margin-left: 5px + 8px/2px; // Uses +, does division
}
```

**编译为**

```css
p {
  font: 10px/8px;
  width: 500px;
  height: 250px;
  margin-left: 9px; }
```

如果需要使用**变量**，同时又要确保 `/` **不做除法运算**而是完整地编译到 CSS 文件中，只需要用 `#{}` 插值语句将变量包裹。 ^05690a

```
p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height};
}
```

**编译为**

```
p {
  font: 12px/30px; }
```

#### 3.3.2 颜色值运算

颜色值的运算是分段计算进行的，也就是分别计算**红色**，**绿色**，以及**蓝色**的值

```scss
p {
  color: #010203 + #040506;
}
```

计算 `01 + 04 = 05` `02 + 05 = 07` `03 + 06 = 09`，然后编译为

```css
p {
  color: #050709; }
```

数字与颜色值之间也可以进行算数运算，同样也是分段计算的，比如

```scss
p {
  color: #010203 * 2;
}
```

计算 `01 * 2 = 02` `02 * 2 = 04` `03 * 2 = 06`，然后编译为

```css
p {
  color: #020406; 
}
```

需要注意的是，如果颜色值包含 alpha channel（rgba 或 hsla 两种颜色值），必须拥有相等的 alpha 值才能进行运算，因为算术运算不会作用于 alpha 值。

```scss
p {
  color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);
}
```

**编译为**

```css
p {
  color: rgba(255, 255, 0, 0.75); 
}
```

#### 3.3.3 圆括号 (Parentheses)

圆括号可以用来影响运算的顺序：

```scss
p {
  width: 1em + (2em * 3);
}
```

**编译为**

```css
p {
  width: 7em; }
```

### 3.4 函数 (Functions)

SassScript 定义了多种函数，有些甚至可以通过普通的 CSS 语句调用：

```scss
p {
  color: hsl(0, 100%, 50%);
}
```

**编译为**

```css
p {
  color: #ff0000; }
```

### 3.5 插值语句 `#{}`

通过 `#{}` 插值语句可以在选择器或属性名中使用变量：

```scss
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}
```

**编译为**

```css
p.foo {
  border-color: blue; }
```

`#{}` 插值语句也可以在属性值中插入 SassScript，大多数情况下，这样可能还不如使用变量方便，但是使用 `#{}` [[#^05690a|可以避免 Sass 运行运算表达式]]，直接编译 CSS。

```scss
p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height};
}
```

**编译为**

```css
p {
  font: 12px/30px; }
```