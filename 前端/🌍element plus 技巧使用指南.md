# 🌍Element plus 技巧使用指南

## 1 统一配置组件

在业务开发中，我们可能要重复的去配置组件的某一个属性，这大大增加了我们的开发维护成本

假如你的项目中需要使用保持模态框居中显示，你可以这样配置

```js
// main.js

import { ElDialog } from 'element-plus'
// 配置模态框始终剧中显示
ElDialog.props.alignCenter = {
  type: Boolean,
  default: true, 
}
```