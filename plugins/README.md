# Claude Code 插件开发指南

这个目录包含所有自定义的 Claude Code 插件。每个插件都遵循标准的目录结构和配置格式。

## 现有插件

### 1. Productivity Plugin（生产力插件）

提升工作效率的生产力工具集。

**功能**：
- ✅ 待办事项管理（/todo）
- 🎯 专注模式（/focus）
- 🤖 任务管理助手（TaskAssistant）
- 📊 项目规划技能
- ⏰ 时间管理技能

**使用场景**：项目规划、任务管理、时间优化

[查看详情](productivity-plugin/README.md)

### 2. Dev Tools Plugin（开发工具插件）

面向开发者的专业工具集。

**功能**：
- 🚀 代码生成（/gen）
- 🔍 代码审查（/review）
- 🤖 代码审查专家（CodeReviewer）
- 🏗️ 架构设计专家（Architect）
- 📊 代码分析技能
- 🔧 重构技能

**使用场景**：代码开发、质量把控、架构设计

[查看详情](dev-tools-plugin/README.md)

## 插件结构

每个 Claude Code 插件都遵循以下标准结构：

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json          # 插件元数据（必需）
├── commands/                 # 自定义斜杠命令（可选）
│   └── command-name.md
├── agents/                   # 自定义代理（可选）
│   └── agent-name.md
├── skills/                   # 代理技能（可选）
│   └── skill-name/
│       └── SKILL.md
├── hooks/                    # 事件处理程序（可选）
│   └── hooks.json
└── README.md                 # 插件使用说明
```

## 创建新插件

### 步骤 1：创建插件目录

```bash
cd plugins
mkdir my-plugin
cd my-plugin
```

### 步骤 2：创建基础结构

```bash
mkdir -p .claude-plugin commands agents skills hooks
```

### 步骤 3：编写插件元数据

创建 `.claude-plugin/plugin.json`：

```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "description": "插件描述",
  "author": "Your Name",
  "homepage": "https://github.com/yourusername/repo",
  "keywords": ["keyword1", "keyword2"],
  "license": "MIT"
}
```

**字段说明**：
- `name`（必需）：插件唯一标识符，使用小写和连字符
- `version`（必需）：语义化版本号（SemVer）
- `description`（必需）：简短描述插件功能
- `author`（可选）：作者名称
- `homepage`（可选）：项目主页 URL
- `keywords`（可选）：关键词数组，便于搜索
- `license`（可选）：开源许可证

### 步骤 4：添加命令（可选）

在 `commands/` 目录下创建 Markdown 文件，文件名即为命令名。

**示例**：`commands/hello.md`

```markdown
# Command: /hello

问候命令示例。

## 描述

这是一个简单的问候命令，演示如何创建自定义命令。

## 用法

```
/hello [name]
```

## 参数

- `name` - （可选）要问候的名字，默认为 "World"

## 示例

```
/hello
/hello Alice
/hello Bob
```

## 输出

```
你好，World！
你好，Alice！
你好，Bob！
```
```

**命令 Markdown 格式规范**：
- 标题必须是 `# Command: /command-name`
- 包含用法、参数、示例和输出说明
- 使用代码块展示示例
- 清晰描述命令功能和行为

### 步骤 5：添加代理（可选）

在 `agents/` 目录下创建 Markdown 文件。

**示例**：`agents/helper.md`

```markdown
# Agent: Helper

我是一个通用助手代理。

## 角色定位

我可以帮助你：
- 回答问题
- 提供建议
- 执行任务

## 工作方式

当你向我提问时，我会：
1. 理解你的需求
2. 分析问题
3. 提供解决方案

## 使用示例

**你**：帮我写一个函数

**我**：好的，我来帮你写...

## 我的技能

- 编程能力
- 问题解决
- 任务规划
```

**代理 Markdown 格式规范**：
- 标题必须是 `# Agent: AgentName`
- 描述代理的角色、能力和工作方式
- 提供使用示例
- 说明代理的专长领域

### 步骤 6：添加技能（可选）

在 `skills/` 目录下创建子目录，每个技能一个目录，包含 `SKILL.md` 文件。

**示例**：`skills/my-skill/SKILL.md`

```markdown
# Skill: 我的技能

技能描述。

## 技能描述

这个技能使代理能够...

## 使用场景

- 场景 1：...
- 场景 2：...

## 核心能力

### 能力 1

描述和示例...

### 能力 2

描述和示例...

## 集成说明

这个技能会被以下代理使用：
- Agent1
- Agent2

## 版本历史

- v1.0.0 - 初始版本
```

**技能文件格式规范**：
- 标题必须是 `# Skill: 技能名称`
- 描述技能的功能和使用场景
- 说明核心能力
- 提供集成说明

