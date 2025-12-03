# Command: /review

对代码进行专业审查，提供改进建议的命令。

## 描述

/review 命令帮助开发者快速审查代码，识别潜在问题，提供最佳实践建议。

## 用法

```
/review [file] [options]
```

### 参数

- `file` - 要审查的文件路径（可选，默认审查当前文件）
- `--focus` - 审查重点（security, performance, style, all）
- `--depth` - 审查深度（quick, normal, deep）

## 示例

### 审查当前文件

```
/review
```

### 审查特定文件

```
/review src/components/UserList.jsx
```

### 专注于安全性审查

```
/review --focus security
```

### 深度审查

```
/review src/api/auth.js --depth deep
```

## 审查维度

### 1. 代码质量

检查项：
- ✅ 代码可读性
- ✅ 命名规范
- ✅ 函数复杂度
- ✅ 代码重复
- ✅ 注释完整性

### 2. 安全性

检查项：
- 🔒 SQL 注入风险
- 🔒 XSS 漏洞
- 🔒 CSRF 防护
- 🔒 敏感信息泄露
- 🔒 输入验证

### 3. 性能

检查项：
- ⚡ 算法效率
- ⚡ 内存使用
- ⚡ 数据库查询
- ⚡ 缓存策略
- ⚡ 异步处理

### 4. 最佳实践

检查项：
- 📚 设计模式使用
- 📚 SOLID 原则
- 📚 DRY 原则
- 📚  错误处理
- 📚 测试覆盖

## 审查报告示例

```markdown
# 代码审查报告

## 文件：src/api/user.js

### 总体评分：7.5/10

---

## 🔴 严重问题（必须修复）

### 1. SQL 注入风险
**位置**：第 45 行
**代码**：
```javascript
const query = `SELECT * FROM users WHERE id = ${userId}`;
```
**问题**：直接拼接用户输入到 SQL 查询
**建议**：使用参数化查询
```javascript
const query = 'SELECT * FROM users WHERE id = ?';
db.query(query, [userId]);
```

---

## 🟡 中等问题（建议修复）

### 2. 缺少错误处理
**位置**：第 78-85 行
**代码**：
```javascript
function getUserData(id) {
  const user = db.query('SELECT * FROM users WHERE id = ?', [id]);
  return user;
}
```
**问题**：没有处理数据库查询可能的错误
**建议**：添加 try-catch 错误处理
```javascript
async function getUserData(id) {
  try {
    const user = await db.query('SELECT * FROM users WHERE id = ?', [id]);
    return user;
  } catch (error) {
    logger.error('获取用户数据失败:', error);
    throw new Error('无法获取用户数据');
  }
}
```

### 3. 函数过于复杂
**位置**：第 120-180 行
**问题**：函数 `processUserRegistration` 有 60 行代码，圈复杂度为 12
**建议**：拆分为多个小函数
```javascript
// 拆分前
function processUserRegistration(userData) {
  // 60 行代码...
}

// 拆分后
function processUserRegistration(userData) {
  validateUserData(userData);
  const hashedPassword = hashPassword(userData.password);
  const user = createUser({ ...userData, password: hashedPassword });
  sendWelcomeEmail(user.email);
  logRegistration(user.id);
  return user;
}
```

---

## 🟢 轻微问题（可选修复）

### 4. 命名不够清晰
**位置**：第 25 行
**代码**：
```javascript
const d = new Date();
```
**建议**：使用更描述性的变量名
```javascript
const currentDate = new Date();
```

### 5. 缺少注释
**位置**：第 95-105 行
**问题**：复杂的业务逻辑缺少注释说明
**建议**：添加注释解释业务规则

---

## ✅ 做得好的地方

1. ✨ 代码格式统一，遵循 ESLint 规则
2. ✨ 使用了 async/await 处理异步操作
3. ✨ 变量命名总体清晰（除个别情况）
4. ✨ 使用了适当的常量定义

---

## 📊 代码指标

- **圈复杂度**：平均 5.2（目标 < 10）
- **函数长度**：平均 28 行（目标 < 50）
- **代码重复率**：3%（目标 < 5%）
- **注释覆盖率**：45%（目标 > 60%）

---

## 🎯 优先修复建议

1. **立即修复**：SQL 注入风险（第 45 行）
2. **本周修复**：添加错误处理（第 78-85 行）
3. **下次重构**：拆分复杂函数（第 120-180 行）

---

## 📚 推荐阅读

- [OWASP SQL 注入防护指南](https://owasp.org/www-community/attacks/SQL_Injection)
- [JavaScript 错误处理最佳实践](https://javascript.info/try-catch)
- [重构：改善既有代码的设计](https://refactoring.com/)
```

## 审查类型

### 快速审查（--depth quick）

- ⏱️ 时间：1-2 分钟
- 🎯 重点：明显的问题和常见错误
- 📋 报告：简洁的问题列表

### 常规审查（--depth normal，默认）

- ⏱️ 时间：3-5 分钟
- 🎯 重点：代码质量、安全、性能
- 📋 报告：详细的问题和建议

### 深度审查（--depth deep）

- ⏱️ 时间：10-15 分钟
- 🎯 重点：全面分析，包括架构设计
- 📋 报告：完整的审查报告和改进计划

## 审查清单

### 安全性
- [ ] 输入验证和清理
- [ ] SQL 注入防护
- [ ] XSS 防护
- [ ] 身份认证和授权
- [ ] 敏感数据处理

### 性能
- [ ] 算法效率
- [ ] 数据库查询优化
- [ ] 缓存使用
- [ ] 内存管理
- [ ] 异步处理

### 可维护性
- [ ] 代码结构清晰
- [ ] 函数单一职责
- [ ] 适当的注释
- [ ] 错误处理完整
- [ ] 测试覆盖充分

### 代码风格
- [ ] 命名规范
- [ ] 格式一致
- [ ] 代码简洁
- [ ] 避免重复
- [ ] 遵循最佳实践

## 集成建议

将代码审查集成到开发流程：

1. **提交前审查**：在 git commit 前运行快速审查
2. **PR 审查**：创建 Pull Request 时进行常规审查
3. **定期审查**：每周进行深度审查关键模块
4. **持续集成**：在 CI/CD 管道中自动运行审查

## 配置示例

```json
{
  "review": {
    "defaultDepth": "normal",
    "autoFix": false,
    "ignorePatterns": ["*.test.js", "*.spec.js"],
    "rules": {
      "security": "error",
      "performance": "warn",
      "style": "info"
    }
  }
}
```

## 特性

- 🔍 全面的代码分析
- 🎯 针对性的改进建议
- 📊 量化的代码指标
- 🚀 自动化审查流程
- 📚 学习最佳实践

## 相关命令

- `/gen` - 生成代码模板
- `/refactor` - 重构代码
- `/optimize` - 性能优化
- `/fix` - 自动修复问题

