# 深圳大厂 Agent / 大模型应用开发面试复习手册

> 适用方向：AI Agent 开发、大模型应用开发、RAG 应用开发、AI Coding 后端、大模型平台、大模型网关、LLM Infra 入门岗。  
> 重点目标：先拿下「大模型应用 / Agent 工程化」岗位，再根据背景补算法、训练、推理系统方向。

---

## 0. 复习使用方法

建议把这份文档分成三轮复习：

| 轮次 | 目标 | 做法 |
|---|---|---|
| 第一轮 | 建立知识框架 | 快速通读，标记不会的名词和题目 |
| 第二轮 | 准备面试表达 | 每个高频题都用自己的话讲 1 分钟 |
| 第三轮 | 项目和机试冲刺 | 围绕简历项目、系统设计、算法题反复模拟 |

**优先级原则：**

1. 后端基础和算法机试不能丢。
2. RAG、Agent、工具调用、评测、可观测性是大模型应用岗核心。
3. Transformer、LoRA、DPO、KV Cache、vLLM 是高频加分项。
4. CUDA、Megatron、DeepSpeed、分布式训练是系统 / 训练岗重点，不是所有应用岗都深挖。

---

## 1. 岗位类型和准备重点

### 1.1 三类相关岗位

| 岗位方向 | 更适合的人 | 主要考察点 | 准备优先级 |
|---|---|---|---|
| AI Agent / 大模型应用开发 | 后端、全栈、Python/Java/Go 开发 | RAG、Agent、工具调用、Workflow、工程落地、稳定性、成本、评测 | 最高 |
| 大模型算法 / 后训练 | 算法、NLP、机器学习背景 | Transformer、SFT、DPO、RLHF、数据、训练、评测、论文理解 | 中高 |
| 大模型系统 / 推理加速 / 训练框架 | C++、CUDA、分布式系统背景 | vLLM、SGLang、KV Cache、并行策略、显存优化、CUDA、分布式训练 | 按背景选择 |

### 1.2 当前最现实的切入口

如果你是后端或应用开发背景，建议主攻：

```text
大模型应用开发
AI Agent 开发
RAG 平台开发
AI Coding 后端
大模型平台工程师
大模型网关
LLM 应用工程师
```

核心面试判断标准不是“会不会调 API”，而是：

> 你能不能把 Agent / RAG 做成稳定、可评测、可观测、可控成本、可接业务系统的工程系统。

---

## 2. 总体复习路线

```text
计算机基础
  ├─ 编程语言
  ├─ 操作系统
  ├─ 网络
  ├─ 数据库
  ├─ Redis / MQ
  └─ 系统设计

大模型基础
  ├─ Transformer
  ├─ Tokenizer
  ├─ SFT / RLHF / DPO / LoRA
  ├─ 推理优化
  └─ 模型评测

RAG 专项
  ├─ 文档解析
  ├─ chunk 切分
  ├─ embedding
  ├─ 向量库
  ├─ hybrid search
  ├─ rerank
  ├─ 引用溯源
  └─ RAG eval

Agent 专项
  ├─ ReAct
  ├─ Tool Calling
  ├─ Planner
  ├─ Memory
  ├─ Workflow
  ├─ MCP
  ├─ Guardrails
  ├─ Trace
  └─ Agent Eval

面试输出
  ├─ 项目包装
  ├─ 系统设计
  ├─ 机试题
  └─ 行为面试
```

---

# 第一部分：计算机基础八股

---

## 3. 编程语言基础

至少要熟练一门主力语言：Python、Go、Java、C++。  
大模型应用岗最常见组合是：**Python + Go / Java + SQL + Linux**。

### 3.1 Python 高频题

需要掌握：

- GIL 是什么？为什么 Python 多线程不适合 CPU 密集任务？
- 多线程、多进程、协程分别适合什么场景？
- `asyncio`、事件循环、`await`、`async` 的原理。
- 生成器和迭代器区别。
- 装饰器怎么实现？常用于哪些场景？
- 上下文管理器 `with` 的原理。
- `list`、`dict`、`set` 的底层结构和复杂度。
- 深拷贝和浅拷贝区别。
- Python 内存管理和引用计数。
- FastAPI / Flask 如何处理并发请求。

### 3.2 Go 高频题

需要掌握：

- goroutine 和线程的区别。
- channel 的使用场景。
- `context` 如何做超时、取消、链路传递。
- GMP 调度模型。
- `defer` 执行顺序。
- `panic` / `recover` 使用场景。
- map 是否线程安全？如何保证并发安全？
- interface 底层是什么？
- Go GC 基本原理。

### 3.3 Java 高频题

需要掌握：

- JVM 内存区域。
- GC 算法和常见垃圾收集器。
- HashMap、ConcurrentHashMap 原理。
- synchronized 和 ReentrantLock 区别。
- volatile 的作用。
- 线程池参数和拒绝策略。
- Spring Boot 请求链路。
- MyBatis / JPA 常见问题。

### 3.4 C++ 高频题

需要掌握：

- 智能指针：`unique_ptr`、`shared_ptr`、`weak_ptr`。
- RAII 思想。
- 虚函数和多态。
- 构造函数、析构函数、拷贝构造、移动构造。
- 左值、右值、移动语义。
- 内存泄漏和野指针。
- STL 常见容器底层。

---

## 4. 操作系统八股

### 4.1 高频问题清单

- 进程和线程区别？
- 协程和线程区别？
- 进程间通信有哪些方式？
- 死锁产生的四个条件是什么？如何避免？
- 用户态和内核态区别？为什么切换慢？
- select、poll、epoll 区别？
- epoll 为什么适合高并发？
- mmap 是什么？有什么应用？
- Page Cache 是什么？
- 零拷贝是什么？常见场景有哪些？
- 什么是上下文切换？
- Linux 如何排查 CPU 飙高？
- Linux 如何排查内存泄漏？
- Linux 如何排查磁盘 IO 高？
- Linux 如何排查网络连接问题？

### 4.2 面试表达模板：CPU 飙高怎么排查

```text
1. top / htop 查看哪个进程 CPU 高。
2. ps -T -p <pid> 查看线程级 CPU。
3. 将线程 id 转成十六进制。
4. Java 用 jstack，Python 用 py-spy / faulthandler，Go 用 pprof。
5. 判断是死循环、锁竞争、GC、系统调用、IO 等问题。
6. 结合日志、监控、火焰图定位代码。
```

---

## 5. 计算机网络八股

### 5.1 高频问题清单

- TCP 三次握手流程。
- TCP 四次挥手流程。
- 为什么 TIME_WAIT 需要等待？
- TCP 和 UDP 区别。
- TCP 如何保证可靠传输？
- 拥塞控制和流量控制区别。
- TCP 粘包是什么？如何解决？
- HTTP/1.1、HTTP/2、HTTP/3 区别。
- HTTPS 握手流程。
- TLS 证书校验过程。
- REST、RPC、gRPC 区别。
- WebSocket、SSE、长轮询区别。
- 大模型流式输出为什么常用 SSE？
- DNS 解析过程。
- CDN 基本原理。

