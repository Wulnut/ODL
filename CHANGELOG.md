# Change Log

ODL 扩展的所有重要更改都将记录在此文件中。

格式基于 [Keep a Changelog](http://keepachangelog.com/)。

## [0.0.1] - 2024-02-10

### 新增
- ODL 语法高亮支持
  - 支持注释 (单行和多行)
  - 章节关键字 (%config, %define, %populate)
  - 结构关键字 (object, mib, select, extend, using)
  - 导入和包含语句 (import, include, #include, &include, ?include, requires)
  - 属性修饰符 (%persistent, %read-only, %unique, %key, %global, 等)
  - 数据类型 (string, bool, uint32, int32, datetime, double, float, 等)
  - 事件和动作 (on event, on action, call, filter)
  - 配置变量和环境变量 (${variable}, $(ENV))
  - 运算符和常量
  - 函数调用识别

- 代码编辑功能
  - 括号自动补全
  - 代码折叠支持
  - 智能缩进
  - 注释快捷键支持

- 文档
  - 完整的 README 文档
  - 使用示例和语言简介

### 支持的文件类型
- `.odl` 文件
- `.odl.uc` 文件

---

## [Unreleased]

### 计划中的功能
- 代码片段 (snippets) 支持
- 智能提示 (IntelliSense)
- 代码验证 (linting)
- 跳转到定义 (Go to Definition)
- 符号搜索 (Symbol Search)
- 重构支持
