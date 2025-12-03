# Skill: 代码分析

这个技能使代理能够深入分析代码质量、识别问题和提供改进建议。

## 技能描述

代码分析技能使 CodeReviewer 和 Architect 代理能够：
- 分析代码质量和复杂度
- 识别代码异味（Code Smells）
- 检测安全漏洞
- 评估性能问题
- 提供重构建议

## 分析维度

### 1. 代码质量指标

**圈复杂度（Cyclomatic Complexity）**
- 衡量代码路径数量
- 目标：< 10（简单）
- 警告：10-20（中等）
- 危险：> 20（复杂）

**认知复杂度（Cognitive Complexity）**
- 衡量代码理解难度
- 考虑嵌套、递归等因素

**代码行数**
- 函数：< 50 行
- 类：< 300 行
- 文件：< 500 行

**代码重复率**
- 目标：< 5%
- 警告：5-10%
- 危险：> 10%

### 2. 代码异味检测

**Bloaters（膨胀者）**
```
❌ 过长方法
function processOrder(order) {
  // 100+ 行代码
}

✅ 拆分为小函数
function processOrder(order) {
  validateOrder(order);
  calculateTotal(order);
  applyDiscounts(order);
  processPayment(order);
  updateInventory(order);
  sendConfirmation(order);
}
```

**Long Parameter List（长参数列表）**
```
❌ 参数过多
function createUser(name, email, age, phone, address, city, country, zip) {
  // ...
}

✅ 使用对象参数
function createUser(userData) {
  const { name, email, age, phone, address, city, country, zip } = userData;
  // ...
}
```

**Data Clumps（数据泥团）**
```
❌ 重复的数据组合
function drawCircle(x, y, radius) { }
function moveCircle(x, y, dx, dy) { }
function scaleCircle(x, y, factor) { }

✅ 封装为对象
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
}

class Circle {
  constructor(center, radius) {
    this.center = center;
    this.radius = radius;
  }
  
  draw() { }
  move(dx, dy) { }
  scale(factor) { }
}
```

**Primitive Obsession（基本类型偏执）**
```
❌ 滥用基本类型
function sendEmail(email) {
  if (!email.includes('@')) {
    throw new Error('Invalid email');
  }
  // ...
}

✅ 使用值对象
class Email {
  constructor(value) {
    if (!value.includes('@')) {
      throw new Error('Invalid email');
    }
    this.value = value;
  }
  
  toString() {
    return this.value;
  }
}

function sendEmail(email) {
  // email 已经是验证过的 Email 对象
  // ...
}
```

### 3. 安全分析

**注入攻击**
```
❌ SQL 注入
const query = `SELECT * FROM users WHERE id = ${userId}`;

✅ 参数化查询
const query = 'SELECT * FROM users WHERE id = ?';
db.query(query, [userId]);
```

**敏感信息泄露**
```
❌ 硬编码密钥
const API_KEY = 'sk-1234567890abcdef';

✅ 环境变量
const API_KEY = process.env.API_KEY;
```

**不安全的随机数**
```
❌ Math.random()
const token = Math.random().toString(36);

✅ 加密级随机数
const crypto = require('crypto');
const token = crypto.randomBytes(32).toString('hex');
```

### 4. 性能分析

**算法复杂度**
```
❌ O(n²) 嵌套循环
for (let i = 0; i < arr1.length; i++) {
  for (let j = 0; j < arr2.length; j++) {
    // ...
  }
}

✅ O(n) 使用哈希表
const map = new Map(arr2.map(item => [item.id, item]));
for (const item of arr1) {
  const match = map.get(item.id);
  // ...
}
```

**内存泄漏**
```
❌ 未清理事件监听
element.addEventListener('click', handler);
// 元素移除后，监听器仍然存在

✅ 及时清理
element.addEventListener('click', handler);
// 不再需要时
element.removeEventListener('click', handler);
```