### 5.2 SSE 和 WebSocket 对比

| 对比点 | SSE | WebSocket |
|---|---|---|
| 通信方向 | 服务端到客户端单向推送 | 双向通信 |
| 协议基础 | HTTP | 独立协议，基于 HTTP 握手升级 |
| 适用场景 | 大模型流式输出、消息通知 | 即时聊天、多人协作、实时互动 |
| 实现复杂度 | 低 | 中高 |
| 自动重连 | 浏览器原生支持 | 需要自己实现 |

大模型回答流式输出一般是服务端持续推 token，客户端只需要接收，所以 SSE 很常见。

---

## 6. 数据库、缓存、消息队列

### 6.1 MySQL 高频题

- MySQL 索引为什么常用 B+ 树？
- 聚簇索引和非聚簇索引区别。
- 覆盖索引是什么？
- 最左前缀原则是什么？
- 索引失效有哪些情况？
- explain 怎么看？
- 事务 ACID 是什么？
- 事务隔离级别有哪些？
- MVCC 是什么？
- 当前读和快照读区别。
- 间隙锁、临键锁是什么？
- 慢 SQL 如何排查？
- 分库分表怎么设计？

### 6.2 Redis 高频题

- Redis 常见数据结构。
- String、Hash、List、Set、ZSet 使用场景。
- Redis 为什么快？
- Redis 持久化 RDB 和 AOF 区别。
- 缓存穿透、击穿、雪崩是什么？
- 分布式锁怎么实现？
- RedLock 有什么争议？
- Redis 过期策略。
- Redis 淘汰策略。
- Redis Cluster 如何分片？
- 热 Key 怎么处理？
- 大 Key 怎么处理？

### 6.3 MQ 高频题

- Kafka、RabbitMQ、RocketMQ 区别。
- 如何保证消息不丢？
- 如何处理消息重复消费？
- 如何保证消息顺序？
- 消费积压怎么办？
- 延迟队列怎么实现？
- 死信队列是什么？
- Exactly Once 能否真正做到？

### 6.4 和大模型应用的结合点

| 技术 | 在大模型应用中的用途 |
|---|---|
| MySQL / PostgreSQL | 用户、权限、配置、Prompt 版本、任务记录 |
| Redis | 缓存、限流、分布式锁、短期上下文、热点问题缓存 |
| Kafka / RabbitMQ | 文档解析异步任务、embedding 入库、评测任务、日志事件 |
| Elasticsearch | BM25 全文检索、日志检索、hybrid search |
| 对象存储 | PDF、图片、原始文档、评测数据集 |

---

## 7. 系统设计基础

Agent / RAG 岗很容易出系统设计题。

### 7.1 高频系统设计题

- 设计一个企业知识库问答系统。
- 设计一个客服 Agent 系统。
- 设计一个 AI 编程助手。
- 设计一个数据分析 Agent。
- 设计一个大模型网关。
- 设计一个 Prompt 管理和灰度发布平台。
- 设计一个多租户 RAG 平台。
- 设计一个模型评测平台。
- 设计一个 AI 工作流平台。

### 7.2 系统设计回答框架

```text
1. 明确需求
   - 用户是谁？
   - 核心功能是什么？
   - QPS / 延迟 / 数据规模 / 权限要求？

2. 画整体架构
   - 前端 / API Gateway / 服务层 / 存储 / 模型服务 / 观测系统

3. 讲核心链路
   - 请求进入后如何处理？
   - 调用哪些组件？
   - 如何返回结果？

4. 讲难点
   - 准确率、延迟、成本、权限、安全、稳定性

5. 讲优化
   - 缓存、限流、异步化、降级、灰度、评测、监控

6. 讲权衡
   - 为什么这样设计？不用另一种方案的原因？
```

---

# 第二部分：大模型基础八股

---

## 8. Transformer 高频知识

### 8.1 必须掌握的问题

- Transformer 为什么适合大模型？
- Self-Attention 公式是什么？
- Q、K、V 分别是什么？
- Attention 的时间复杂度是多少？
- Multi-Head Attention 的作用是什么？
- Position Encoding 是什么？
- RoPE 是什么？解决什么问题？
- LayerNorm 和 RMSNorm 区别。
- FFN、SwiGLU 是什么？
- Encoder-only、Decoder-only、Encoder-Decoder 区别。
- GPT 类模型为什么是 Decoder-only？
- Tokenizer 是什么？
- BPE / SentencePiece 原理。
- 上下文窗口为什么有限？
- 为什么长上下文不等于长期记忆？

### 8.2 Self-Attention 简明解释

Attention 的核心是：

```text
每个 token 根据自己和其他 token 的相关性，动态聚合上下文信息。
```

公式：

```text
Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V
```

解释：

- Q：Query，当前 token 想找什么信息。
- K：Key，其他 token 提供什么索引。
- V：Value，其他 token 实际携带的信息。
- `QK^T`：计算 token 之间相关性。
- `sqrt(d_k)`：缩放，避免数值过大导致 softmax 饱和。
- softmax：转成权重。
- 乘以 V：按权重聚合信息。

### 8.3 MHA / MQA / GQA

| 概念 | 含义 | 作用 |
|---|---|---|
| MHA | Multi-Head Attention，多头注意力 | 多个头学习不同关系 |
| MQA | Multi-Query Attention，多个 Q 共享 K/V | 降低 KV Cache 显存，提高推理效率 |
| GQA | Grouped-Query Attention，多个 Q 分组共享 K/V | 在效果和效率之间折中 |

### 8.4 RoPE 简明解释

RoPE 是旋转位置编码。核心思想是：

```text
把位置信息以旋转矩阵的形式注入 Q 和 K，使模型能感知 token 的相对位置关系。
```

面试时可这样说：

> RoPE 不像绝对位置编码那样直接加一个位置向量，而是在注意力计算前对 Q、K 做和位置相关的旋转变换，使点积结果天然包含相对位置信息，因此更适合自回归模型和一定程度的长度外推。

---

## 9. 训练与后训练

### 9.1 高频概念

| 概念 | 作用 | 面试重点 |
|---|---|---|
| Pretraining | 用海量语料训练基础语言能力 | 预测下一个 token，自监督学习 |
| SFT | 指令微调 | 让模型学会按人类指令回答 |
| RLHF | 人类反馈强化学习 | 用偏好数据训练 reward model，再用 PPO 优化 |
| DPO | Direct Preference Optimization | 不显式训练 reward model，直接用偏好数据优化模型 |
| GRPO | Group Relative Policy Optimization | 常用于推理、数学等场景的强化学习优化思路 |
| LoRA | 低秩适配微调 | 冻结基座模型，只训练小矩阵 |
| QLoRA | 量化后做 LoRA | 降低显存占用 |

### 9.2 SFT 是什么

