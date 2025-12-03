# Dev Tools Plugin

面向开发者的专业工具插件，提供代码生成、审查、重构和架构设计支持。

## 插件信息

- **名称**：dev-tools-plugin
- **版本**：1.0.0
- **作者**：Your Name
- **类型**：开发工具

## 功能概览

这个插件为开发者提供专业的代码开发辅助工具：

- 🚀 快速生成代码模板
- 🔍 专业的代码审查
- 🏗️ 架构设计指导
- 🔧 重构建议和指导
- 📊 代码质量分析

## 包含的命令

### 1. /gen - 代码生成

快速生成各种代码模板和样板代码。

**支持的代码类型**：
- API 端点
- 数据模型
- 单元测试
- UI 组件
- CRUD 操作
- 中间件
- 配置文件

**用法**：
```
/gen api User
/gen model Product name:string price:number
/gen test UserService
/gen component Button
```

[详细文档](commands/gen.md)

### 2. /review - 代码审查

对代码进行全面审查，提供专业的改进建议。

**审查维度**：
- 代码质量
- 安全性
- 性能
- 最佳实践

**用法**：
```
/review
/review src/api/user.js
/review --focus security
/review --depth deep
```

[详细文档](commands/review.md)

## 包含的代理

### 1. CodeReviewer - 代码审查专家

专业的代码审查者，帮助你提高代码质量。

**专长**：
- 🔍 识别代码问题
- 🔒 发现安全漏洞
- ⚡ 性能优化建议
- 📚 最佳实践指导

**使用方式**：
```
@CodeReviewer 请审查这段代码
@CodeReviewer 这个设计有什么问题吗？
```

[详细文档](agents/code-reviewer.md)

### 2. Architect - 架构设计专家

软件架构师，帮助你设计可扩展的系统。

**专长**：
- 🏗️ 系统架构设计
- 📐 设计模式应用
- 🔄 架构重构方案
- 🎯 技术选型建议

**使用方式**：
```
@Architect 帮我设计一个电商系统
@Architect 我们的系统该怎么重构？
```

[详细文档](agents/architect.md)

## 包含的技能

### 1. 代码分析

深入分析代码质量，识别问题和改进空间。

**能力**：
- 质量指标计算
- 代码异味检测
- 安全漏洞扫描
- 性能问题识别

[详细文档](skills/code-analysis/SKILL.md)

### 2. 代码重构

系统化的重构指导和方案。

**能力**：
- 重构模式应用
- 安全重构流程
- 重构风险控制
- 最佳实践

[详细文档](skills/refactoring/SKILL.md)

## 安装方法

### Windows

```powershell
Copy-Item -Recurse plugins\dev-tools-plugin "$env:APPDATA\Claude\plugins\dev-tools-plugin"
```

### macOS/Linux

```bash
cp -r plugins/dev-tools-plugin ~/.config/claude/plugins/dev-tools-plugin
```

安装后重启 Claude Code。

## 使用场景

### 场景 1：快速开发

```
你: /gen api User
（生成 REST API 模板）

你: /gen test UserAPI
（生成对应的测试代码）

你: /review
（审查生成的代码）
```

### 场景 2：代码审查

```
你: @CodeReviewer 请审查这个文件

CodeReviewer: （提供详细的审查报告）
- 🔴 SQL 注入风险
- 🟡 缺少错误处理
- 🟢 代码结构清晰

你: 如何修复 SQL 注入问题？

CodeReviewer: （提供具体的修复方案和示例代码）
```

### 场景 3：架构设计

```
你: @Architect 我要开发一个博客系统，帮我设计架构

Architect: （提供完整的架构设计）
- 系统分层
- 技术选型
- 数据库设计
- 扩展方案

你: 如果用户增长到100万，该怎么扩展？

Architect: （提供扩展方案）
```

### 场景 4：重构现有代码

