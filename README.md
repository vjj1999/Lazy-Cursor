# Lazy-Cursor - AI 辅助开发最佳实践 🚀

> 一个基于 Cursor AI 的智能开发助手配置项目，旨在通过 AI 提升开发效率和代码质量。

## 项目特点 ✨

- 🤖 **AI 驱动开发** - 利用 Cursor AI 提供智能化的开发辅助
- 📝 **标准化规范** - 提供完整的项目开发规范和最佳实践
- 🔄 **工作流优化** - 优化开发流程，提高团队协作效率
- 🛠️ **易于配置** - 简单的配置步骤，快速集成到现有项目
- 📈 **持续改进** - 通过 AI 反馈不断优化开发流程

## 快速开始 🚀

### 前置要求

1. 安装 [Cursor Editor](https://cursor.sh/)
2. 启用 Claude 3 Sonnet 模型

### 安装步骤

1. 克隆项目到本地
```bash
git clone https://github.com/vjj1999/Lazy-Cursor.git
```

2. 复制配置文件到你的项目
```bash
cp awesome-rules/.cursorrules your-project/
```

3. 根据需要调整配置（可选）

### 验证安装

1. 在 Cursor 中打开你的项目
2. 使用快捷键 `Cmd/Ctrl + K` 打开 AI 助手
3. 输入 "你好，请确认配置是否生效" 进行测试

## 详细配置 🔧

### 1. Cursor Settings 配置

1. 打开 Cursor Settings
2. 导航到 `Features > Chat & Composer`
3. 启用以下设置：
   ```
   ✓ Enable YOLO mode
   ```
4. 在 `Models` 中：
   ```
   启用claude 3 sonnet & o1 mini
   ```

### 2. AI Rules 设置

1. 在项目根目录创建 `.cursorrules` 文件，复制本项目的 `.cursorrules` 文件内容
2. 添加基础 AI 规则：
```
you are claude.
you can use <edit_file> tool.
please use chinese.
please make sure that the task can be executed step by step.
```

### 3. 验证配置

1. 打开 Composer（`Cmd/Ctrl + Shift + P`）
2. 输入测试指令：
```
请确认当前配置是否生效
```

3. 检查响应是否：
   - 使用中文
   - 遵循步骤化
   - 符合项目规范

## 项目结构 📁

```
project_root/
  ├── .cursorrules/        # Cursor AI 规则
  │   ├── common/         # 通用规则
  │   ├── language/       # 语言特定规则
  │   └── framework/      # 框架特定规则
  ├── api/               # API 文档和 Swagger 文件
  ├── controller/        # HTTP 处理器
  ├── logic/            # 业务逻辑
  ├── repository/       
  │   ├── dto/         # 请求对象
  │   ├── vo/          # 响应对象
  │   └── model/       # 数据库模型
  ├── services/         
  │   ├── xxx_service/ # 复杂业务服务
  │   └── xxx/         # 工具服务
  ├── middleware/       # 全局中间件
  ├── third_party/     # 第三方集成
  ├── constant/
  │   └── errcode/     # 错误码
  ├── tests/           # 测试文件
  ├── util/            # 工具函数
  └── scripts/         # 数据库迁移脚本
```
## 项目规范生成 📝

### 1. 项目规范

1. 确保 `.cursorrules` 位于根目录
2. 打开 Composer（`Cmd/Ctrl + Shift + P`）
3. 输入指令生成规范：
```
Use codebase_search and View <# Project Guidelines> tags in .cursorrules. Replace the <# Project Guidelines> tags in .cursorrules according to the project structure and the corresponding Unified Middleware. The content of the tags is required to meet the needs of the workflow and strictly express the project guidelines.
```

### 2. 需求文档生成

1. 创建 `requirement.md` 文件，包含：
   - 需求描述
   - 原型图
   - UI 草图
   
2. 在 Composer 中将 requirement.cursorrules 加入上下文（@Suggested），输入：
```
Based on requirement.md, supplemented with a complete requirements document.
```

## Cursor 使用指南 🛠️

### 1. 模型选择

- **Sonnet 3.5**
  - 适用：代码生成、修改、补全
  - 特点：响应快速、代码质量高
  - 实践：提供完整上下文信息

- **o1 mini**
  - 适用：需求分析、架构设计、代码审查
  - 特点：推理能力强、输出结构化
  - 实践：用于项目规划阶段

### 2. 快捷键指南

- `Cmd/Ctrl + K`: 打开 Composer
- `Cmd/Ctrl + L`: 打开 Chat
- `Cmd/Ctrl + I`: Chat 内容移至 Composer
- `Cmd/Ctrl + /`: 切换模型
- `Cmd/Ctrl + Enter`: 使用代码库上下文

### 3. 上下文管理
- `@file`: 添加文件到上下文
- `@folder`: 添加文件夹到上下文
- `@web`: 使用网络信息
- `@git`: 添加 git 上下文

## 工具使用指南 (introduction4cursor.md)

这是一个全面的cursor指令集，帮助开发者更高效地控制cursor：

### 1. 代码搜索工具 🔍
- **codebase_search**: 语义化代码搜索，适用于理解功能和查找相似实现
- **grep_search**: 精确文本/正则搜索，适用于查找具体的函数或变量
- **file_search**: 模糊文件名搜索，帮助快速定位文件

### 2. 文件操作工具 📁
- **read_file**: 读取文件内容，查看代码实现
- **edit_file**: 修改文件内容，进行代码更新
- **delete_file**: 删除不需要的文件
- **list_dir**: 浏览目录结构

### 3. 命令执行工具 ⚡️
- **run_terminal_cmd**: 执行终端命令，支持各种命令行操作

### 4. 编辑修复工具 ✏️
- **reapply**: 重新应用上一次的编辑，优化编辑结果

## 开发流程最佳实践 💡

### 1. 需求分析
```
1. 使用 o1 mini 分析需求文档
2. 添加相关文档到上下文
3. 生成任务分解和实现计划
4. 使用 Cmd+I 转到 Composer
```

### 2. 代码实现
```
1. 使用 Sonnet 3.5 生成代码
2. 添加相关文件(@file)
3. 遵循项目规范和分层标准
4. 分步实现，持续验证
```

### 3. 代码审查
```
1. 使用 o1 mini 审查代码
2. 添加 git 差异(@git)
3. 检查规范遵循情况
4. 优化和修复问题
```

## 项目规范参考 📚

### 分层标准

#### Controller 层
```go
func (ctrl *UserController) Create(c *gin.Context) {
    ctx := application.TraceCtx(c.Request.Context())
    
    var req dto.CreateUserRequest
    if err := c.ShouldBindJSON(&req); err != nil {
        return echo.Error(c, errcode.InvalidParams, err)
    }
    
    user, err := ctrl.logic.CreateUser(ctx, req)
    if err != nil {
        return echo.Error(c, err)
    }
    
    return echo.Success(c, user)
}
```

#### Logic 层
```go
func (l *UserLogic) CreateUser(ctx context.Context, req dto.CreateUserRequest) (*vo.UserVO, error) {
    if err := l.validateUser(ctx, req); err != nil {
        return nil, errs.NewBusinessErr(errs.ValidationFailed, err.Error())
    }
    
    tx := model.BeginCtxTx(ctx)
    defer tx.Rollback()
    
    user, err := l.userRepo.Create(ctx, req.ToModel())
    if err != nil {
        return nil, err
    }
    
    if err := tx.Commit(); err != nil {
        return nil, err
    }
    
    return vo.FromUser(user), nil
}
```

## 团队协作 👥

### 1. 规范统一
- 统一 Cursor 配置
- 共享提示模板
- 制定 AI 辅助编码规范
- 维护最佳实践文档

### 2. 知识共享
- 维护团队 cursorrules
- 分享有效提示模式
- 记录常见问题解决方案
- 定期更新最佳实践

### 3. 质量控制
- AI 生成代码审查标准
- 代码质量基线
- 自动化测试覆盖
- 性能指标监控

## 注意事项 ⚠️

### 1. 性能优化
- 合理使用模型配额
- 优化上下文大小
- 避免重复生成
- 缓存常用提示

### 2. 安全考虑
- 避免提交敏感信息
- 审查生成的代码
- 遵循安全最佳实践
- 定期更新规则

### 3. 持续改进
- 收集使用数据
- 优化工作流程
- 更新最佳实践
- 跟踪新功能发布

记住：Cursor 是辅助工具，最终代码质量和决策仍需要开发者的专业判断。定期检查和更新这些最佳实践，确保它们与项目需求和团队发展保持一致。

[参考资料]
- [Cursor Documentation](https://docs.cursor.com)
- [项目 GitHub 仓库](https://github.com/vjj1999/Lazy-Cursor)

## 使用示例 💡

### 1. 代码生成

```bash
# 在 Cursor 中输入
请帮我生成一个用户注册的 API 接口，包含参数验证和错误处理
```

AI 助手将根据项目规范生成符合要求的代码。

### 2. 代码优化

```bash
# 在 Cursor 中输入
请帮我优化这段代码的性能，并确保符合项目规范
```

AI 助手将分析代码并提供优化建议。

### 3. 文档生成

```bash
# 在 Cursor 中输入
请为这个函数生成完整的文档注释
```

AI 助手将生成符合规范的文档注释。

## 最佳实践 👍

### 1. 提示词编写

- 使用清晰、具体的描述
- 提供必要的上下文信息
- 说明特殊要求或约束

### 2. 代码审查

- 让 AI 助手参与代码审查
- 检查代码规范遵循情况
- 获取优化建议

### 3. 文档维护

- 及时更新文档
- 保持注释和文档的一致性
- 使用 AI 辅助生成文档

## 常见问题 ❓

### 1. 配置未生效？

- 检查 `.cursorrules` 文件位置是否正确
- 确认 Cursor 设置是否正确
- 重启 Cursor 编辑器

### 2. AI 响应不符合预期？

- 检查提示词是否清晰
- 提供更多上下文信息
- 适当调整配置参数

### 3. 如何自定义规范？

- 修改 `.cursorrules` 文件
- 添加自定义规则
- 调整现有规范

## 贡献指南 🤝

欢迎提交 Issue 和 Pull Request 来帮助改进项目。在贡献之前，请：

1. 查看现有的 Issue 和 PR
2. 遵循项目的代码规范
3. 提供清晰的描述和文档

## 许可证 📄

本项目采用 BSD-2-Clause 许可证 - 详见 [LICENSE](LICENSE) 文件