SFT，全称 Supervised Fine-Tuning，监督微调。  
它使用人工构造或清洗后的「指令 - 回答」数据，让基础模型学会按照用户指令输出。

面试回答：

```text
SFT 主要解决模型“会语言但不一定会听指令”的问题。
预训练模型学到的是通用语言建模能力，SFT 通过高质量指令数据，让模型学习问答格式、任务遵循、安全边界和领域表达风格。
```

### 9.3 RLHF 是什么

RLHF，全称 Reinforcement Learning from Human Feedback。基本流程：

```text
1. 收集同一个问题下多个模型回答。
2. 人类标注偏好排序。
3. 训练 Reward Model。
4. 用 PPO 等强化学习方法优化模型，使模型输出更符合人类偏好。
```

### 9.4 DPO 是什么

DPO，全称 Direct Preference Optimization。  
它用偏好数据直接优化模型，不需要单独训练 Reward Model，也不需要复杂的 PPO 训练流程。

面试回答：

```text
DPO 的优势是训练流程更简单、更稳定，工程复杂度低于传统 RLHF/PPO。
它直接利用 chosen / rejected 偏好样本，让模型提高优选回答概率，降低劣选回答概率。
```

### 9.5 LoRA 是什么

LoRA 的核心思想：

```text
冻结大模型原有参数，只在部分线性层旁边增加低秩矩阵 A 和 B，训练这部分小参数。
```

优点：

- 显存占用低。
- 训练成本低。
- 可为不同任务保存不同 adapter。
- 适合领域适配和轻量微调。

常见追问：

- rank 怎么选？
- alpha 是什么？
- target_modules 选哪些层？
- LoRA 和全量微调区别？
- LoRA 会不会影响模型通用能力？
- 多个 LoRA adapter 能否合并？

---

## 10. 推理优化八股

### 10.1 必须掌握的概念

- Prefill 和 Decode 阶段区别。
- TTFT：Time To First Token。
- TPOT：Time Per Output Token。
- KV Cache 是什么？
- PagedAttention 是什么？
- Continuous Batching 是什么？
- Prefix Caching 是什么？
- Speculative Decoding 是什么？
- INT8、INT4、AWQ、GPTQ、FP8 量化区别。
- 为什么 batch 越大吞吐越高但延迟可能变差？
- 如何做大模型服务限流、排队、超时、降级？

### 10.2 Prefill 和 Decode

| 阶段 | 含义 | 特点 |
|---|---|---|
| Prefill | 处理输入 prompt，生成第一步 KV Cache | 计算量大，可并行度高，影响 TTFT |
| Decode | 自回归逐 token 生成输出 | 每步生成一个 token，受内存带宽和 KV Cache 影响大 |

### 10.3 KV Cache

自回归生成时，每生成一个新 token，都要关注之前所有 token。  
如果每一步都重新计算历史 token 的 K/V，会非常浪费。KV Cache 会缓存历史 token 的 Key 和 Value，后续 decode 阶段直接复用。

优点：

- 显著减少重复计算。
- 提高生成速度。

代价：

- 占用显存。
- 上下文越长、batch 越大，KV Cache 越大。

### 10.4 vLLM 为什么快

可从这些点回答：

```text
1. PagedAttention：像操作系统分页一样管理 KV Cache，减少显存碎片。
2. Continuous Batching：动态把不同请求合并，提高 GPU 利用率。
3. Prefix Caching：相同前缀复用 KV Cache，降低重复 prefill 成本。
4. 支持多种量化和并行策略，提高吞吐。
```

### 10.5 推理服务优化思路

```text
延迟优化：
- 减少 prompt 长度。
- 使用流式输出。
- 使用 prefix caching。
- 小模型优先处理简单请求。
- 做模型路由和降级。

吞吐优化：
- continuous batching。
- 合理 batch size。
- 量化。
- 多实例部署。
- KV Cache 管理。

成本优化：
- prompt 压缩。
- 缓存高频问题。
- 混合使用大模型和小模型。
- 异步任务队列。
- 限流和配额。
```

---

# 第三部分：RAG 专项

---

## 11. RAG 全流程

RAG，全称 Retrieval-Augmented Generation，检索增强生成。  
核心思路是：先从外部知识库检索相关内容，再把检索结果提供给大模型生成答案。

### 11.1 标准流程

```text
文档上传
  ↓
文档解析：PDF / Word / HTML / Markdown / 图片 OCR
  ↓
文档清洗：去噪、去页眉页脚、去重复
  ↓
Chunk 切分：按标题、段落、语义、长度
  ↓
Embedding 向量化
  ↓
入库：向量库 + 元数据 + 原文
  ↓
用户提问
  ↓
Query Rewrite / Query Expansion
  ↓
检索：向量检索 + BM25 + metadata filter
  ↓
Rerank 重排
  ↓
Prompt 组装
  ↓
LLM 生成答案
  ↓
引用溯源
  ↓
评测与反馈
```

### 11.2 RAG 必会组件

| 组件 | 作用 | 常见技术 |
|---|---|---|
| 文档解析 | 把原始文件转成文本和结构 | Unstructured、PyMuPDF、docx、OCR |
| Chunking | 把文档切成可检索片段 | 长度切分、标题切分、语义切分 |
| Embedding | 文本转向量 | BGE、E5、OpenAI embedding、Qwen embedding |
| 向量库 | 存储和检索向量 | Milvus、Qdrant、FAISS、pgvector |
| 全文检索 | 关键词匹配 | Elasticsearch、BM25 |
| Hybrid Search | 语义 + 关键词召回 | 向量检索 + BM25 融合 |
| Rerank | 对候选文档重新排序 | bge-reranker、cross-encoder |
| Prompt Assembly | 组织上下文 | 模板、引用、压缩 |
| Evaluation | 评估效果 | Faithfulness、Context Recall、Answer Relevancy |

---

## 12. RAG 高频面试题

### 12.1 基础题

- RAG 是什么？
- RAG 和微调怎么取舍？
- Embedding 模型怎么选？
- Chunk size 过大或过小有什么问题？
- overlap 为什么有用？
- Top-k 选多少合适？
- 向量相似度 cosine、dot product、L2 区别。
- BM25 和向量检索区别。
- 为什么要 hybrid search？
- Rerank 的作用是什么？

### 12.2 进阶题

- RAG 召回不到答案怎么办？
- 召回到了答案但模型不采用怎么办？
- 如何降低幻觉？
- 如何做引用溯源？
- 如何支持多轮问答？
- 如何做权限隔离？
- 如何处理表格、合同、财报、图片？
- 如何处理超长文档？
- 如何做增量更新？
- 如何做多租户知识库？
- 如何评估 RAG 效果？

---

## 13. RAG 题目回答模板

### 13.1 RAG 和微调怎么取舍

```text
RAG 适合知识频繁变化、需要引用来源、需要接企业私有数据的场景。
微调适合让模型学习特定风格、格式、领域表达或稳定任务模式。

如果问题是“模型不知道最新知识”，优先 RAG。
如果问题是“模型知道但不会按要求回答”，可以考虑 SFT / LoRA。
生产里经常是 RAG + 少量微调结合。
```

