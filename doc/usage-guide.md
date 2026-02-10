# ODL 插件使用指南

## 快速开始

### 1. 安装插件

将 ODL 插件文件夹复制到 VSCode 扩展目录，或在 VSCode 中按 `F5` 进行开发调试。

### 2. 打开 ODL 文件

打开任何 `.odl` 或 `.odl.uc` 文件，插件将自动激活并提供语法高亮。

## 功能特性

### 语法高亮

插件会自动为以下元素提供颜色高亮：

- **关键字**: `%config`, `%define`, `%populate`, `object`, `mib`, `import`, `include`, 等
- **数据类型**: `string`, `bool`, `uint32`, `datetime`, 等
- **属性修饰符**: `%persistent`, `%read-only`, `%unique`, `%key`, 等
- **注释**: `//` 单行注释和 `/* */` 多行注释
- **字符串**: 双引号和单引号字符串
- **变量**: `${config}` 和 `$(ENV)` 变量引用
- **运算符**: `==`, `!=`, `&&`, `||`, 等

### 代码片段 (Snippets)

按下以下前缀并按 `Tab` 键快速插入代码片段：

#### 章节片段
- `config` - 插入 `%config {}` 章节
- `define` - 插入 `%define {}` 章节
- `populate` - 插入 `%populate {}` 章节

#### 对象片段
- `object` - 插入对象定义
- `object[]` - 插入多实例对象定义
- `pobject` - 插入持久化对象定义
- `mib` - 插入 MIB 定义

#### 参数片段
- `string` - 插入字符串参数
- `bool` - 插入布尔参数
- `uint32` - 插入 32 位无符号整数参数
- `pstring` - 插入持久化字符串参数
- `pbool` - 插入持久化布尔参数
- `puint32` - 插入持久化整数参数
- `readonly` - 插入只读参数
- `key` - 插入唯一键参数

#### 导入/包含片段
- `import` - 插入导入语句
- `include` - 插入包含语句
- `#include` - 插入可选包含语句
- `?include` - 插入条件包含语句
- `requires` - 插入依赖声明

#### 事件处理片段
- `onevent` - 插入事件处理器
- `oneventfilter` - 插入带过滤器的事件处理器
- `onaction` - 插入动作处理器

#### 其他片段
- `function` - 插入函数定义
- `entrypoint` - 插入入口点定义
- `extend` - 插入 MIB 扩展
- `select` - 插入对象选择和扩展
- `odltemplate` - 插入完整的 ODL 文件模板

### 代码编辑功能

#### 自动括号补全
输入 `{`, `[`, `(`, `"`, `'` 时会自动插入对应的右括号。

#### 代码折叠
点击行号左侧的折叠图标可以折叠代码块：
- `%config {}` 章节
- `%define {}` 章节
- `%populate {}` 章节
- `object {}` 定义
- `mib {}` 定义

#### 注释快捷键
- 单行注释: 选中代码后按 `Cmd+/` (macOS) 或 `Ctrl+/` (Windows/Linux)
- 块注释: 选中代码后按 `Shift+Option+A` (macOS) 或 `Shift+Alt+A` (Windows/Linux)

#### 智能缩进
在代码块内按 `Enter` 会自动缩进到正确的位置。

## 使用示例

### 创建基本的 ODL 文件

1. 创建新文件 `example.odl`
2. 输入 `odltemplate` 然后按 `Tab`
3. 填写模块名称和描述
4. 开始编写你的数据模型

### 定义数据模型

```odl
%define {
    // 输入 'pobject' 然后按 Tab
    %persistent object MyDevice {
        // 输入 'pstring' 然后按 Tab
        %persistent string Name = "Default";

        // 输入 'pbool' 然后按 Tab
        %persistent bool Enable = true;

        // 输入 'object[]' 然后按 Tab
        object Port[] {
            %unique %key string Alias;
            %persistent uint32 Number;
        }
    }
}
```

### 添加事件处理

```odl
%populate {
    // 输入 'oneventfilter' 然后按 Tab
    on event "dm:object-changed" call my_handler
        filter 'path == "MyDevice." && contains("parameters.Enable")';
}
```

## 配置变量和环境变量

### 使用配置变量

在 `%config` 章节中定义变量：
```odl
%config {
    name = "my_module";
    version = "1.0.0";
}
```

在其他地方引用：
```odl
include "${name}_definition.odl";
print "Module: ${name} v${version}";
```

### 使用环境变量

```odl
%config {
    install_path = "$(PREFIX)/lib";
    home_dir = "$(HOME)";
}
```

## 键盘快捷键

- `Cmd+/` (macOS) / `Ctrl+/` (Windows/Linux): 切换行注释
- `Shift+Option+A` (macOS) / `Shift+Alt+A` (Windows/Linux): 切换块注释
- `Tab`: 展开代码片段
- `Cmd+Shift+[` (macOS) / `Ctrl+Shift+[` (Windows/Linux): 折叠代码块
- `Cmd+Shift+]` (macOS) / `Ctrl+Shift+]` (Windows/Linux): 展开代码块

## 故障排除

### 语法高亮不工作

1. 确认文件扩展名是 `.odl` 或 `.odl.uc`
2. 尝试重新加载窗口: `Cmd+Shift+P` → "Developer: Reload Window"
3. 检查 VSCode 版本是否 >= 1.107.0

### 代码片段不显示

1. 确认已启用代码片段建议: 设置 → `editor.suggest.snippetsPreventQuickSuggestions` → false
2. 尝试手动触发建议: `Ctrl+Space`

### 自动缩进不正确

1. 检查 VSCode 设置中的缩进配置
2. 确认使用的是 Tab 或 空格（不要混用）

## 技巧和最佳实践

### 1. 使用代码片段提高效率
不要手动输入重复的代码结构，使用代码片段可以节省大量时间。

### 2. 利用代码折叠
在大型 ODL 文件中，使用代码折叠可以更好地组织和导航代码。

### 3. 保持一致的命名风格
- 对象名使用 PascalCase: `MyObject`, `DeviceInfo`
- 参数名使用 PascalCase: `Enable`, `MaxValue`
- 函数名使用 snake_case: `my_function`, `handle_event`

### 4. 添加注释
为复杂的对象定义和事件过滤器添加注释，方便以后理解和维护。

### 5. 合理组织文件
- 将配置放在主文件中
- 将数据模型定义放在单独的 `_definition.odl` 文件中
- 将默认值放在 `_defaults.odl` 文件中

## 更多资源

- [ODL 完整文档](../doc/odl.md)
- [Ambiorix 项目](https://gitlab.com/prpl-foundation/components/ambiorix)
- [BBF TR-181 规范](https://usp-data-models.broadband-forum.org/)

## 反馈和支持

如有问题或建议，请在项目仓库中提交 Issue。
