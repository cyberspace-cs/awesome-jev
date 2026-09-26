# 🏠 LLM2Jev - 本地版 Jev 决策引擎

> ⭐ 335 stars | 纯本地跑，不依赖云端 Jev

---

## 🎯 这是什么？

把 HuggingFace 因果模型改造成 **Jev 兼容的结构化决策引擎**，纯本地跑，不调云端、不依赖商用 Jev。

**解决的问题：**
- 没有 Jev API Key 也能用 Jev
- 私有数据不能上传云端
- 需要高并发、可复现的实验

---

## ✨ 核心能力

### 1. 三种决策类型
- **Choice**：出选项分布
- **Score**：出档位加权分
- **Noul**：出"为真"概率

### 2. Prefill-only 推理
- 不用自回归生成，只算候选 token 概率
- 输出稳定，便于批量处理
- 比"生成 JSON 再解析"快很多

### 3. 多模态支持
- 文本输入 ✅
- 图片等非文本输入 ✅（最新更新）

### 4. 多后端支持
- Transformers
- SGLang

---

## 💡 和云端 Jev 的对比

| 维度 | 云端 Jev | LLM2Jev 本地版 |
|------|---------|---------------|
| 数据隐私 | 要上传云端 | **纯本地，数据不出门** |
| 成本 | 按调用付费 | **一次部署，随便跑** |
| 延迟 | 网络往返 | **本地推理，更快** |
| 模型大小 | 黑盒，不知道多大 | **自己选模型，可控** |
| 多模态 | 官方支持 | **最新支持图片** |
| 适合场景 | 生产环境、快速验证 | **实验、私有数据、高并发** |

---

## 🚀 怎么用？

```python
# 伪代码示例
from llm2jev import LLM2Jev, Choice, Score, Noul

# 加载本地模型
engine = LLM2Jev(model="Qwen2.5-7B")

# 问一个 Choice 问题
result = engine.ask(
    state={"user_input": "帮我看看这个代码有没有 bug"},
    question=Choice(
        instructions="判断这个问题的类型",
        criteria={"bug": "代码 bug", "feature": "新功能", "question": "用户疑问"}
    )
)

print(result.choice)  # "bug"
print(result.probabilities)  # {"bug": 0.85, "feature": 0.1, "question": 0.05}
```

---

## 📦 相关链接

- **原仓库**：https://github.com/Yinsongxu/LLM2Jev
- **我们的 fork**：https://github.com/cyberspace-cs/llm2jev
- **作者**：Yinsongxu

---

## 🎯 我们可以怎么用？

### 1. 本地开发测试
开发 Jev 相关功能时，不用调云端 API，本地就能测，省钱又快。

### 2. 私有数据场景
公司内部的敏感数据，不能上传云端 Jev，用 LLM2Jev 本地跑。

### 3. 高并发场景
批量跑实验、做 benchmark，用本地模型成本更低。

### 4. 二次开发
可以改成自己的决策引擎，加自定义的 primitive。

---

## 💡 核心启示

**Jev 不只是云端 API，而是一种范式：**
- 送一段 state，问结构化问题
- 直接拿带概率的类型化答案
- 不用解析自然语言 JSON

这种范式可以用任何模型实现，不管是云端还是本地。