### 13.2 Chunk size 怎么设置

```text
Chunk size 没有固定答案，要结合文档结构、embedding 模型、下游任务和上下文窗口。

过小：语义不完整，召回片段缺上下文。
过大：噪声多，向量语义被稀释，召回不精准，还会浪费上下文。

一般会先按标题 / 段落 / Markdown 结构切分，再控制 token 长度，并保留一定 overlap。
最终通过评测集调参，看 context recall、answer faithfulness 和延迟成本。
```

### 13.3 为什么需要 hybrid search

```text
向量检索擅长语义相似，但对专有名词、编号、错误码、合同条款、精确关键词不一定稳定。
BM25 擅长关键词精确匹配，但不理解语义改写。

Hybrid search 把两者结合，可以提高召回覆盖率，尤其适合企业知识库、代码文档、法律合同、客服 FAQ。
```

### 13.4 Rerank 为什么有效

```text
第一阶段检索追求召回率，会返回较多候选文档。
Rerank 用更强的交叉编码器或大模型对 query 和候选文档做精排，判断真正相关性。

它牺牲一点延迟，换取更高的 top-k 准确率，减少无关上下文进入 prompt，从而降低幻觉。
```

### 13.5 RAG 幻觉怎么解决

```text
我会从召回、生成、约束、评测四层处理：

1. 召回层：改进 chunk、hybrid search、rerank、query rewrite，提高相关上下文质量。
2. 生成层：prompt 明确要求只能基于引用资料回答，资料不足就说不知道。
3. 约束层：答案必须带引用，关键字段做规则校验或二次验证。
4. 评测层：建立问题集，统计 faithfulness、context recall、引用正确率，并分析失败 case。
```

---

## 14. RAG 项目会被深挖的问题

如果简历写了 RAG 项目，必须提前准备：

- 数据规模多大？多少文档？多少 chunk？
- 文档格式有哪些？PDF 表格怎么处理？
- 文档解析失败怎么办？
- chunk 怎么切？为什么这样切？
- embedding 模型怎么选？有没有评估？
- 用什么向量库？为什么不用别的？
- 向量索引用什么？HNSW、IVF、Flat 有什么区别？
- top-k 设置多少？为什么？
- 有没有 hybrid search？融合分数怎么做？
- 有没有 rerank？rerank 后提升多少？
- 多轮问答怎么处理历史上下文？
- 权限控制怎么做？不同用户能看到不同文档吗？
- 更新文档后怎么增量入库？
- 删除文档后如何清理 chunk？
- 如何避免回答没有依据？
- 如何做引用溯源？
- 如何评估系统效果？
- 延迟和成本是多少？
- 失败 case 有哪些？你怎么改的？

---

# 第四部分：Agent 专项

---

## 15. Agent 核心概念

### 15.1 Agent 和 Chatbot 的区别

| 对比点 | 普通 Chatbot | Agent |
|---|---|---|
| 能力 | 回答问题 | 规划任务、调用工具、执行动作 |
| 状态 | 通常只依赖上下文 | 可维护任务状态和记忆 |
| 外部系统 | 很少调用 | 可调用 API、数据库、代码、搜索、企业系统 |
| 决策 | 一问一答 | 多步推理和行动循环 |
| 风险 | 较低 | 需要权限、审计、失败回滚 |

面试表达：

```text
Chatbot 更像是对话生成系统，Agent 则是带有目标、状态、工具和行动能力的系统。
Agent 不只是回答，而是能把任务拆解成步骤，选择工具执行，并根据观察结果继续决策。
```

### 15.2 Agent 基本架构

```text
User Input
  ↓
Intent Router / Task Classifier
  ↓
Planner
  ↓
Tool Registry / MCP Tools
  ↓
Executor
  ↓
Observation
  ↓
Memory / State Store
  ↓
Evaluator / Guardrail
  ↓
Final Response
  ↓
Trace / Metrics / Feedback Loop
```

### 15.3 生产级 Agent 的关键思想

面试时建议强调：

```text
我不会让 Agent 在生产环境里完全自由行动。
我会优先使用可控 workflow，把高风险步骤做成确定性节点。
只有开放探索、复杂推理、工具选择这类场景才让 LLM 决策。
```

这个观点很重要，因为大厂更关心：

- 可控
- 可测
- 可回滚
- 可审计
- 可观测
- 成本可控
- 权限可控

---

## 16. Agent 必会概念

| 概念 | 简明解释 | 面试重点 |
|---|---|---|
| ReAct | Reason + Act，边推理边行动 | 如何把推理、工具调用、观察结果串起来 |
| Tool Calling | 模型选择工具并生成参数 | schema、参数校验、失败处理、权限 |
| Function Calling | 一种结构化工具调用形式 | JSON schema、类型约束、函数注册 |
| Planner | 任务规划器 | 任务拆解、步骤控制、重规划 |
| Executor | 执行器 | 调用工具、处理结果、重试、超时 |
| Memory | 记忆 | 短期上下文、长期记忆、用户偏好 |
| Workflow | 固定流程 | 可控、稳定、适合生产 |
| Multi-Agent | 多智能体协作 | 分工、通信、冲突、成本 |
| MCP | Model Context Protocol | 统一模型和外部工具 / 数据源连接方式 |
| Guardrails | 安全护栏 | 防越权、防注入、防危险操作 |
| Trace | 链路追踪 | 每一步 prompt、tool、observation、token、latency |
| Agent Eval | 智能体评测 | 任务成功率、步骤正确率、工具调用正确率 |

---

## 17. Agent 高频面试题

### 17.1 基础题

- Agent 的基本架构是什么？
- Agent 和 Chatbot 区别？
- ReAct 原理是什么？
- Tool Calling 怎么设计？
- Function Calling 是什么？
- MCP 解决什么问题？
- Planner 和 Executor 怎么分工？
- Workflow 和 Agent 怎么取舍？
- LangGraph 解决什么问题？

### 17.2 工程题

- 如何防止 Agent 无限循环？
- Tool 调用失败怎么办？
- Tool 参数错误怎么办？
- 如何做工具权限控制？
- 如何设计 tool schema？
- 如何处理超时和重试？
- 如何做人工确认？
- 如何防 prompt injection？
- 如何防止 Agent 执行危险操作？
- 如何接企业内部系统？
- 如何做 trace 和失败回放？
- 如何降低 Agent 成本？
- 如何降低 Agent 延迟？

### 17.3 进阶题

- Agent memory 怎么设计？
- 长期记忆应该放向量库还是关系库？
- 多 Agent 协作有哪些模式？
- Multi-Agent 什么时候有用，什么时候反而复杂？
- Agent 如何做任务评测？
- 如何评估工具调用正确率？
- 如何把 Agent Demo 做成生产系统？
- AI Coding Agent 的核心难点是什么？

---

## 18. Agent 题目回答模板

