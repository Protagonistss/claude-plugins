# Code Review Plugin

专业的代码审查插件，提供全面的代码质量分析、安全检查和性能优化建议。

## 🚀 功能特性

### 🔍 代码质量审查
- 全面的代码结构分析
- 代码复杂度评估
- 最佳实践检查
- 可维护性分析
- 代码重复检测

### 🔒 安全审查
- OWASP Top 10 安全风险检查
- SQL注入、XSS等常见漏洞检测
- 认证授权机制审查
- 敏感数据处理检查
- 加密实现验证

### ⚡ 性能分析
- 算法复杂度分析
- 资源使用评估
- 数据库查询优化
- 并发性能检查
- 内存泄漏检测

### 🤖 智能代理
- **CodeReviewer**: 全方位代码审查专家
- **SecurityExpert**: 专业安全审查专家

## 📋 安装方法

### 方法1: 直接复制插件目录
```bash
# 复制插件到 Claude Code 插件目录
cp -r plugins/code-review ~/.config/claude/plugins/code-review
```

### 方法2: 创建符号链接
```bash
# 在插件目录创建符号链接
ln -s /path/to/your/claude-plugins/plugins/code-review ~/.config/claude/plugins/code-review
```

### Windows 用户
```powershell
# 复制插件目录
Copy-Item -Recurse plugins\code-review "$env:APPDATA\Claude\plugins\code-review"
```

## 🎯 使用指南

### 基本命令

#### 全面代码审查
```bash
/review                    # 审查当前文件
/review src/              # 审查整个目录
/review file.js           # 审查特定文件
/review --focus security  # 专注于安全审查
/review --depth deep      # 深度审查模式
```

#### 专业安全审查
```bash
/security                     # 基本安全检查
/security --owasp            # 按OWASP标准检查
/security --compliance gdpr  # GDPR合规性检查
/security api/auth.js        # 审查特定文件
```

#### 性能分析
```bash
/performance                # 基本性能分析
/performance --metrics      # 详细性能指标
/performance --benchmark    # 基准测试对比
/performance algorithms/    # 分析算法性能
```

### 智能代理

#### 代码审查专家
```bash
@CodeReviewer 请审查这段代码的安全性
@CodeReviewer 帮我优化这个函数的性能
@CodeReviewer 这个架构设计合理吗？
```

#### 安全专家
```bash
@SecurityExpert 检查这个登录功能的安全问题
@SecurityExpert 分析可能的SQL注入风险
@SecurityExpert 这个加密实现安全吗？
```

## 📊 审查报告示例

### 代码质量报告
```markdown
# 代码审查报告

## 总体评分: 8.2/10
- 可读性: 9/10 ✅
- 复杂性: 7/10 ⚠️
- 可维护性: 8/10 ✅
- 健壮性: 8/10 ✅

## 🔴 严重问题 (1个)
### SQL注入漏洞 - 第45行
**风险**: 可能导致数据库泄露
**修复**: 使用参数化查询

## 🟡 重要问题 (3个)
### 1. 函数过于复杂 - handleUserUpdate() 75行
### 2. 缺少错误处理 - 第78-85行
### 3. 内存泄漏风险 - 事件监听器未清理

## 改进建议
1. 立即修复SQL注入漏洞
2. 重构复杂函数
3. 完善错误处理机制
```

### 安全审查报告
```markdown
# 安全审查报告

## 风险评级: 中等
- 严重漏洞: 0个 ✅
- 高危漏洞: 2个 ⚠️
- 中危漏洞: 5个 ⚠️
- 低危漏洞: 8个

## 🚨 高危问题
### 1. 弱密码策略
- 位置: auth.js:23
- 修复: 实施强密码要求

### 2. 缺少CSRF防护
- 位置: forms.js:45
- 修复: 添加CSRF token

## 📋 合规性检查
- ✅ GDPR基本要求
- ⚠️ 需要改进数据加密
- ❌ 缺少用户同意机制
```

### 性能分析报告
```markdown
# 性能分析报告

## 性能评分: 6.8/10
- 响应时间: 245ms (目标: <200ms)
- 吞吐量: 450 RPS (目标: >1000 RPS)
- CPU使用: 78% (目标: <70%)
- 内存使用: 1.8GB

## 🚀 主要优化机会
### 1. 数据库查询优化 (预计提升60%)
- 问题: N+1查询
- 解决: 使用JOIN查询

### 2. 缓存策略 (预计提升40%)
- 建议: 实施Redis缓存
- 热点数据: 用户信息、配置

## 📊 性能对比
| 操作 | 优化前 | 优化后 | 提升 |
|------|--------|--------|------|
| 用户列表 | 892ms | 245ms | 72% |
| 用户搜索 | 2.3s | 340ms | 85% |
```

## ⚙️ 配置选项

### 创建配置文件
在项目根目录创建 `.codereview.json`:

