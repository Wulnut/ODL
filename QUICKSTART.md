# ODL VSCode 插件 - 快速开始

## 🚀 5分钟快速上手指南

### 步骤 1: 测试插件

在当前项目目录中按 **F5** 键，VSCode 会启动一个新的扩展开发主机窗口。

### 步骤 2: 打开测试文件

在新窗口中，打开项目中的 `test_syntax.odl` 文件。

你应该能看到：
- ✅ 语法高亮正常显示
- ✅ 不同的关键字有不同的颜色
- ✅ 注释、字符串、数字都被正确高亮

### 步骤 3: 测试代码片段

创建一个新的 `.odl` 文件，尝试以下操作：

1. **创建完整模板**
   - 输入: `odltemplate`
   - 按: `Tab`
   - 结果: 生成完整的 ODL 文件模板

2. **创建配置章节**
   - 输入: `config`
   - 按: `Tab`
   - 结果: 生成 `%config {}` 章节

3. **创建对象**
   - 输入: `pobject`
   - 按: `Tab`
   - 结果: 生成持久化对象定义

4. **添加参数**
   - 输入: `pstring`
   - 按: `Tab`
   - 结果: 生成持久化字符串参数

5. **添加事件处理**
   - 输入: `oneventfilter`
   - 按: `Tab`
   - 结果: 生成带过滤器的事件处理器

### 步骤 4: 测试编辑功能

1. **自动括号补全**
   - 输入 `{` → 自动补全 `}`
   - 输入 `"` → 自动补全 `"`

2. **代码折叠**
   - 点击 `%config {` 左侧的折叠图标
   - 点击 `object MyObject {` 左侧的折叠图标

3. **注释快捷键**
   - 选中一行代码
   - 按 `Cmd+/` (Mac) 或 `Ctrl+/` (Win/Linux)
   - 结果: 该行被注释或取消注释

4. **智能缩进**
   - 在 `{` 后按 `Enter`
   - 结果: 自动缩进到正确位置

## 📝 创建你的第一个 ODL 文件

### 例子 1: 简单的配置模块

```odl
%config {
    name = "my_module";
    version = "1.0.0";
}

%define {
    object Settings {
        string Name = "Default";
        bool Enable = true;
    }
}
```

### 例子 2: 带事件处理的模块

```odl
%config {
    name = "device_manager";
}

import "device-lib.so" as "devlib";

%define {
    %persistent object Device {
        %persistent bool Enable = false;
        %persistent string Name;
    }
}

%populate {
    on event "app:start" call initialize;
    
    on event "dm:object-changed" call handle_enable
        filter 'path == "Device." && contains("parameters.Enable")';
}
```

## 🎯 推荐的代码片段

| 片段前缀 | 说明 | 使用场景 |
|---------|------|---------|
| `odltemplate` | 完整文件模板 | 创建新的 ODL 文件 |
| `config` | %config 章节 | 添加配置章节 |
| `define` | %define 章节 | 添加定义章节 |
| `populate` | %populate 章节 | 添加填充章节 |
| `pobject` | 持久化对象 | 定义持久化对象 |
| `object[]` | 多实例对象 | 定义表格对象 |
| `pstring` | 持久化字符串 | 添加字符串参数 |
| `pbool` | 持久化布尔值 | 添加布尔参数 |
| `puint32` | 持久化整数 | 添加整数参数 |
| `key` | 唯一键 | 添加键参数 |
| `readonly` | 只读参数 | 添加只读参数 |
| `onevent` | 事件处理 | 添加事件处理器 |
| `oneventfilter` | 带过滤器的事件 | 添加复杂事件处理 |
| `import` | 导入库 | 导入共享库 |
| `include` | 包含文件 | 包含其他 ODL 文件 |

## 🔍 验证清单

在继续使用之前，请确认：

- [ ] 语法高亮工作正常
- [ ] 代码片段可以正常触发 (Tab 键展开)
- [ ] 括号自动补全工作
- [ ] 代码折叠可用
- [ ] 注释快捷键 (Cmd+/ 或 Ctrl+/) 工作
- [ ] 智能缩进正确

## 📚 下一步

- 阅读 [使用指南](doc/usage-guide.md) 了解更多功能
- 查看 [README.md](README.md) 了解完整特性
- 参考 [ODL 文档](doc/odl.md) 学习 ODL 语法

## 🐛 遇到问题？

1. **语法高亮不工作**
   - 确认文件扩展名是 `.odl` 或 `.odl.uc`
   - 尝试重新加载窗口: `Cmd+Shift+P` → "Reload Window"

2. **代码片段不显示**
   - 按 `Ctrl+Space` 手动触发建议
   - 确认已启用代码片段建议

3. **其他问题**
   - 查看 [使用指南](doc/usage-guide.md) 的"故障排除"部分

## 🎉 享受编码！

现在你已经准备好使用 ODL VSCode 插件了！

试着创建一些 ODL 文件，体验语法高亮和代码片段带来的效率提升。