```
你: @CodeReviewer 这段代码有什么问题？
（粘贴代码）

CodeReviewer: 
- 🟡 函数过于复杂
- 🟡 存在代码重复
- 建议：提取函数、消除重复

你: 能给我重构方案吗？

CodeReviewer: （提供具体的重构步骤和代码）
```

## 配置选项

插件支持通过配置自定义行为：

```json
{
  "codeGeneration": {
    "defaultLanguage": "javascript",
    "template": "standard",
    "includeComments": true,
    "includeTests": true
  },
  "codeReview": {
    "defaultDepth": "normal",
    "focusAreas": ["security", "performance", "quality"],
    "autoFix": false
  },
  "analysis": {
    "complexityThreshold": 10,
    "duplicationThreshold": 5,
    "securityScan": true
  }
}
```

## 支持的语言和框架

### 后端
- JavaScript / Node.js / Express
- TypeScript / NestJS
- Python / Flask / Django / FastAPI
- Java / Spring Boot
- Go / Gin
- Rust / Actix

### 前端
- React / Next.js
- Vue / Nuxt.js
- Angular
- Svelte

### 数据库
- PostgreSQL
- MySQL
- MongoDB
- Redis

## 最佳实践

### 1. 开发流程

```
1. 使用 /gen 快速生成代码模板
2. 编写具体的业务逻辑
3. 使用 /review 进行代码审查
4. 根据建议进行改进
5. 编写测试用例
6. 提交代码
```

### 2. 代码审查

```
1. 开发完成后，先自己审查一遍
2. 使用 @CodeReviewer 进行自动审查
3. 重点关注安全和性能问题
4. 修复严重和中等问题
5. 请团队成员进行人工审查
```

### 3. 架构设计

```
1. 明确需求和约束
2. 与 @Architect 讨论架构方案
3. 评估不同方案的优劣
4. 选择最适合的方案
5. 编写架构文档
6. 团队评审
```

### 4. 重构策略

```
1. 识别需要重构的代码
2. 补充测试用例
3. 与 @CodeReviewer 讨论重构方案
4. 小步重构，频繁测试
5. 及时提交代码
6. 持续改进
```

## 高级功能

### 批量代码生成

```
/gen api User Post Comment --batch
```

### 自定义模板

```
/gen api User --template rest-advanced
```

### 深度架构分析

```
@Architect 分析我们的系统架构 --mode deep
```

### 安全审计

```
/review --focus security --report detailed
```

## 集成开发工具

### VS Code 集成

```json
{
  "claude.plugins": ["dev-tools-plugin"],
  "claude.autoReview": true,
  "claude.reviewOnSave": true
}
```

### Git Hooks

```bash
# pre-commit hook
#!/bin/sh
claude /review --focus security --staged
```

### CI/CD 集成

```yaml
# .github/workflows/code-review.yml
- name: Code Review
  run: |
    claude /review --depth deep --output report.md
```

## 常见问题

### Q: 代码生成的模板可以自定义吗？

A: 当前版本使用内置模板。未来版本会支持自定义模板。

### Q: 代码审查会自动修复问题吗？

A: 默认不会自动修复。可以启用 `autoFix` 选项进行自动修复（实验性功能）。

### Q: 支持哪些代码质量工具？

A: 插件内置了代码分析能力。也可以集成 ESLint、SonarQube 等外部工具。

### Q: 如何为特定项目配置规则？

A: 在项目根目录创建 `.clauderc` 文件，配置项目特定的规则。

## 贡献和反馈

欢迎：
- 报告 Bug
- 提出新功能建议
- 分享使用经验
- 贡献代码模板

## 更新日志

### v1.0.0 (2024-12-03)

- ✨ 初始版本发布
- 🚀 代码生成命令
- 🔍 代码审查命令
- 🤖 CodeReviewer 代理
- 🏗️ Architect 代理
- 📊 代码分析技能
- 🔧 重构技能

## 许可证

MIT License - 详见项目根目录 LICENSE 文件

---

**让我们一起写出更好的代码！🚀**