### 18.1 如何防止 Agent 无限循环

```text
我会从执行预算、状态检测、工具约束和兜底策略四层做控制：

1. 设置 max_steps，超过步数直接停止并返回当前进度。
2. 设置总超时和单工具超时。
3. 检测重复 action / observation，连续重复则停止。
4. 对工具调用做 schema 校验，避免无效参数反复调用。
5. 对高风险工具加入人工确认。
6. 失败后做 fallback，比如转人工、返回需要补充的信息、或降级成普通问答。
```

### 18.2 Tool schema 怎么设计

```text
好的 tool schema 要让模型“容易选对、容易填对、容易校验”。

我会包含：
- 工具名称：简洁明确。
- 工具描述：说明什么时候用、什么时候不要用。
- 参数 schema：类型、必填项、枚举值、范围。
- 返回 schema：统一格式，包含 success、data、error_code、message。
- 权限等级：只读、写操作、高风险操作。
- 超时和重试策略。
- 示例调用。
```

### 18.3 Tool 调用失败怎么办

```text
分类型处理：

1. 参数错误：让模型基于错误信息修正参数，但限制重试次数。
2. 工具超时：重试或降级，避免阻塞整个任务。
3. 权限错误：不重试，提示用户无权限。
4. 外部系统错误：记录 trace，返回友好提示或转人工。
5. 结果为空：让 Agent 判断是否换查询条件、补充问题或结束。
```

### 18.4 Workflow 和 Agent 怎么取舍

```text
确定性强、风险高、流程稳定的业务，我会优先用 workflow。
例如审批、下单、退款、权限变更。

开放性强、需要规划和工具选择的任务，可以用 Agent。
例如数据分析、代码修复、复杂查询、多步骤调研。

生产中通常是 workflow 包 Agent：关键节点确定，局部步骤由 Agent 决策。
```

### 18.5 Agent 如何做评测

```text
Agent 评测不能只看最终回答，还要看过程。

我会评估：
1. 任务成功率。
2. 工具选择准确率。
3. 参数填写准确率。
4. 步骤数量是否合理。
5. 是否越权或触发危险操作。
6. 最终答案是否正确。
7. 延迟、token 成本、失败率。
8. 失败 case 是否可复现和回放。
```

---

## 19. Agent 项目会被深挖的问题

如果简历写了 Agent 项目，必须准备：

- Agent 能调用哪些工具？
- 每个工具的 schema 怎么设计？
- 工具参数怎么校验？
- 工具调用失败怎么办？
- 有没有超时和重试？
- 如何防止无限循环？
- max_steps 设置多少？为什么？
- 有没有人工确认？
- 敏感操作如何拦截？
- 用户权限怎么控制？
- memory 怎么实现？
- 是否用了向量库保存长期记忆？
- trace 记录哪些字段？
- 如何回放一次失败任务？
- 怎么评估任务成功率？
- 多 Agent 有没有必要？
- 为什么不用普通 workflow？
- 线上出错怎么定位？
- 成本过高怎么优化？
- 延迟过高怎么优化？

---

# 第五部分：框架和工具

---

## 20. Agent / Workflow 框架

| 工具 | 需要掌握程度 | 重点 |
|---|---|---|
| LangChain | 了解到熟悉 | tools、agent、prompt、memory、retriever |
| LangGraph | 推荐重点学 | 状态机、可恢复、可控 workflow、生产级 Agent |
| LlamaIndex | 推荐重点学 | RAG、文档索引、检索、agentic workflow |
| OpenAI Agents SDK 思路 | 了解 | agent loop、tool、tracing、guardrail |
| MCP | 高频概念 | 统一模型与外部工具 / 数据源的连接方式 |
| Dify / Coze / FastGPT | 了解 | 低代码 RAG 和 workflow 平台 |
| CrewAI / AutoGen | 了解 | Multi-Agent 协作模式 |

### 20.1 LangGraph 为什么适合生产 Agent

可以这样回答：

```text
LangGraph 把 Agent 流程建模成有状态图，不是简单线性 chain。
它适合长流程、多分支、可恢复、可观察的 Agent。
相比普通 LangChain chain，LangGraph 更容易控制步骤、保存状态、处理失败和回放。
```

---

## 21. RAG / 向量库工具

| 类别 | 工具 |
|---|---|
| 向量库 | Milvus、Qdrant、FAISS、pgvector、Redis Vector |
| 全文检索 | Elasticsearch、OpenSearch、BM25 |
| 文档解析 | PyMuPDF、Unstructured、docx、OCR 工具 |
| Embedding | BGE、E5、Qwen Embedding、OpenAI Embedding |
| Reranker | bge-reranker、cross-encoder、LLM rerank |
| 评测 | Ragas、DeepEval、自定义评测集 |

---

## 22. 模型服务 / 推理工具

| 工具 | 作用 |
|---|---|
| vLLM | 高吞吐 LLM 推理服务 |
| SGLang | LLM serving 和复杂推理流程优化 |
| TensorRT-LLM | NVIDIA 推理优化 |
| Ollama | 本地模型运行，适合开发测试 |
| llama.cpp | CPU / 边缘端 / 量化模型运行 |
| TGI | Hugging Face Text Generation Inference |
| Triton Inference Server | 通用推理服务 |
| Ray Serve | 分布式模型服务 |
| KServe | Kubernetes 上的模型服务 |

---

## 23. 评测和可观测性

| 方向 | 工具 / 指标 |
|---|---|
| RAG 评测 | Faithfulness、Answer Relevancy、Context Precision、Context Recall |
| Agent 评测 | Task Success Rate、Tool Accuracy、Step Accuracy、Safety Violation Rate |
| Trace | LangSmith、OpenTelemetry、自研 trace |
| 监控 | Prometheus、Grafana |
| 日志 | ELK、Loki |
| 成本 | token 数、模型单价、缓存命中率 |
| 延迟 | TTFT、TPOT、总耗时、工具耗时 |

---

# 第六部分：机试和笔试准备

---

## 24. 算法题优先级

### 24.1 数组 / 哈希

- 两数之和
- 三数之和
- 最长连续序列
- 和为 K 的子数组
- 合并区间
- 缺失的第一个正数

### 24.2 双指针 / 滑动窗口

- 最长无重复子串
- 最小覆盖子串
- 盛最多水的容器
- 接雨水
- 移动零
- 找到字符串中所有字母异位词

### 24.3 链表

- 反转链表
- 合并两个有序链表
- 合并 K 个升序链表
- 环形链表
- 两两交换链表节点
- LRU Cache

### 24.4 栈 / 队列 / 堆

- 有效括号
- 最小栈
- 单调栈
- 滑动窗口最大值
- Top K 高频元素
- 数据流中位数

### 24.5 二叉树

- 前中后序遍历
- 层序遍历
- 最近公共祖先
- 二叉树最大路径和
- 二叉树直径
- 序列化和反序列化二叉树

### 24.6 图

