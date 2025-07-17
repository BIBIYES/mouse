---
number headings: first-level 1, max 6, _.1.1
tags:
  - 布局
  - css
  - flex
  - 弹性布局
date: 2025-05-25
---

# CSS布局

## 1 弹性布局

[弹性盒子](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_flexible_box_layout)是一种用于按行或按列布局元素的一维布局方法。元素可以膨胀以填充额外的空间，收缩以适应更小的空间。本文将解释所有的基本原理。

## 2 Flex 模型说明

当我们给父组件（flex container）定义 flex 布局时，子元素（item）会按照主轴和纵轴来排布

```css
.parent{
	display:flex
}
```

![[Pasted image 20250524203556.png]]

### 2.1 主轴方向

子元素会按照主轴进行排布（main axis）

如果你想要切换子元素的排布方向可以使用 `flex-direction` 来切换列模式

```css
.parent{
	display:flex
	flex-direction: column
}

```

### 2.2 对其方式

* `justify-content` 用于在**主轴**上对齐子项（横向或纵向，取决于 `flex-direction`）
	- `flex-start`：子项靠主轴起始方向对齐（默认）
	- `flex-end`：子项靠主轴结束方向对齐
	- `center`：子项在主轴方向上居中对齐
	- `space-between`：**首尾对齐**，子项之间的间距相等
	- `space-around`：子项之间的间距相等，两端的间距是中间的一半
	- `space-evenly`：子项之间及两端的间距都完全相等
* `align-items` 用于在**交叉轴**上对齐子项（默认是垂直方向
	- `flex-start`：子项靠交叉轴起始方向对齐（上对齐）
	- `flex-end`：子项靠交叉轴结束方向对齐（下对齐）
	- `center`：子项在交叉轴方向上居中对齐（垂直居中）
	- `stretch`：**默认值**，子项被拉伸以填满容器（前提是子项没有固定高度）
	- `baseline`：子项根据其文本的**基线**对齐（比如文字底部对齐）

## 3 换行

当我们的**子元素**的宽度超出了**父元素**，那么我们的子元素就会被压缩

![[Pasted image 20250524204203.png]]

这里每个子元素的宽度设置 `400px` 因为空间不够被压缩了

我们可以设置来允许子元素换行

```css
.parent{
  flex-wrap: wrap;
}
```

![[Pasted image 20250525100936.png]]

### 3.1 间距

如果你想给盒子设置间距可以使用

```css
.parent{
 	gap:10px
}
```

### 3.2 对其方式

当你给父元素定义了 ` flex-wrap: wrap` 你会获得一个新的属性 `align-content`, `align-content`：控制**多行整体在交叉轴上的对齐方式**,适用于容器内的内容**换行时**（`flex-wrap: wrap;`），作用于**多行之间的间距分布**。

![[Pasted image 20250525115451.png]]

## 4 增长、收缩与基准

### 4.1 增长

控制子项在有剩余空间时如何放大。数值越大，分得的额外空间越多。默认是 0，不放大。

```css
.parent{
 flex-grow:1
}
```

### 4.2 收缩（flex-shrink）

控制子项在空间不足时如何缩小。数值越大，收缩越明显。默认是 1，允许缩小。

```css
.parent{
 flex-shrink:1
}
```

### 4.3 基准（flex-basis）

定义子项的初始大小（主轴方向），可以是长度值或 `auto`（默认，使用内容大小）。

```css
.parent{
 flex-basis:1
}
```

### 4.4 `flex` 简写

`flex` 是 `flex-grow`、`flex-shrink` 和 `flex-basis` 的简写属性，用于同时设置子项的放大比例、缩小比例和基准大小。  
例如：`flex: 1 1 0;` 表示 `flex-grow: 1; flex-shrink: 1; flex-basis: 0;`

当然可以，以下是你这段 CSS `position` 布局笔记的优化版本，保持 Markdown 格式，结构更清晰、语义更准确：

---

## 5 Position 布局

### 5.1 `position` 支持的值

- `static`（默认值）：元素按照正常文档流排列，**不支持 top/left/right/bottom/z-index 等定位属性**。
    
- `relative`：**相对于元素自身原本的位置进行偏移**，**仍保留原本占位空间**。
    
- `absolute`：**相对于最近一个 `position` 非 `static` 的祖先元素定位**，若没有则相对于 `html`（或 `body`）。**元素脱离文档流，不占据空间**。
    
- `fixed`：**相对于视口（viewport）进行定位**，**在页面滚动时位置不变**。
    
- `sticky`：**在特定滚动范围内表现为 relative，超出范围后表现为 fixed**，常用于粘性头部等。

---

### 5.2 只要 `position` 设置为非 `static`，以下属性才会生效

- `top` 距离顶部的高度
    
- `bottom` 距离底部的高度
    
- `left` 距离左侧的距离
    
- `right` 距离右侧的距离
    
- `z-index` 图层 
