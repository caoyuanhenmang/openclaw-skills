---
name: feishu-at-mention
description: "飞书@人正确姿势指南。解决飞书消息中@人不生效、格式错误等问题。提供正确的<at user_id=\"ou_xxx\"></at>格式，以及如何获取用户open_id的方法。适合需要在飞书群里@人的Agent使用。"
---

# 飞书@人助手

## 问题背景

很多 Agent 在飞书群里尝试@人时，会遇到以下问题：
- 用 `@用户名` 格式 → 不生效，只显示纯文本
- 用 `@ou_xxx` 格式 → 不生效
- 用 `<@ou_xxx>` 格式 → 不生效

## ✅ 正确格式

```xml
<at user_id="ou_xxxxxxxxxxxx"></at>
```

### 完整示例

```xml
<at user_id="ou_b9ea1576e68af3c8f1327c81b4fe08c0"></at> 你好呀！
```

## 📋 使用步骤

### 步骤1: 获取用户的 open_id

在群里@人之前，需要先获取目标用户的 open_id（格式：`ou_xxx`）。

**方法一：通过群成员列表**

使用 `feishu_chat_members` 工具获取群成员列表：

```json
{
  "chat_id": "oc_xxx",
  "member_id_type": "open_id"
}
```

返回结果中包含每个成员的 `open_id`。

**方法二：通过用户搜索**

使用 `feishu_search_user` 工具搜索用户：

```json
{
  "query": "用户姓名"
}
```

### 步骤2: 在消息中使用@格式

获取到 open_id 后，在消息中使用正确格式：

```xml
<at user_id="ou_xxx"></at> 你的消息内容
```

## ⚠️ 注意事项

1. **必须用 `<at user_id="ou_xxx"></at>` 格式**
   - 注意是 `user_id` 属性
   - 值要用引号包裹
   - 标签要闭合 `</at>`

2. **只能在同一个群里@人**
   - 无法跨群@人
   - 私聊中@人没有意义（已经是1v1对话）

3. **open_id 格式**
   - 用户：`ou_xxx`
   - 群：`oc_xxx`
   - 不要混淆

4. **常见错误格式**（不要用！）
   - ❌ `@用户名`
   - ❌ `@ou_xxx`
   - ❌ `<@ou_xxx>`
   - ❌ `@{ou_xxx}`
   - ❌ `<at id="ou_xxx"></at>`（应该是 `user_id` 不是 `id`）

## 🎯 最佳实践

### 示例1：在回复中@某人

```
<at user_id="ou_xxx"></at> 收到！我马上处理~
```

### 示例2：@多人

```
<at user_id="ou_aaa"></at> <at user_id="ou_bbb"></at> 两位看下这个~
```

### 示例3：结合消息内容

```
<at user_id="ou_xxx"></at> 你好！这是你要的早报：

📰 今日科技早报...
```

## 🔧 技术细节

飞书消息使用富文本格式，`<at>` 是飞书定义的特殊标签，用于实现@提醒功能。

- `user_id` 属性：指定被@用户的 open_id
- 标签内容：可以为空，也可以填写用户名（但通常留空）
- 发送后：被@用户会收到特殊提醒通知

## 📚 相关文档

- 飞书开放平台：https://open.feishu.cn
- 消息体格式：富文本消息支持 `<at>` 标签

---

记住这个格式就够啦：`<at user_id="ou_xxx"></at>` 🦞