- 岛屿数量
- 课程表
- 拓扑排序
- 最短路径
- 并查集
- 克隆图

### 24.7 动态规划

- 爬楼梯
- 打家劫舍
- 最长递增子序列
- 最长公共子序列
- 编辑距离
- 01 背包
- 股票买卖

### 24.8 字符串 / Trie

- KMP 思想
- 前缀树
- 单词搜索
- 敏感词匹配
- 字符串解码

---

## 25. 大模型应用岗可能出现的工程机试

### 25.1 实现 LRUCache + TTL

考点：

- 哈希表
- 双向链表
- 过期时间
- 并发安全扩展

需要讲清楚：

```text
get：如果 key 不存在或过期，返回空；否则移动到链表头。
put：如果存在则更新并移动到头；如果超容量则淘汰尾部。
TTL：get / put 时懒删除过期 key，也可加后台定时清理。
```

### 25.2 实现限流器

常见算法：

| 算法 | 特点 |
|---|---|
| 固定窗口 | 简单，但边界突刺明显 |
| 滑动窗口 | 更平滑，成本略高 |
| 令牌桶 | 支持突发流量，常用于 API 限流 |
| 漏桶 | 匀速处理，适合削峰 |

大模型网关常考：

```text
按用户 / 租户 / API Key / 模型维度限流。
超过限制后返回 429，或进入队列，或降级到小模型。
```

### 25.3 实现 SSE 流式输出接口

考点：

- HTTP 流式响应
- 生成器 / 异步迭代器
- 客户端断开处理
- 异常处理
- token 分片返回

### 25.4 实现简化版 RAG 检索器

输入：文档列表 + query。  
要求：

```text
1. 文档切 chunk。
2. 对 query 和 chunk 计算简单相似度。
3. 返回 top-k。
4. 可扩展 BM25 / embedding / rerank。
```

### 25.5 实现 Tool Calling Loop

要求：

```text
最多执行 5 步。
每一步模型返回 tool_name + arguments。
校验 tool 是否存在。
校验参数。
执行 tool。
记录 observation。
失败重试。
最终输出 answer。
```

核心伪代码：

```python
for step in range(max_steps):
    action = llm.plan(messages, tools)

    if action.type == "final":
        return action.answer

    if action.tool_name not in tool_registry:
        messages.append("工具不存在，请重新选择")
        continue

    try:
        args = validate(action.arguments, tool_schema[action.tool_name])
        result = execute_tool(action.tool_name, args, timeout=tool_timeout)
        messages.append({"role": "tool", "content": result})
    except Exception as e:
        messages.append({"role": "tool", "content": f"工具调用失败：{e}"})

return fallback_answer(messages)
```

### 25.6 实现 Prompt Template 渲染器

例子：

```text
你好 {{name}}，你的订单是 {{order_id}}
```

要求支持：

- 变量替换
- 缺失变量检查
- 默认值
- 转义
- 防止模板注入

### 25.7 实现任务调度器

场景：Agent 多个工具任务有依赖关系，给一个 DAG，要求按依赖执行。

考点：

- 拓扑排序
- 并发执行
- 失败处理
- 超时取消
- 结果合并

### 25.8 实现对话上下文裁剪函数

要求：

```text
输入历史消息和最大 token 限制。
保留 system prompt。
保留最近 N 轮对话。
保留重要 memory。
删除或摘要中间低价值内容。
```

---

# 第七部分：项目准备和简历包装

---

## 26. 推荐项目：企业知识库 + 工具调用 Agent + 评测平台

### 26.1 技术栈建议

```text
后端：Python FastAPI / Go / Java Spring Boot
向量库：Milvus / Qdrant / pgvector
全文检索：Elasticsearch / BM25
缓存：Redis
数据库：PostgreSQL / MySQL
队列：Celery / Kafka / RabbitMQ
模型服务：OpenAI API / Qwen / DeepSeek / vLLM
Agent：LangGraph / 自研状态机
评测：Ragas / DeepEval / 自定义测试集
部署：Docker Compose / Kubernetes
观测：Prometheus + Grafana + OpenTelemetry
```

### 26.2 功能清单

建议至少实现：

- [ ] 上传 PDF / Markdown / Word / HTML 文档。
- [ ] 文档解析、清洗、切分。
- [ ] embedding 向量化并入库。
- [ ] 支持向量检索。
- [ ] 支持 BM25 关键词检索。
- [ ] 支持 hybrid search。
- [ ] 支持 rerank。
- [ ] 回答时带引用来源。
- [ ] 支持多轮问答。
- [ ] 支持工具调用，例如查订单、查数据库、生成工单、查日志。
- [ ] Agent 有 max_steps、timeout、retry、fallback。
- [ ] 高风险工具需要人工确认。
- [ ] 每次调用记录 trace、token、延迟、成本。
- [ ] 准备 50 到 100 条评测问题。
- [ ] 输出准确率、召回率、幻觉 case、失败分析。

### 26.3 项目架构图

```text
                ┌─────────────────────┐
                │      Web / API       │
                └──────────┬──────────┘
                           │
                 ┌─────────▼─────────┐
                 │   Backend Service  │
                 │ FastAPI / Go / Java│
                 └───────┬─────┬─────┘
                         │     │
             ┌───────────▼┐   ┌▼─────────────┐
             │ RAG Service │   │ Agent Service│
             └─────┬───────┘   └──────┬──────┘
                   │                  │
      ┌────────────▼───────┐   ┌──────▼─────────┐
      │ Vector DB / ES     │   │ Tool Registry  │
      │ Milvus / Qdrant    │   │ MCP / APIs     │
      └────────────┬───────┘   └──────┬─────────┘
                   │                  │
      ┌────────────▼───────┐   ┌──────▼─────────┐
      │ Document Pipeline  │   │ Business System│
      │ Parse / Chunk / Emb│   │ DB / CRM / Logs│
      └────────────────────┘   └────────────────┘
                           │
                 ┌─────────▼──────────┐
                 │ LLM Gateway         │
                 │ Route / Limit / Log │
                 └─────────┬──────────┘
                           │
                 ┌─────────▼──────────┐
                 │ Model Service       │
                 │ API / vLLM / SGLang │
                 └────────────────────┘
```

### 26.4 项目亮点表达

面试时重点说：

```text
我不是只做了一个调用大模型 API 的 Demo。
我把 RAG、Agent、工具调用、评测、观测、权限控制、成本控制都做了闭环。
```

可以展开：

- 检索侧：hybrid search + rerank 提升召回质量。
- 生成侧：引用溯源 + 不知道机制降低幻觉。
- Agent 侧：tool schema 校验 + max_steps + retry + human-in-the-loop。
- 工程侧：异步文档处理 + 缓存 + 限流 + trace + 监控。
- 评测侧：构建评测集，分析失败 case，持续优化。

---

## 27. 简历写法

### 27.1 不建议这样写

```text
熟悉大模型，熟悉 Agent，熟悉 RAG。
```

问题：太空泛，无法证明你做过工程落地。

