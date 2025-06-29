# real-time_communicate_with_cursor
A comprehensive set of interactive communication rules designed specifically for Cursor AI, effectively preventing AI from going down the wrong path and enabling timely error correction and direction adjustment.

## 📖 Project Background

When using Cursor's Agent mode for development, we often encounter the following issues:

- **AI Going Down the Wrong Path**: When encountering errors, AI may adopt unreasonable solutions, such as simulating server functionality in test code instead of starting a real server
- **Lack of User Participation**: AI completes what it considers correct operations and directly ends the conversation, leaving users unable to timely review and provide feedback
- **Error Accumulation**: Users cannot intervene at critical steps, leading to continuous error accumulation
- **Resource Waste**: Users' new ideas cannot be communicated in time, wasting tokens and development resources

## 🎯 Solution

This project provides a complete set of interactive communication rules that achieve the following through user confirmation using `echo` commands at key nodes:

- ✅ **Timely Error Correction**: Pause and wait for user confirmation before each critical step
- ✅ **Enhanced Participation**: Users can participate in and control the development process in real-time
- ✅ **Prevent Error Accumulation**: Get user feedback before problems occur
- ✅ **Save Resources**: Reduce token waste caused by wrong directions

## 🚀 How to Use

### Basic Configuration

Add the following rules to your Cursor prompts:

```
# Instruction: Adopt a "Dialog-Style" Communication Mechanism
- **Use the `echo "confirmation_message"` command to confirm with the user in the following situations**:
  - Before modifying any file or directory (e.g., `echo "About to modify file: <filename>, proceed? [Yes]/No"`).
  - Before deciding to execute any command (e.g., `echo "Planned command execution: <command>, proceed? [Yes]/No"`).
  - After completing any task (e.g., `echo "<Task> is now complete. Confirm? [Yes]/No"`).
  - When encountering uncertain or high-risk operations (e.g., data deletion or major changes).
  - Any other situation where user intervention might be needed (at least once every 3 interactions).
- **Confirmation message format requirements**:
  - Must include a confirmation statement with options, clearly marking the default option in square brackets.
  - Example: `"Accept changes? [Yes]/No"` or `"Select action type: [Overwrite]/Skip/Cancel"`.
- **Dialog Mode Toggle**:
  - Maintain dialog-style communication by default.
  - Upon receiving `use dialog` instruction: **Enhance confirmation mechanism** (mandatory confirmation for critical steps).
  - Upon receiving `dont use dialog` instruction: **Disable confirmation mechanism** (only confirm for extremely high-risk operations).
    - Dialog-style communication resumes after receiving `use dialog`.

# Why Use "Dialog-Style" Communication?
- **If not used**:
  - AI errors may accumulate without allowing user correction mid-process.
  - New user ideas cannot be communicated promptly, wasting tokens and resources.
- **If used**:
  - Enables real-time error correction and directional adjustments.
  - Enhances user participation and sense of control.
- **Additional Tip**: Encourage the AI to proactively raise questions or suggestions (e.g., "Should this step be optimized?") to stimulate creative responses.

# Fundamental Principles of "Dialog-Style" Communication
- **Provide frequent confirmation opportunities**: Pause at critical steps and wait for user input (must provide clear options).
- **Avoid "plowing ahead"**: If the user rejects an operation without new instructions, stop and request guidance (e.g., `echo "Operation canceled. Provide new instructions: [Continue]/Terminate"`).
- **Ensure efficiency**: Confirmation messages must be complete and include options to minimize comprehension effort.
- **Default option design**: The bracketed option should represent the conventional choice (e.g., `[Continue]` is preferable to `[Cancel]` unless cancellation is desired).
```

## ⚡ Advanced Tips

### Dynamic Interactive Mode Adjustment
```bash
# Enable enhanced confirmation mode
use interactive

# Disable interactive mode (only keep high-risk confirmations)
dont use interactive
```

### Utilizing Cursor's Command Modification Feature
In Cursor, you can modify the echo command content that AI is about to execute, achieving real-time instruction communication:

