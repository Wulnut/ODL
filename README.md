# ODL Language Support for VSCode

这是一个为 Visual Studio Code 提供 ODL (Object Definition Language) 语言支持的扩展插件。

## 功能特性

### 语法高亮

该扩展为 ODL 文件提供了全面的语法高亮支持，包括：

- **注释**: 支持单行注释 (`//`) 和多行注释 (`/* */`)
- **章节关键字**: `%config`, `%define`, `%populate`
- **结构关键字**: `object`, `mib`, `select`, `extend`, `using`
- **导入/包含**: `import`, `include`, `#include`, `&include`, `?include`, `requires`
- **属性修饰符**: `%persistent`, `%read-only`, `%unique`, `%key`, `%global`, 等
- **数据类型**: `string`, `bool`, `uint32`, `int32`, `datetime`, `double`, `float`, 等
- **事件和动作**: `on event`, `on action`, `call`, `filter`
- **配置变量**: `${config_option}` 和环境变量 `$(ENV_VAR)`
- **运算符**: 逻辑运算符、比较运算符、算术运算符
- **常量**: `true`, `false`, `null`
- **函数调用**: 自动识别函数名称

### 代码片段 (Snippets)

提供 30+ 个常用的代码片段，快速插入：
- 章节定义 (`config`, `define`, `populate`)
- 对象定义 (`object`, `object[]`, `pobject`, `mib`)
- 参数定义 (`string`, `bool`, `uint32`, `pstring`, `pbool`, `readonly`, `key`)
- 导入语句 (`import`, `include`, `#include`, `?include`)
- 事件处理 (`onevent`, `oneventfilter`, `onaction`)
- 完整文件模板 (`odltemplate`)

详细的代码片段列表和使用方法请查看 [使用指南](doc/usage-guide.md)。

### 代码编辑功能

- **自动补全括号**: 自动匹配 `{}`, `[]`, `()`, `""`, `''`
- **代码折叠**: 支持折叠 `%config`, `%define`, `%populate`, `object`, `mib` 等代码块
- **智能缩进**: 自动缩进代码块
- **注释快捷键**: 使用 `Cmd+/` (macOS) 或 `Ctrl+/` (Windows/Linux) 快速注释/取消注释

## 支持的文件扩展名

- `.odl`
- `.odl.uc`

## 快速开始

### 安装

1. 下载或克隆此仓库
2. 将文件夹复制到 VSCode 扩展目录:
   - Windows: `%USERPROFILE%\.vscode\extensions`
   - macOS/Linux: `~/.vscode/extensions`
3. 重新加载 VSCode

或者使用命令行安装:

```bash
cd /path/to/this/extension
code --install-extension .
```

### 使用

1. 打开或创建一个 `.odl` 文件
2. 输入代码片段前缀（如 `odltemplate`）并按 `Tab` 键
3. 享受语法高亮和智能编辑功能

## 示例代码

```odl
%config {
    name = "ssh_server";
    storage-path = "${rw_data_path}/${name}/";
}

import "amx-ssh-server.so" as "${name}";

%define {
    %persistent object SSH {
        %persistent bool Enable = true;

        %persistent object Server[] {
            %unique %key string Alias;
            %read-only string Status = "Disabled";
            %persistent uint32 Port = 22;

            uint32 close_sessions();
        }
    }
}

%populate {
    on event "app:start" call app_start;

    on event "dm:object-changed" call ssh_toggle
        filter 'path == "SSH." && contains("parameters.Enable")';
}
```

## ODL 语言简介

ODL (Object Definition Language) 是一种用于定义数据模型的领域特定语言，主要用于 Ambiorix 框架。它提供了一种简单的方式来定义层次化的对象树，每个对象可以包含参数和函数。

### 主要特性

- 支持定义层次化的数据模型
- 可以绑定函数实现
- 支持事件处理机制
- 支持配置选项和环境变量
- 兼容 BBF TR-181 数据模型规范

## 文档

- [使用指南](doc/usage-guide.md) - 详细的使用说明和技巧
- [ODL 语言规范](doc/odl.md) - 完整的 ODL 语言文档
- [更新日志](CHANGELOG.md) - 版本更新历史

## 开发和调试

1. 在 VSCode 中打开此项目文件夹
2. 按 `F5` 启动扩展开发主机
3. 在新窗口中打开 `.odl` 文件进行测试
4. 查看 `test_syntax.odl` 文件以测试所有语法高亮功能

## 贡献

欢迎提交 Issue 和 Pull Request！

### 开发环境设置

```bash
# 克隆仓库
git clone <repository-url>
cd ODL

# 在 VSCode 中打开
code .

# 按 F5 启动调试
```

## 更新日志

### 0.0.1 (2024-02-10)

- ✨ 初始版本发布
- 🎨 完整的 ODL 语法高亮支持
- 📝 30+ 个代码片段
- 🔧 支持代码折叠和自动缩进
- 📖 完整的文档和使用指南

查看 [CHANGELOG.md](CHANGELOG.md) 了解更多详情。

## 参考资料

- [Ambiorix ODL 文档](doc/odl.md)
- [prpl Foundation](https://gitlab.com/prpl-foundation/components/ambiorix)
- [BBF TR-181 规范](https://usp-data-models.broadband-forum.org/)

## 许可证

请参考项目中的相关许可证文件。

## 致谢

感谢 Ambiorix 项目和 prpl Foundation 提供的优秀框架和文档。

---

**享受 ODL 编程的乐趣！** 🚀