### 27.2 推荐写法：RAG 项目

```text
设计并实现企业知识库 RAG 系统，支持 PDF / Markdown / HTML 文档解析、语义切分、向量检索、BM25 混合召回和 rerank；构建 80 条业务评测集，针对召回失败、幻觉和引用错误进行 case 分析，并通过 chunk 策略、query rewrite 和 rerank 优化回答质量。
```

### 27.3 推荐写法：Agent 项目

```text
实现基于 LangGraph / 自研状态机的工具调用 Agent，支持 max_steps、tool schema 校验、超时重试、人工确认、trace 记录和失败回放，接入订单查询、SQL 查询、工单创建等内部工具，提升复杂任务自动化处理能力。
```

### 27.4 推荐写法：大模型网关

```text
搭建大模型网关，支持模型路由、流式输出、限流、重试、缓存、token 统计和调用审计；针对高频问题引入语义缓存和 prompt 压缩，降低重复调用成本并提升响应稳定性。
```

### 27.5 推荐写法：评测平台

```text
构建大模型应用评测流程，覆盖 RAG faithfulness、context recall、answer relevancy、Agent 工具调用准确率、任务成功率和安全违规率；支持评测集管理、批量运行、结果对比和失败样本回放。
```

---

# 第八部分：系统设计题准备

---

## 28. 设计一个大模型网关

### 28.1 需求

- 统一接入多个模型。
- 支持鉴权、限流、配额。
- 支持流式输出。
- 支持模型路由。
- 支持失败重试和降级。
- 支持 token、延迟、成本统计。
- 支持日志审计。

### 28.2 架构

```text
Client
  ↓
API Gateway
  ↓
Auth / Rate Limit / Quota
  ↓
Request Normalizer
  ↓
Model Router
  ↓
Cache / Prompt Compression
  ↓
Model Adapter
  ↓
LLM Providers / vLLM / SGLang
  ↓
Response Streamer
  ↓
Trace / Metrics / Billing / Audit
```

### 28.3 关键设计点

- 多租户隔离。
- 按模型、用户、租户维度限流。
- 简单问题路由到小模型，复杂问题路由到大模型。
- 支持超时、重试、熔断。
- 流式输出中断处理。
- token 成本统计。
- prompt 和 response 脱敏。
- 日志采样和审计。

---

## 29. 设计一个企业知识库问答系统

### 29.1 需求

- 企业文档上传和解析。
- 支持多格式文档。
- 支持权限隔离。
- 支持问答引用来源。
- 支持多轮对话。
- 支持质量评测和反馈。

### 29.2 核心链路

```text
文档链路：
Upload → Parse → Clean → Chunk → Embedding → Vector DB / ES → Index Update

问答链路：
Question → Query Rewrite → Hybrid Search → Rerank → Context Assembly → LLM → Citation → Feedback
```

### 29.3 难点

- PDF 表格和扫描件解析。
- chunk 语义完整性。
- 权限过滤。
- 召回准确率。
- 幻觉控制。
- 引用准确性。
- 文档增量更新。
- 延迟和成本。

---

## 30. 设计一个客服 Agent

### 30.1 核心能力

- 理解用户意图。
- 查询 FAQ / 知识库。
- 查询订单 / 物流 / 账户信息。
- 创建工单。
- 必要时转人工。
- 高风险操作二次确认。

### 30.2 架构

```text
User Message
  ↓
Intent Classifier
  ↓
Policy / Safety Check
  ↓
RAG FAQ Search
  ↓
Agent Planner
  ↓
Tool Calling: Order / Refund / Ticket / CRM
  ↓
Human Confirmation for Risky Actions
  ↓
Final Response
  ↓
Trace / Feedback / Quality Review
```

### 30.3 面试强调点

- 不让 Agent 直接执行退款、改地址等高风险动作。
- 只读工具和写操作工具分权限。
- 所有工具调用可审计。
- 失败时转人工。
- 有任务成功率、转人工率、用户满意度等指标。

---

## 31. 设计一个 AI Coding Agent

### 31.1 核心能力

- 理解代码仓库。
- 检索相关文件。
- 分析 issue。
- 修改代码。
- 运行测试。
- 生成 patch。
- 提交 PR。

### 31.2 难点

- 大仓库上下文太长。
- 需要精确检索相关代码。
- 修改代码不能破坏已有功能。
- 需要运行测试验证。
- 需要防止误删、误改。
- 需要权限和审计。

### 31.3 架构

```text
Issue / User Request
  ↓
Repo Indexer: AST / Symbol / Embedding / Keyword
  ↓
Context Retriever
  ↓
Planner
  ↓
Code Edit Tool
  ↓
Test Runner
  ↓
Static Analysis
  ↓
Patch Review
  ↓
PR Generation
```

---

# 第九部分：50 个必须准备的高频题

---

## 32. Agent / RAG 方向 25 题

- [ ] 1. RAG 是什么？
- [ ] 2. RAG 和微调怎么取舍？
- [ ] 3. chunk size 怎么设置？
- [ ] 4. overlap 有什么用？
- [ ] 5. embedding 模型怎么选？
- [ ] 6. 向量检索和 BM25 区别？
- [ ] 7. hybrid search 怎么做？
- [ ] 8. rerank 为什么有效？
- [ ] 9. RAG 幻觉怎么解决？
- [ ] 10. RAG 如何做权限控制？
- [ ] 11. 如何评估 RAG？
- [ ] 12. Agent 和 Chatbot 区别？
- [ ] 13. ReAct 原理是什么？
- [ ] 14. Tool Calling 怎么设计？
- [ ] 15. Function Calling 和 MCP 区别？
- [ ] 16. Agent 为什么会无限循环？
- [ ] 17. 如何限制 Agent 行为？
- [ ] 18. Agent memory 怎么设计？
- [ ] 19. Multi-Agent 有什么优缺点？
- [ ] 20. Workflow 和 Agent 怎么取舍？
- [ ] 21. LangGraph 解决什么问题？
- [ ] 22. Agent trace 记录什么？
- [ ] 23. Agent 失败如何回放？
- [ ] 24. 如何做 Agent eval？
- [ ] 25. 如何降低 Agent 延迟和成本？

## 33. LLM 方向 20 题

- [ ] 26. Transformer 结构。
- [ ] 27. Attention 公式。
- [ ] 28. MHA / MQA / GQA 区别。
- [ ] 29. RoPE 原理。
- [ ] 30. Decoder-only 为什么适合生成？
- [ ] 31. Tokenizer 原理。
- [ ] 32. SFT 是什么？
- [ ] 33. RLHF 是什么？
- [ ] 34. DPO 是什么？
- [ ] 35. GRPO 是什么？
- [ ] 36. LoRA 原理。
- [ ] 37. QLoRA 原理。
- [ ] 38. KV Cache 是什么？
- [ ] 39. Prefill 和 Decode 区别。
- [ ] 40. vLLM 为什么快？
- [ ] 41. PagedAttention 是什么？
- [ ] 42. Continuous Batching 是什么？
- [ ] 43. Speculative Decoding 是什么？
- [ ] 44. 量化有什么收益和风险？
- [ ] 45. 如何评估大模型输出质量？

