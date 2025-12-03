# Productivity Plugin

生产力增强插件，提供任务管理、时间追踪和效率提升工具。

## 插件信息

- **名称**：productivity-plugin
- **版本**：1.0.0
- **作者**：Your Name
- **类型**：生产力工具

## 功能概览

这个插件提供了一套完整的生产力工具，帮助你：

- ✅ 管理待办事项
- 🎯 保持专注
- ⏰ 优化时间使用
- 📊 跟踪任务进度

## 包含的命令

### 1. /todo - 待办事项管理

快速管理你的待办事项列表。

**用法**：
```
/todo add 完成项目文档
/todo list
/todo done 1
/todo remove 2
```

[详细文档](commands/todo.md)

### 2. /focus - 专注模式

启动专注模式，提高工作效率。

**用法**：
```
/focus on
/focus 完成代码审查
/focus off
```

[详细文档](commands/focus.md)

## 包含的代理

### TaskAssistant - 任务管理助手

你的个人任务管理专家，帮助你规划、组织和完成工作。

**特点**：
- 📋 任务分解
- 🎯 优先级排序
- ⏰ 时间估算
- 📊 进度追踪

**使用方式**：
```
@TaskAssistant 帮我规划一下开发用户登录功能
@TaskAssistant 这三个任务哪个应该先做？
```

[详细文档](agents/task-assistant.md)

## 包含的技能

### 1. 项目规划

帮助代理进行项目规划和任务分解。

**能力**：
- 任务分解
- 时间估算
- 依赖管理
- 里程碑设定

[详细文档](skills/project-planning/SKILL.md)

### 2. 时间管理

优化时间使用和提高工作效率。

**方法**：
- 番茄工作法
- 时间块技术
- 艾森豪威尔矩阵
- 三点估算法

[详细文档](skills/time-management/SKILL.md)

## 安装方法

### Windows

```powershell
Copy-Item -Recurse plugins\productivity-plugin "$env:APPDATA\Claude\plugins\productivity-plugin"
```

### macOS/Linux

```bash
cp -r plugins/productivity-plugin ~/.config/claude/plugins/productivity-plugin
```

安装后重启 Claude Code。

## 使用场景

### 场景 1：开始新项目

```
你: @TaskAssistant 我需要开发一个博客系统

TaskAssistant: 好的，让我帮你规划这个项目...
（提供详细的任务分解和时间估算）

你: /todo add 设计数据库结构
你: /todo add 实现后端API
你: /focus 设计数据库结构
```

### 场景 2：日常任务管理

```
你: /todo list
（查看今天的任务）

你: @TaskAssistant 这些任务应该按什么顺序做？
（获得优先级建议）

你: /focus on
（开始专注工作）

你: /todo done 1
（完成任务）
```

### 场景 3：时间规划

```
你: @TaskAssistant 我今天有这些任务，帮我安排时间

TaskAssistant: 根据你的任务，我建议这样安排...
（提供详细的时间安排方案）
```

## 配置选项

插件支持通过配置文件自定义行为（未来版本）：

```json
{
  "pomodoro": {
    "workTime": 25,
    "shortBreak": 5,
    "longBreak": 15
  },
  "taskStorage": {
    "persistent": false,
    "syncAcrossDevices": false
  }
}
```

## 最佳实践

1. **每天开始时**
   - 使用 `/todo list` 查看任务
   - 请 TaskAssistant 帮助排优先级
   - 用 `/focus` 开始最重要的任务

2. **项目规划时**
   - 与 TaskAssistant 讨论项目需求
   - 获取任务分解和时间估算
   - 使用 `/todo` 创建任务列表

3. **需要专注时**
   - 启用 `/focus` 模式
   - 应用番茄工作法
   - 避免频繁任务切换

## 常见问题

### Q: 任务列表会持久保存吗？

A: 当前版本任务存储在会话中，重启后会清空。未来版本会支持持久化存储。

### Q: 可以自定义番茄钟时长吗？

A: 当前使用标准的 25/5 分钟周期。自定义功能将在未来版本中添加。

### Q: TaskAssistant 可以管理团队任务吗？

A: 当前版本主要面向个人任务管理。团队协作功能在规划中。

## 更新日志

### v1.0.0 (2024-12-03)

- ✨ 初始版本发布
- ✅ 支持待办事项管理
- 🎯 专注模式
- 🤖 TaskAssistant 代理
- 📊 项目规划技能
- ⏰ 时间管理技能

## 贡献

欢迎提出改进建议和新功能想法！

## 许可证

MIT License - 详见项目根目录 LICENSE 文件