**同步阻塞操作**
```
❌ 同步读文件
const data = fs.readFileSync('large-file.txt');

✅ 异步操作
const data = await fs.promises.readFile('large-file.txt');
```

## 分析流程

### 第一步：静态分析

```
1. 代码结构分析
   - 模块组织
   - 依赖关系
   - 命名规范

2. 质量指标计算
   - 圈复杂度
   - 代码行数
   - 重复率

3. 模式匹配
   - 代码异味
   - 反模式
   - 最佳实践违反
```

### 第二步：安全扫描

```
1. 漏洞检测
   - 注入攻击
   - XSS 漏洞
   - CSRF 风险

2. 依赖检查
   - 已知漏洞
   - 过时版本
   - 许可证问题

3. 敏感信息
   - 硬编码密钥
   - 密码明文
   - 个人信息
```

### 第三步：性能评估

```
1. 算法分析
   - 时间复杂度
   - 空间复杂度
   - 瓶颈识别

2. 资源使用
   - 内存占用
   - CPU 密集
   - I/O 操作

3. 优化建议
   - 缓存策略
   - 异步处理
   - 数据结构优化
```

### 第四步：生成报告

```
1. 问题分类
   - 严重问题
   - 中等问题
   - 轻微问题

2. 优先级排序
   - 影响程度
   - 修复难度
   - 风险评估

3. 改进建议
   - 具体方案
   - 示例代码
   - 参考资料
```

## 分析示例

### 输入代码

```javascript
function getUserOrders(userId) {
  var orders = [];
  for (var i = 0; i < allOrders.length; i++) {
    if (allOrders[i].userId == userId) {
      orders.push(allOrders[i]);
    }
  }
  return orders;
}
```

### 分析输出

```markdown
# 代码分析报告

## 问题列表

### 🟡 性能问题
**时间复杂度**：O(n)
- 当前实现需要遍历所有订单
- 随着数据量增长，性能会下降

**改进建议**：使用索引或缓存
```javascript
// 方案1：使用 Map 索引
const ordersByUser = new Map();
// 预处理建立索引
allOrders.forEach(order => {
  if (!ordersByUser.has(order.userId)) {
    ordersByUser.set(order.userId, []);
  }
  ordersByUser.get(order.userId).push(order);
});

function getUserOrders(userId) {
  return ordersByUser.get(userId) || [];
}

// 方案2：数据库查询
function getUserOrders(userId) {
  return db.query('SELECT * FROM orders WHERE user_id = ?', [userId]);
}
```

### 🟢 代码风格
**使用 var**：应该使用 const/let
**松散相等（==）**：应该使用严格相等（===）

**改进建议**：
```javascript
function getUserOrders(userId) {
  const orders = [];
  for (let i = 0; i < allOrders.length; i++) {
    if (allOrders[i].userId === userId) {
      orders.push(allOrders[i]);
    }
  }
  return orders;
}

// 更现代的写法
function getUserOrders(userId) {
  return allOrders.filter(order => order.userId === userId);
}
```

### ✅ 做得好的地方
- 函数命名清晰
- 功能单一
- 逻辑简单易懂

## 总体评分：7/10

## 建议优先级
1. 考虑性能优化方案
2. 更新代码风格
```

## 集成说明

这个技能会被以下代理自动使用：
- CodeReviewer - 进行代码审查时
- Architect - 评估架构质量时

激活条件：
- 用户请求代码审查
- 用户询问代码质量
- 用户寻求优化建议

## 技能配置

```json
{
  "complexityThreshold": 10,
  "lineLimitFunction": 50,
  "lineLimitClass": 300,
  "duplicationThreshold": 5,
  "securityScan": true,
  "performanceAnalysis": true
}
```

## 支持的语言

- JavaScript / TypeScript
- Python
- Java
- Go
- Rust
- PHP

## 版本历史

- v1.0.0 - 初始版本，支持基础代码分析功能