![modify the echo command content](https://github.com/abigass/real-time_communicate_with_cursor/raw/main/modify_echo.gif)  

## 🤝 Contributing

Welcome to submit Issues and Pull Requests to improve this rule set. If you have better practical experience or discover new application scenarios, please feel free to share.

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

**Make AI development more controllable and collaboration more efficient!** 🚀 

---
# Cursor 对话式沟通提示词

一个专为 Cursor AI 设计的对话式沟通规则集，有效防止 AI 一错到底，实现及时纠错和方向调整。

## 📖 项目背景

在使用 Cursor 的 Agent 模式进行开发时，经常会遇到以下问题：

- **AI 一错到底**：遇到错误时 AI 可能采用不合理的解决方案，比如在测试代码中模拟服务器功能而不是启动真实服务器
- **缺乏用户参与**：AI 完成自认为正确的操作后直接结束对话，用户无法及时验收和反馈
- **错误累积**：用户无法在关键步骤进行干预，导致错误不断累积
- **资源浪费**：用户的新想法无法及时传达，浪费 token 和开发资源

## 🎯 解决方案

本项目提供了一套完整的对话式沟通规则，通过在关键节点使用 `echo` 命令与用户确认，实现：

- ✅ **及时纠错**：在每个关键步骤前暂停等待用户确认
- ✅ **提升参与感**：用户能够实时参与和控制开发过程
- ✅ **避免错误累积**：在问题发生前就能得到用户反馈
- ✅ **节省资源**：减少因错误方向导致的 token 浪费

## 🚀 使用方法

### 基础配置

将以下规则添加到你的 Cursor 提示词中：

```
# 指令：采用“对话式”沟通机制
- **在以下时机，使用 `echo "确认消息"` 命令向用户确认**：
  - 每次修改文件或目录前（例如：`echo "即将修改文件：<文件名>，是否继续？[是]/否"`）。
  - 每次决定执行命令前（例如：`echo "计划执行命令：<命令>，是否继续？[是]/否"`）。
  - 每次完成任务之后（例如：`echo "<任务>现已完成，是否确认？[是]/否"`）。
  - 每次遇到不确定性或高风险操作时（如数据删除或重大变更）。
  - 任何其他您认为用户可能需要干预的时机（至少每3步交互一次）。
- **确认消息格式要求**：
  - 必须包含带选项的确认语句，用中括号标注默认选项
  - 示例：`"是否接受修改？[是]/否"` 或 `"选择操作类型：[覆盖]/跳过/取消"`
- **对话模式开关**：
  - 默认保持对话式沟通
  - 当收到 `use 对话` 指令时：**强化确认机制**（关键步骤必须确认）
  - 当收到 `dont use 对话` 指令时：**不再进行确认机制**（仅极高风险操作需确认）
    - 之后收到 `use 对话` 后恢复对话式沟通

# 为什么要使用“对话式”沟通
- **如果不使用**：
  - AI 错误可能导致错误累积，用户无法中途纠正
  - 用户新想法无法及时传达，浪费 token 和资源
- **如果使用**：
  - 实现及时纠错和方向调整
  - 提升用户参与感和控制权
- **额外提示**：鼓励 AI 主动提出疑问或建议（如“是否需要优化此步骤？”），以激发创造性响应

# “对话式”沟通的根本原则
- **多给用户确认机会**：在关键步骤暂停，等待用户输入（需提供明确选项）
- **避免闷头苦干**：若用户拒绝操作但未给新指令，必须停止并请求指导（例如：`echo "操作已取消，请提供新指令：[继续]/终止"`）
- **确保高效性**：确认消息需完整且包含选项，减少理解成本
- **默认选项设计**：中括号选项应为常规选择（如 `[继续]` 比 `[取消]` 更好，除非希望用户取消）
```

## 💡 情景示例

### 文件修改确认
```bash
echo "即将修改 src/components/Header.tsx，添加新的导航菜单，是否继续？[是]/否"
```

### 命令执行确认
```bash
echo "计划执行命令：npm install react-router-dom，是否继续？[是]/否"
```

### 任务完成确认
```bash
echo "路由配置已完成，所有测试通过。是否需要我继续优化代码结构？[是]/否"
```

### 高风险操作确认
```bash
echo "检测到将删除 node_modules 目录，这是高风险操作，是否确认执行？是/[否]"
```

## ⚡ 进阶技巧

### 动态调整对话模式
```bash
# 开启强化确认模式
use 对话

# 关闭对话模式（仅保留高风险确认）
dont use 对话
```

### 利用 Cursor 命令修改功能
在 Cursor 中，你可以修改 AI 即将执行的 echo 命令内容，实现实时指令传达：

![modify the echo command content](https://github.com/abigass/real-time_communicate_with_cursor/raw/main/modify_echo.gif)  

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来完善这套规则集。如果你有更好的实践经验或发现了新的应用场景，请随时分享。

## 📄 许可证

本项目采用 MIT 许可证，详见 [LICENSE](LICENSE) 文件。

---

**让 AI 开发更可控，让协作更高效！** 🚀 
