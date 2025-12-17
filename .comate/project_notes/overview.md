# butterfly-admin 项目总览

## 项目基本信息
- **项目类型**: 基于AMIS的后台管理系统模板
- **技术栈**: AMIS + Nginx + 前端静态页面
- **部署方式**: 自定义编译Nginx，静态资源部署

## 项目架构
```
butterfly-admin
├── conf/                    # Nginx配置文件
├── static/                  # AMIS页面配置和静态资源
│   ├── pages/               # 所有页面配置JSON
│   ├── jssdk/               # AMIS SDK (可选)
│   └── logo/                # 项目Logo
├── templates/               # HTML模板文件
├── sbin/                    # 自定义编译的Nginx二进制
└── run.sh                   # Nginx进程管理脚本
```

## 核心功能模块

### 1. 消息队列模块
位置: `static/pages/canghai/`
- **队列管理**: 队列状态监控
- **消息统计**: 不同状态消息计数
- **动态模板**: 模板字符串渲染

### 2. 演示模块
位置: `static/pages/demo/`
- **基础表单**: 各种表单控件示例
- **进阶功能**: CRUD操作、向导表单
- **交互示例**: 复杂表单交互模式

## AMIS框架能力分析

### 1. 数据源机制 (Source)
**支持程度**:  ⭐⭐⭐⭐⭐
- **API动态加载**: 支持从API接口动态获取数据
```json
"source": "/api/vpcs/${vpc_id}/subnets"
```
- **表达式支持**: 支持参数化URL，基于表单值动态构建请求
- **异步加载**: 支持搜索筛选和分页加载

### 2. 条件显示机制 (visibleOn/disabledOn/hiddenOn)
**支持程度**: ⭐⭐⭐⭐⭐
- **表达式语法**: 完整的表达式语言支持
```json
"visibleOn": "${custom_spec == true}",
"disabledOn": "this.status === 'running'",
"requiredOn": "${public_access == true}"
```
- **多层嵌套**: 支持复杂条件逻辑
- **上下文引用**: 支持`this`关键字引用当前数据上下文

### 3. 动态表单字段更新机制
**支持程度**:  ⭐⭐⭐⭐⭐
- **联动更新**: 字段间值依赖动态更新
```json
"minDate": "${start}",
"source": "/api/vpcs/${vpc_id}/security-groups"
```
- **步骤联动**: 向导表单中各步骤数据传递
- **实时验证**: 基于表达式的即时验证规则

### 4. 模板引用和组件复用
**支持程度**: ⭐⭐⭐⭐
- **JSON引用**: 支持`$ref`引用外部JSON配置
```json
{"$ref": "operation-template.json#/actionButtons"}
```
- **模板字符串**: 支持`tpl`属性使用模板字符串
```json
"tpl": "<a href='#/canghai/msg_list?queue_name=${name}'>${count}</a>"
```
- **组件标准化**: 通过模板实现标准化操作按钮

## AMIS框架支持程度总结

| 功能特性 | 支持程度 | 实现方式 | 备注 |
|---------|---------|----------|------|
| 数据源机制 |  ⭐⭐⭐⭐⭐ | source属性 + 表达式 | 完全支持动态API调用 |
| 条件显示 | ⭐⭐⭐⭐⭐ | visibleOn/disabledOn | 完整表达式语言支持 |
| 表单联动 |  ⭐⭐⭐⭐⭐ | 字段间表达式依赖 | 实时更新和验证 |
| 模板引用 |  ⭐⭐⭐⭐ | $ref + tpl模板 | JSON引用和字符串模板 |
| 外部配置 | ⭐⭐⭐⭐ | API + JSON文件 | 支持远程和本地配置 |

## 实现建议

### 1. 动态预设配置
- 使用`source`属性实现动态配置加载
- 结合`visibleOn`实现条件配置显示
- 通过JSON模板实现配置复用

### 2. 复杂表单交互
- 采用向导模式拆分复杂配置
- 使用条件显示实现步骤间依赖
- 集成实时验证保证数据一致性

### 3. 组件化开发
- 提取通用组件为独立JSON模板
- 使用`$ref`引用实现组件复用
- 标准化API和交互模式

这个项目充分展示了AMIS框架在复杂后台管理系统中的强大能力，特别是在动态配置、条件交互和组件复用方面的成熟支持。
