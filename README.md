# 中转 API 降智检测:一键测你的 Claude/GPT 中转是不是「满血模型」

> **Is your AI API relay silently downgrading the model? A free, one-click check —
> your key is never stored.** 你付 Opus 的钱,拿的可能是 Haiku 的活。这份说明教你
> **怎么判断中转有没有偷偷降智**,并给你两个自己就能跑的免费工具。

**📅 更新:2026-07** · 作者做 [cocodot](https://cocodot.co)(一个不降智可验证的 AI 中转),
但下面的检测方法**对任何中转都通用**,包括不选 cocodot 的情况。**别信口头保证,自己测。**

---

## 什么是「降智」?

你用中转站调 Claude Opus / GPT,中转方为了省成本,可能:
- **偷换模型**:你请求 Opus,它后台给你返小模型(Haiku / 老版本),你察觉不到。
- **限流截断**:高峰期悄悄压缩上下文、截断输出。
- **缓存复用**:不同请求返回雷同结果。

结果:**你按满血价付费,拿的是缩水货。** 这在中文中转圈很常见,而且大多数人不会验。

---

## 怎么自己验(两个免费工具)

### 1. 网页版 · 30 秒出结果 —— [probe.cocodot.co](https://probe.cocodot.co)
填你**任意中转**的 `base_url` + `key` + 模型,一键跑 **6 道探针**:
**模型身份 / 能力(另一个模型当裁判打分)/ 延迟 / 上下文长度 / 限流 / 一致性**。
- ✅ **免费、免注册**
- ✅ **Key 不存、不记日志、用完即弃**
- ✅ 测的是你**正在用的那家**,不是我家——谁降智一测露馅

### 2. 命令行版 · 可审计 —— [LLMprobe](https://github.com/cocodot2026/LLMprobe)(开源)
同一套探针的开源 CLI,适合想看源码、想批量测、想接 CI 的人:

```bash
pip install openai
python llmprobe.py --base-url https://<你的中转>/api/ai/v1 --api-key <你的KEY> --model <模型>
```

Key 只在本机用,代码开源可审计。

---

## 挑中转的 6 条硬标准

测完之后,拿这 6 条挑(**不管选不选 cocodot**):

1. **降智可验证** —— 能用上面工具测出真模型,而不是只会嘴上保证。
2. **费率透明** —— 倍率/按量怎么算,有没有藏加价。
3. **模型齐** —— Claude / GPT / Gemini / DeepSeek 一个 Key 能不能都调。
4. **支付宝/人民币** —— 没海外卡的关键。
5. **稳定不限速** —— 高峰会不会截断。
6. **标准兼容** —— 是不是标准 OpenAI/Anthropic 兼容端点(能无痛接 Claude Code / Cursor / Cline)。

> 作者用 LLMprobe 实测过 cocodot = **87/100**(真 Claude、零降智);但**重点是这个方法**,
> 你拿同一把尺子量任何一家就行。

---

*检测工具 [probe.cocodot.co](https://probe.cocodot.co)(网页)/ [LLMprobe](https://github.com/cocodot2026/LLMprobe)(开源 CLI)均免费。作者与 cocodot 利益相关,已声明。欢迎 Issue 纠错。*
