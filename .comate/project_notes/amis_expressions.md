# AMIS表达式语法详解

## 表达式语法概览

AMIS使用类似JavaScript的表达式语法，支持多种表达式类型和操作符。

### 基础语法

```javascript
// 字段值引用
${field_name}
${field_name == 'value'}

// 表单数据上下文
this.field_name
this.field_name === 'value'

// 逻辑表达式
${a && b} 
${a || b}
${!condition}

// 比较运算
${a > b}
${a >= b} 
${a < b}
${a <= b}
${a == b}
${a === b}
${a != b}
${a !== b}
```

## 实际应用案例

### 条件显示 (visibleOn)

```json
{
  "label": "CPU核心数",
  "type": "number", 
  "name": "cpu",
  "visibleOn": "${custom_spec == true}",
  "requiredOn": "${custom_spec == true}"
}
```

### 动态数据源 (source)

```json
{
  "label": "子网",
  "type": "select",
  "name": "subnet_id", 
  "source": "/api/vpcs/${vpc_id}/subnets",
  "visibleOn": "${vpc_id}"
}
```

### 联动验证

```json
{
  "label": "存储大小",
  "type": "number",
  "name": "storage",
  "validations": {
    "greaterThanOrEquals": "${original_storage}"
  },
  "validationErrors": {
    "greaterThanOrEquals": "存储只能扩容，不能缩容"
  }
}
```

## 表达式上下文

### 1. 表单数据上下文
- `this`: 当前表单的所有字段值
- `${field_name}`: 特定字段的值

### 2. 全局上下文变量
- `${API_HOST}`: API基础路径
- 页面全局配置变量

### 3. 系统变量
- 路由参数、查询参数等

## 高级表达式功能

### 模板字符串 (tpl)

```json
{
  "label": "队列统计", 
  "type": "tpl",
  "tpl": "<a href='#/canghai/msg_list?queue_name=${name}'>${count}</a>"
}
```

### 复合条件

```json
{
  "visibleOn": "${deploy_mode == 'cluster' && version === '8.0'}"
}
```

### 多值匹配

```json
{
  "disabledOn": "${status == 'running' || status == 'starting'}"
}
```

## 表达式使用最佳实践

### 1. 引用字段时使用${}语法
```javascript
// 推荐
"visibleOn": "${custom_spec}"

// 不推荐  
"visibleOn": "custom_spec"
```

### 2. 复杂逻辑使用this上下文
```javascript
// 清晰明确
"visibleOn": "this.custom_spec && this.version === '8.0'"
```

### 3. 避免过度复杂的表达式
```javascript
// 清晰
"visibleOn": "${step1_completed && step2_valid}"

// 过度复杂
"visibleOn": "${(a && b) || (c && !d) && e > 10}"
```

## 表达式调试技巧

### 1. 使用console调试
```javascript
// 在浏览器控制台检查表达式结果
console.log(amis.data)
```

### 2. 分段测试复杂表达式
```javascript
// 分段验证
"visibleOn": "${condition1}"
"disabledOn": "${condition2}" 
```

### 3. 利用模板预览
```javascript
// 使用tpl预览变量值
"tpl": "当前值: ${field_name}"
```

这个分析基于项目中的实际使用案例，展示了AMIS表达式在动态表单配置中的强大能力。