```json
{
  "review": {
    "defaultDepth": "standard",
    "autoFix": false,
    "ignorePatterns": [
      "*.test.js",
      "*.spec.js",
      "node_modules/**",
      "dist/**"
    ],
    "rules": {
      "security": {
        "enabled": true,
        "severity": "error"
      },
      "performance": {
        "enabled": true,
        "severity": "warn"
      },
      "style": {
        "enabled": true,
        "severity": "info"
      }
    },
    "customRules": [
      {
        "name": "no-console-in-production",
        "pattern": "console\\.",
        "message": "生产环境不应该有console语句"
      }
    ]
  },
  "security": {
    "owasp": true,
    "compliance": ["gdpr"],
    "excludeDevDependencies": true
  },
  "performance": {
    "maxComplexity": 10,
    "maxFunctionLength": 50,
    "benchmark": true
  }
}
```

### Git Hooks 集成

#### Pre-commit Hook
```bash
#!/bin/sh
# .git/hooks/pre-commit

echo "🔍 运行代码审查..."

# 运行安全检查
npx claude /security --focus critical

# 检查代码风格
npm run lint

# 运行测试
npm test

echo "✅ 代码审查通过"
```

#### Pre-push Hook
```bash
#!/bin/sh
# .git/hooks/pre-push

echo "🚀 运行完整代码审查..."

# 全面代码审查
npx claude /review --depth standard

# 性能分析
npx claude /performance

# 生成报告
npx claude /review --format report > review-report.md

echo "✅ 推送前审查完成"
```

## 🔗 CI/CD 集成

### GitHub Actions
```yaml
# .github/workflows/code-review.yml
name: Code Review

on:
  pull_request:
    branches: [ main ]

jobs:
  review:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '18'

    - name: Install dependencies
      run: npm ci

    - name: Run security review
      run: npx claude /security --owasp

    - name: Run performance analysis
      run: npx claude /performance --metrics

    - name: Generate review report
      run: npx claude /review --format report > review-report.md

    - name: Upload review report
      uses: actions/upload-artifact@v2
      with:
        name: review-report
        path: review-report.md

    - name: Comment PR
      uses: actions/github-script@v6
      with:
        script: |
          const fs = require('fs');
          const report = fs.readFileSync('review-report.md', 'utf8');

          github.rest.issues.createComment({
            issue_number: context.issue.number,
            owner: context.repo.owner,
            repo: context.repo.repo,
            body: `## 📋 代码审查报告\n\n${report}`
          });
```

## 📚 最佳实践

### 开发阶段
1. **编码前**: 了解安全编码规范
2. **编码中**: 遵循代码质量标准
3. **提交前**: 运行快速代码审查
4. **发布前**: 进行全面安全检查

### 团队协作
1. **统一标准**: 建立团队代码规范
2. **定期审查**: 安排定期代码审查会议
3. **知识分享**: 分享安全最佳实践
4. **持续改进**: 根据审查结果改进流程

### 安全优先
1. **威胁建模**: 在设计阶段考虑安全威胁
2. **最小权限**: 遵循最小权限原则
3. **深度防御**: 实施多层安全控制
4. **持续监控**: 建立安全监控机制

## 🛠️ 故障排除

### 常见问题

#### 插件无法加载
```bash
# 检查插件路径
ls -la ~/.config/claude/plugins/

# 重新安装插件
rm -rf ~/.config/claude/plugins/code-review
cp -r plugins/code-review ~/.config/claude/plugins/
```

#### 命令无法执行
```bash
# 检查语法
claude --help
/review --help

# 重启 Claude Code
# 确保插件正确加载
```

#### 性能分析超时
```json
// 配置文件中调整超时设置
{
  "performance": {
    "timeout": 60000,
    "skipLargeFiles": true
  }
}
```

### 调试模式
```bash
# 启用调试日志
export CODE_REVIEW_DEBUG=true
claude /review --debug
```

## 📖 学习资源

### 安全学习
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [安全编码实践](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)
- [CVE漏洞数据库](https://cve.mitre.org/)

### 性能优化
- [Web性能优化](https://developers.google.com/web/fundamentals/performance/)
- [算法复杂度分析](https://www.bigocheatsheet.com/)
- [数据库优化指南](https://www.percona.com/blog/)

### 代码质量
- [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350884)
- [重构：改善既有代码的设计](https://refactoring.com/)
- [代码审查最佳实践](https://google.github.io/eng-practices/review/)

## 🤝 贡献指南

欢迎贡献代码、报告问题或提出改进建议：

1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'Add amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 创建 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🆘 支持

如果您遇到问题或需要帮助：

- 📧 邮箱: protagonisths@gmail.com
- 🐛 问题反馈: [GitHub Issues](https://github.com/Protagonisths/claude-plugins/issues)
- 📖 文档: [项目Wiki](https://github.com/Protagonisths/claude-plugins/wiki)

---

**让我们一起写出更安全、更高效、更优雅的代码！** 🚀