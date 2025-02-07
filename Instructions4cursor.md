# 🛠️ 代码工具使用指南

> 本指南旨在帮助开发者更高效地使用代码工具套件。通过合理使用这些工具，可以显著提升代码开发和维护效率。

---

## 🔍 代码搜索类工具

### a) codebase_search
- **用途**: 语义化搜索代码
- **最佳场景**: 当需要理解某个功能或查找相似实现时
- **示例**: "请搜索所有与资源日志记录相关的代码"

### b) grep_search
- **用途**: 精确文本/正则搜索
- **最佳场景**: 当知道具体的函数名、变量名时
- **示例**: "查找所有使用 NewGPTTranslator 的地方"

### c) file_search
- **用途**: 模糊文件名搜索
- **最佳场景**: 记得部分文件名但不确定完整路径
- **示例**: "查找包含 resource_log 的文件"

---

## 📁 文件操作类工具

### a) read_file
- **用途**: 读取文件内容
- **最佳场景**: 需要查看具体代码实现
- **示例**: "查看 service.go 中的 makeTTS 函数实现"

### b) edit_file
- **用途**: 修改文件内容
- **最佳场景**: 需要修改代码
- **示例**: "修改 TTS 调用时的 ProjectID 参数"

### c) delete_file
- **用途**: 删除文件
- **最佳场景**: 需要删除不再需要的文件
- **示例**: "删除旧的测试文件"

### d) list_dir
- **用途**: 列出目录内容
- **最佳场景**: 了解目录结构
- **示例**: "查看 services 目录下有哪些文件"

---

## ⚡️ 命令执行类工具

### a) run_terminal_cmd
- **用途**: 执行终端命令
- **最佳场景**: 需要运行命令行操作
- **示例**: "运行测试命令"

---

## ✏️ 编辑修复类工具

### a) reapply
- **用途**: 重新应用上一次的编辑
- **最佳场景**: 当 edit_file 的结果不符合预期
- **示例**: "重新应用刚才的代码修改"

---

## 💡 使用这些工具的最佳实践

### 1️⃣ 信息收集阶段
- 使用 `list_dir` 了解项目结构
- 使用 `file_search` 定位相关文件
- 使用 `codebase_search` 查找相关实现
- 使用 `grep_search` 精确定位

### 2️⃣ 代码分析阶段
- 使用 `read_file` 查看具体实现
- 使用 `codebase_search` 查找类似代码
- 使用 `grep_search` 查找依赖关系

### 3️⃣ 修改实现阶段
- 使用 `edit_file` 修改代码
- 必要时使用 `reapply` 重新应用修改
- 使用 `run_terminal_cmd` 执行测试

### 4️⃣ 验证阶段
- 使用 `read_file` 确认修改
- 使用 `run_terminal_cmd` 运行测试
- 使用 `grep_search` 检查相关影响

---

## 📝 实际应用示例：视频翻译资源记录

### 1. 发现问题
   - 使用 `codebase_search` 搜索 "resource_log.Log"
   - 了解其他地方的使用方式

### 2. 定位代码
   - 使用 `read_file` 查看 service.go
   - 找到 TTS 调用的实现

### 3. 修改实现
   - 使用 `edit_file` 修改 ProjectID
   - 确保修改符合预期

### 4. 验证修改
   - 使用 `read_file` 确认修改
   - 检查相关测试是否需要更新

---

## ⚠️ 工具使用提醒方式

### 1. 直接指定工具使用
- ✅ "请使用 `codebase_search` 搜索所有与资源日志记录相关的代码"
- ✅ "请使用 `grep_search` 查找所有使用 NewGPTTranslator 的地方"
- ✅ "请使用 `file_search` 查找包含 resource_log 的文件"

### 2. 说明工具选择原因
- 💭 "这里需要精确匹配，应该使用 `grep_search`"
- 💭 "我们需要看完整上下文，请用 `read_file` 查看整个文件"

### 3. 指出当前方法的问题
- ⚠️ "`codebase_search` 可能会遗漏一些结果，请改用 `grep_search`"
- ⚠️ "只看部分文件内容可能会遗漏重要信息，请读取完整文件"

### 4. 提供更多上下文
- 📋 "我们在找具体的函数调用，请用 `grep_search` 搜索 'NewGPTTranslator('"
- 📋 "这个文件的其他部分也很重要，请用 `read_file` 查看完整内容"

---

## 🔄 工具组合使用场景

### 1. 代码重构
- 先用 `codebase_search` 找到相关代码
- 用 `grep_search` 确认所有调用点
- 用 `read_file` 详细检查
- 用 `edit_file` 进行修改
- 用 `run_terminal_cmd` 运行测试

### 2. 问题排查
- 用 `file_search` 定位相关文件
- 用 `grep_search` 查找错误信息
- 用 `read_file` 分析代码
- 用 `codebase_search` 寻找类似问题

---

## ❓ 常见问题

### Q: 如何选择 codebase_search 和 grep_search？
A: 当需要理解功能时用 codebase_search，当需要精确查找时用 grep_search

### Q: edit_file 修改失败怎么办？
A: 可以使用 reapply 工具重新应用修改，或调整修改内容再次尝试

### Q: 如何确保搜索结果完整？
A: 建议组合使用 codebase_search 和 grep_search，互相补充