## 34. 系统设计方向 5 题

- [ ] 46. 设计一个大模型网关。
- [ ] 47. 设计一个企业知识库问答系统。
- [ ] 48. 设计一个客服 Agent。
- [ ] 49. 设计一个 AI Coding Agent。
- [ ] 50. 设计一个 Prompt / Eval / Trace 平台。

---

# 第十部分：30 天准备计划

---

## 35. 第 1 周：后端基础 + 算法

目标：普通后端面试不丢分。

每天任务：

- 刷 3 到 5 道算法题。
- 复习一个基础专题。
- 总结 5 个八股回答。

重点：

```text
Day 1：数组、哈希、双指针
Day 2：链表、栈、队列
Day 3：树、递归、DFS / BFS
Day 4：图、拓扑排序、并查集
Day 5：动态规划
Day 6：OS、网络
Day 7：MySQL、Redis、MQ
```

---

## 36. 第 2 周：LLM + RAG

目标：能完整讲清楚 RAG 系统。

重点学习：

- Transformer 基础。
- Tokenizer。
- Embedding。
- 向量检索。
- BM25。
- Hybrid Search。
- Rerank。
- RAG Evaluation。
- 幻觉控制。
- 引用溯源。

本周产出：

- 一篇 RAG 面试笔记。
- 一个最小 RAG demo。
- 20 个 RAG 高频题口述答案。

---

## 37. 第 3 周：Agent 工程

目标：能讲清楚生产级 Agent 架构。

重点学习：

- ReAct。
- Tool Calling。
- Planner / Executor。
- Memory。
- Workflow。
- LangGraph。
- MCP。
- Guardrails。
- Trace。
- Agent Eval。

本周产出：

- 一个简化版 Agent loop。
- 一个工具调用 demo。
- 一个 Agent trace 记录表。
- 20 个 Agent 高频题口述答案。

---

## 38. 第 4 周：项目包装 + 模拟面试

目标：简历项目能抗住 30 分钟深挖。

准备内容：

- 项目架构图。
- 技术选型说明。
- 核心链路说明。
- 10 个失败 case。
- 10 个优化点。
- 5 分钟项目介绍。
- 30 分钟项目深挖回答。
- 1 套系统设计题：企业知识库 Agent。
- 1 套工程机试模板：LRU、限流器、Tool loop、RAG 检索器。

---

# 第十一部分：面试前速查清单

---

## 39. 技术速查

### 39.1 RAG 必背

- RAG = 检索增强生成。
- RAG 适合企业私有知识和动态知识。
- RAG 核心链路：parse → chunk → embedding → retrieve → rerank → generate → cite → eval。
- RAG 难点：解析、切分、召回、重排、幻觉、权限、评测。
- RAG 优化：query rewrite、hybrid search、rerank、prompt 约束、引用、评测集。

### 39.2 Agent 必背

- Agent = LLM + 目标 + 状态 + 工具 + 行动循环。
- Agent 核心：planner、tools、executor、memory、guardrail、trace、eval。
- 生产 Agent 不应完全自由，应结合 workflow。
- 高风险操作必须权限控制、人工确认、审计。
- Agent 评测要看过程，不只看最终答案。

### 39.3 推理优化必背

- Prefill 影响首 token 延迟。
- Decode 影响每 token 生成速度。
- KV Cache 用显存换速度。
- vLLM 通过 PagedAttention 和 continuous batching 提高吞吐。
- 成本优化靠缓存、路由、压缩、限流、小模型降级。

### 39.4 后训练必背

- SFT：让模型学会听指令。
- RLHF：人类偏好 → reward model → PPO 优化。
- DPO：直接用偏好数据优化模型，流程更简单。
- LoRA：冻结基座，只训练低秩 adapter。
- QLoRA：量化后做 LoRA，降低显存。

---

## 40. 项目介绍模板

面试时 3 到 5 分钟项目介绍可以按这个结构：

```text
我做的是一个企业知识库 Agent 系统，目标是让用户基于企业文档问答，并能调用内部工具完成订单查询、工单创建等任务。

系统分为文档处理、检索问答、Agent 工具调用、评测观测四部分。

文档侧支持 PDF / Markdown / HTML 解析，按标题和语义切 chunk，生成 embedding 后写入向量库，同时写入 Elasticsearch 做 BM25 检索。

问答侧使用 hybrid search 召回，再用 reranker 精排，最后把 top-k 上下文和引用信息放入 prompt，要求模型基于资料回答。

Agent 侧使用状态机 / LangGraph 管理流程，工具调用前做 schema 校验，设置 max_steps、timeout、retry，高风险操作需要人工确认。

工程侧记录每次请求的 trace、token、latency、tool result 和失败原因，并用自定义评测集统计准确率、召回率、幻觉率和任务成功率。
```

---

## 41. 项目深挖回答重点

面试官深挖时，你要围绕这些关键词回答：

```text
为什么这样设计？
有哪些失败 case？
你怎么评估？
优化前后有什么变化？
线上如何排查？
如何保证安全？
如何控制成本？
如何支持扩展？
```

不要只说“用了某框架”，要说：

```text
我遇到了什么问题。
我尝试了哪些方案。
我选择这个方案的原因。
我怎么验证它有效。
还有哪些不足。
```

---

# 第十二部分：投递关键词

---

## 42. 招聘网站搜索关键词

```text
AI Agent
Agent 开发
大模型应用开发
大模型应用工程师
LLM 应用开发
RAG
智能体
AI Coding
Workflow
MCP
LangGraph
大模型后端
大模型平台
大模型网关
LLM Infra
模型推理
推理加速
后训练
SFT
DPO
RLHF
```

### 42.1 后端背景优先投

```text
AI Agent 后端开发
大模型应用开发
RAG 应用开发
AI Coding 后端
大模型平台工程师
LLM 应用工程师
大模型网关开发
```

### 42.2 算法背景再投

```text
大模型算法工程师
大模型后训练工程师
Agent 算法工程师
大模型推理优化工程师
```

---

# 第十三部分：最后优先级总结

---

## 43. 最高优先级

```text
后端八股
算法机试
RAG 全流程
Agent 工程化
项目深挖
系统设计
```

## 44. 第二优先级

```text
Transformer
SFT / DPO / LoRA
KV Cache
vLLM
推理延迟和成本优化
模型评测
```

## 45. 第三优先级

```text
CUDA
Megatron
DeepSpeed
分布式训练
算子优化
通信优化
显存优化
```

---

## 46. 一句话策略

> 对大多数后端 / 应用开发背景的人来说，深圳大厂更现实的入口不是一上来卷底层训练算法，而是先用「RAG + Agent + 工程化 + 评测 + 系统设计」证明自己能把大模型能力落到真实业务里。