### 步骤 7：添加事件钩子（可选）

创建 `hooks/hooks.json`：

```json
{
  "onLoad": {
    "description": "插件加载时触发",
    "action": "initPlugin"
  },
  "onCommand": {
    "description": "执行命令时触发",
    "action": "logCommand"
  },
  "onAgentActivate": {
    "description": "激活代理时触发",
    "action": "setupAgent"
  }
}
```

**支持的事件钩子**：
- `onLoad` - 插件加载时
- `onUnload` - 插件卸载时
- `onCommand` - 命令执行时
- `onAgentActivate` - 代理激活时
- `onAgentDeactivate` - 代理停用时
- 其他自定义事件

### 步骤 8：编写 README

创建 `README.md`，说明插件的功能、安装和使用方法。

### 步骤 9：测试插件

将插件复制到 Claude Code 插件目录进行测试：

**Windows**：
```powershell
Copy-Item -Recurse my-plugin "$env:APPDATA\Claude\plugins\my-plugin"
```

**macOS/Linux**：
```bash
cp -r my-plugin ~/.config/claude/plugins/my-plugin
```

重启 Claude Code 后测试插件功能。

## 最佳实践

### 1. 命名规范

**插件名称**：
- 使用小写字母和连字符：`my-plugin`
- 名称要简短且具有描述性
- 避免使用特殊字符

**命令名称**：
- 简短、易记：`/gen`, `/review`
- 使用动词表示动作：`/create`, `/list`
- 避免与系统命令冲突

**代理名称**：
- 首字母大写：`TaskAssistant`, `CodeReviewer`
- 使用名词或角色名称
- 清晰表达代理的功能

**技能名称**：
- 描述性名称：`项目规划`, `代码分析`
- 避免过于宽泛或模糊

### 2. 文档完整性

- ✅ 每个命令都有清晰的使用说明
- ✅ 每个代理都有明确的角色定位
- ✅ 每个技能都有详细的能力描述
- ✅ 提供丰富的使用示例
- ✅ 说明参数和选项

### 3. 版本管理

使用语义化版本号：
- `1.0.0` - 主版本.次版本.补丁版本
- 主版本：不兼容的 API 变更
- 次版本：向后兼容的功能新增
- 补丁版本：向后兼容的问题修正

### 4. 错误处理

- 提供友好的错误信息
- 说明错误原因和解决方法
- 验证输入参数
- 处理边界情况

### 5. 性能考虑

- 避免阻塞操作
- 合理使用缓存
- 优化大量数据处理
- 提供进度反馈

### 6. 安全性

- 不在代码中硬编码敏感信息
- 验证和清理用户输入
- 遵循最小权限原则
- 注意数据隐私

## 插件发布

### 1. 准备发布

- 完善文档
- 充分测试
- 更新版本号
- 编写更新日志

### 2. 发布清单

- [ ] README 文档完整
- [ ] 所有功能已测试
- [ ] 版本号已更新
- [ ] 更新日志已编写
- [ ] 示例代码可用
- [ ] 无明显 Bug

### 3. 分享插件

可以通过以下方式分享：
- Git 仓库
- 压缩包
- 插件市场（如果支持）

## 调试技巧

### 1. 查看日志

Claude Code 会记录插件加载和执行的日志。

### 2. 增量开发

一次只添加一个功能，确保每个功能都能正常工作。

### 3. 使用示例插件

参考现有插件（productivity-plugin、dev-tools-plugin）的实现。

### 4. 社区交流

在社区中寻求帮助和反馈。

## 常见问题

### Q: 插件加载失败怎么办？

A: 检查：
1. plugin.json 格式是否正确
2. 目录结构是否符合规范
3. 文件名和路径是否正确
4. 查看 Claude Code 的错误日志

### Q: 命令不生效怎么办？

A: 确保：
1. 命令文件在 commands/ 目录下
2. 文件名正确（文件名即命令名）
3. Markdown 格式符合规范
4. 重启了 Claude Code

### Q: 代理无法激活？

A: 检查：
1. 代理文件在 agents/ 目录下
2. 文件格式正确
3. 代理名称与文件名一致
4. 技能文件正确配置

### Q: 如何调试插件？

A: 
1. 查看 Claude Code 日志
2. 使用 console.log 输出调试信息
3. 逐步测试各个功能
4. 使用简化版本进行测试

## 参考资源

- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)
- [Markdown 语法指南](https://www.markdownguide.org/)
- [语义化版本规范](https://semver.org/lang/zh-CN/)
- 示例插件源代码

## 贡献

欢迎改进插件开发指南：
- 补充最佳实践
- 添加更多示例
- 完善文档说明
- 分享经验技巧

---

**祝你开发愉快！🚀**

