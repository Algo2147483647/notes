# AlexNet 之后的 AI 关键里程碑

[TOC]

## 说明

这版时间线不再追求“大而全的分析列”，而是改成**高密度枚举表**。  
核心目标是让你通过“行”来建立完整地图，因此：

- 列减少为：`时间`、`领域`、`节点`、`核心贡献`
- 行显著增加，尽量覆盖视觉、NLP、强化学习、生成式、多模态、对齐、AI for Science、系统扩展
- 这份表依然是“关键节点表”，不是所有论文全集，但已经更接近书稿写作的底表

## Evolution Map (SVG)

![AI Evolution Map](./assets/ai_evolution_map_since_alexnet.svg)

## 高密度时间线

| 时间 | 领域 | 节点 | 核心贡献 |
| :--: | :--: | :--- | :------- |
| 2012 | 视觉 | **AlexNet** | 用深层 CNN 在 ImageNet 上建立压倒性优势，证明 GPU 驱动的深度学习可以在大规模感知任务中取代人工特征。 |
| 2013 | NLP | **word2vec** | 以 CBOW / Skip-gram 高效学习词向量，把分布式语义表示变成 NLP 标配。 |
| 2013 | 生成 | **VAE** | 将潜变量建模与神经网络结合，建立“编码到潜空间再生成”的现代生成模型主线之一。 |
| 2014 | NLP | **Seq2Seq** | 用 encoder-decoder 统一可变长输入输出，推动神经机器翻译替代传统统计机器翻译。 |
| 2014 | NLP | **Attention for NMT** | 用软对齐打破固定长度上下文瓶颈，首次把 attention 变成核心结构机制。 |
| 2014 | 生成 | **GAN** | 以生成器-判别器对抗训练建立高质量生成范式，开启现代图像生成浪潮。 |
| 2014 | 记忆增强 | **Neural Turing Machine** | 把神经网络与外部可读写内存结合，开启“可微分程序执行 / 神经符号”方向的一条主线。 |
| 2015 | 训练技术 | **Batch Normalization** | 显著稳定并加速深网训练，使更深更大的模型更容易优化。 |
| 2015 | 强化学习 | **DQN** | 通过经验回放和目标网络，让单个深度 RL 系统从像素中学习 Atari 控制策略。 |
| 2015 | 视觉 | **U-Net** | 用 encoder-decoder + skip connection 统一分割框架，成为医学影像与像素级预测的长期主干。 |
| 2015 | 视觉 | **ResNet** | 用残差连接解决超深网络优化问题，奠定后续几乎所有深层架构的基础。 |
| 2015 | 优化 | **Adam** | 以自适应一阶优化方法成为深度学习训练默认优化器之一。 |
| 2016 | 视觉生成 | **PixelRNN / PixelCNN** | 以像素级自回归方式实现显式生成建模，强化“生成可视作序列预测”的思路。 |
| 2016 | 语音 | **WaveNet** | 端到端原始波形生成显著提升语音合成自然度，展示生成模型对音频的能力。 |
| 2016 | 强化学习 | **AlphaGo** | 结合策略网络、价值网络与 MCTS，在围棋上首次击败职业棋手。 |
| 2016 | 元学习 | **Matching Networks / Meta-Learning 兴起** | few-shot learning 开始形成稳定研究方向，推动“少样本适配”成为长期主题。 |
| 2017 | 通用架构 | **Transformer** | 用自注意力替代递归，建立现代序列建模统一底座。 |
| 2017 | 强化学习 | **PPO** | 以更稳定、更易实现的策略优化方法成为强化学习后续实践常用标准方案。 |
| 2017 | 强化学习 | **AlphaZero** | 去除人工棋类知识，仅靠自博弈学习国际象棋、将棋、围棋，强化“通用学习 + 搜索”范式。 |
| 2017 | 视觉生成 | **Progressive GAN** | 用渐进式分辨率增长稳定高分辨率图像生成。 |
| 2018 | NLP | **ELMo** | 用上下文化词表示显著提升语言理解任务，说明静态词向量不够。 |
| 2018 | NLP | **ULMFiT** | 系统证明语言模型预训练 + 微调可以普遍提升下游任务。 |
| 2018 | NLP | **GPT-1** | 展示生成式预训练再微调可以统一多种 NLP 任务。 |
| 2018 | NLP | **BERT** | 用双向预训练显著刷新理解任务成绩，确立“预训练 + 微调”标准范式。 |
| 2018 | 视觉生成 | **StyleGAN** | 用风格控制与层级潜空间大幅提升图像生成质量和可控性。 |
| 2018 | 强化学习 | **Dreamer / Model-Based RL 路线加强前夜** | 强化学习开始重新重视世界模型与潜空间规划。 |
| 2019 | NLP | **GPT-2** | 显示大规模自回归语言模型具备明显零样本迁移潜力。 |
| 2019 | NLP | **RoBERTa** | 证明 BERT 类模型的很多收益来自更充分的训练而非复杂技巧。 |
| 2019 | NLP | **T5** | 把几乎所有 NLP 任务统一成 text-to-text 格式，强化“统一接口”思想。 |
| 2019 | 强化学习 | **MuZero** | 在不知道环境规则的情况下学习模型并规划，统一 Atari、围棋、国际象棋、将棋。 |
| 2019 | 视觉生成 | **StyleGAN2** | 显著改善伪影问题，使高保真人脸生成更成熟。 |
| 2019 | 视觉 | **EfficientNet** | 系统提出 compound scaling，使模型深度、宽度、分辨率协同缩放。 |
| 2020 | 理论 / 缩放 | **Scaling Laws** | 把参数、数据、算力与损失之间的缩放关系定量化。 |
| 2020 | NLP | **GPT-3** | 用 in-context learning 把 prompt 变成任务接口，弱化传统微调依赖。 |
| 2020 | 生成 | **DDPM** | 把扩散模型变成高质量、稳定的生成框架。 |
| 2020 | 视觉 | **DETR** | 把目标检测重写为 set prediction，让 Transformer 直接进入检测主线。 |
| 2020 | 表征学习 | **SimCLR** | 以对比学习强化自监督学习，推动“无标签预训练”在视觉中的主流化。 |
| 2020 | 知识增强 | **RAG** | 把检索与生成结合，开启“外部知识增强语言模型”路线。 |
| 2020 | 3D / 视觉 | **NeRF** | 用神经辐射场统一新视角合成和隐式三维表示，开启 3D 生成新方向。 |
| 2021 | 视觉 | **ViT** | 证明纯 Transformer 在视觉分类上可与 CNN 竞争甚至超越。 |
| 2021 | 多模态 | **CLIP** | 用海量图文对比学习获得强零样本视觉能力，建立图文基础模型主线。 |
| 2021 | 视觉生成 | **DALL·E** | 展示大规模文本到图像生成在概念组合上的强能力。 |
| 2021 | AI for Science | **AlphaFold 2** | 让蛋白质结构预测达到近实验级精度，AI 深度进入生命科学。 |
| 2021 | 模型扩展 | **Switch Transformer** | 用稀疏 MoE 把参数规模扩展到万亿级，同时保持可控计算成本。 |
| 2021 | 参数高效微调 | **Prefix-Tuning** | 证明不必全量微调，也能通过极少参数适配大模型。 |
| 2021 | 参数高效微调 | **LoRA** | 低秩适配成为后续开源大模型微调和部署的核心方法之一。 |
| 2021 | 强化学习 | **Decision Transformer** | 把强化学习重写为条件序列建模，体现 Transformer 对控制任务的统一能力。 |
| 2022 | 对齐 | **InstructGPT / RLHF** | 把模型从“会续写”推进到“会听指令、按人类偏好回答”。 |
| 2022 | 提示工程 / 推理 | **Chain-of-Thought Prompting** | 显式要求中间推理步骤，显著提升复杂推理任务表现。 |
| 2022 | 提示工程 / 推理 | **Self-Consistency** | 对多条推理链采样并投票，进一步提升推理稳定性。 |
| 2022 | 缩放 / 训练配比 | **Chinchilla** | 指出给定算力下参数和 token 数应更均衡，纠正只堆参数的粗放扩展。 |
| 2022 | 大模型 | **PaLM** | 展示超大规模语言模型在推理、代码、多语言上的强泛化。 |
| 2022 | 指令调优 | **FLAN / Flan-PaLM** | 证明大规模 instruction tuning 能显著提升零样本和少样本表现。 |
| 2022 | 多模态 | **Flamingo** | 展示少样本视觉-语言模型可以处理开放式多模态上下文。 |
| 2022 | 生成 | **Latent Diffusion** | 在潜空间进行扩散，把高质量图像生成成本大幅降下来。 |
| 2022 | 生成 | **Stable Diffusion** | 把文生图能力推向开源社区和大规模创作生态。 |
| 2022 | 语音 | **Whisper** | 用大规模弱监督语音识别实现强鲁棒、多语言 ASR。 |
| 2022 | 推理 / 代理 | **ReAct** | 把 reasoning 与 acting 结合，使模型可边推理边调用外部动作。 |
| 2022 | 产品化 | **ChatGPT** | 把 LLM 以对话产品形式推向大众，AI 进入主流软件与消费市场。 |
| 2023 | 开放模型 | **LLaMA** | 证明中等规模、训练充分的开放基础模型也可具备很强竞争力。 |
| 2023 | 多模态助手 | **GPT-4** | 在可靠性、复杂任务处理和图像输入上实现明显跃迁。 |
| 2023 | 对齐 | **DPO** | 以更简单的偏好优化方式替代复杂 RLHF 管线中的一部分工程负担。 |
| 2023 | 视觉基础模型 | **Segment Anything (SAM)** | 建立通用分割基础模型，提示驱动分割成为新交互模式。 |
| 2023 | 多模态指令 | **LLaVA** | 把视觉编码器与 LLM 结合，推动开源视觉问答 / 多模态助手爆发。 |
| 2023 | 长上下文 | **RAG 工程化与长上下文模型兴起** | 大模型开始同时沿“更长上下文”和“更强检索增强”两条路线演化。 |
| 2023 | 代码模型 | **Code Llama / 专用代码 LLM 系列** | 代码生成进入专门优化阶段，编程助手成为核心应用形态。 |
| 2023 | 开放生态 | **Mistral / Mixtral** | 高效架构和稀疏专家路线在开源生态中快速成熟。 |
| 2024 | 视频生成 | **Sora** | 文生视频在一致性、时长、镜头语言和世界动态建模上迈过重要门槛。 |
| 2024 | 实时多模态 | **GPT-4o** | 单模型统一处理文本、视觉、音频，显著降低实时交互延迟。 |
| 2024 | AI for Science | **AlphaFold 3** | 把结构预测扩展到蛋白、核酸、小分子、离子等复杂生物分子体系。 |
| 2024 | 推理模型 | **OpenAI o1** | 把 test-time reasoning 明确产品化，强调“花更多推理算力思考”。 |
| 2024 | 开放多模态 | **开源 VLM 与端侧多模态加速** | 多模态模型开始从云端研究系统走向更普遍的部署形态。 |
| 2025 | 推理模型 | **DeepSeek-R1** | 用强化学习系统激发推理能力，并以开放模型路线形成广泛影响。 |
| 2025 | 推理生态 | **Reasoning model 成为独立赛道** | 行业从“通用聊天模型”分化出“专门推理模型”，训练与评估体系开始重新定义。 |

## 2023-2026 大模型爆炸期细表

这一段单独拉出来，是因为 **2023-2026 不是普通增量期，而是基础模型、推理模型、多模态模型、Agent 模型同时爆发的阶段**。  
下面这张表的目标不是“精选”，而是把你写书时最容易反复引用的关键节点尽量铺平。
其中一部分商业模型没有统一论文版本，因此日期有时采用**官方公开发布日期**，有时采用**官方系统卡 / 技术报告的公开月份**。

| 时间 | 节点 | 关键词 | 为什么关键 |
| :--: | :--- | :----- | :--------- |
| 2023-03-14 | **GPT-4** | 多模态输入、可靠性跃迁 | 标志闭源前沿模型从“能聊”走向“可承担复杂专业任务”，也让图像输入正式进入主流 LLM。 |
| 2023-05-29 | **DPO** | 偏好优化简化 | 把偏好对齐从奖励模型 + RL 的复杂管线，简化成更直接的优化目标，显著影响后续后训练工程。 |
| 2023-07 | **Claude 2** | 长上下文、企业可用性 | 代表 Claude 路线进入主流竞争，长上下文和稳健写作能力开始成为差异化卖点。 |
| 2023-07-18 | **Llama 2** | 开放权重、Chat 模型开源化 | 让“高质量基础模型 + 对话微调 + 商业可用许可”进入开源主线，极大推动私有部署和二次训练生态。 |
| 2023-08 | **Code Llama** | 代码专用 LLM | 大模型开始从通用聊天进一步分化出代码专门模型，编程成为第一波高价值垂直场景。 |
| 2023-10-10 | **Mistral 7B** | 小模型高效率、GQA、SWA | 证明 7B 级模型通过结构设计与训练质量也能打出极强性能，开源生态从“追大”转向“追效率”。 |
| 2024-01-08 | **Mixtral 8x7B** | 稀疏 MoE 开源化 | 把 MoE 从大厂内部路线带入开源主流，展示“总参数大、激活参数小”的性能/成本优势。 |
| 2024-02-15 | **Gemini 1.5 Pro** | MoE、超长上下文 | 1M 级上下文窗口把“长文档 / 多模态长序列处理”推到新阶段，长上下文正式成为前沿竞争维度。 |
| 2024-03 | **Claude 3 family** | Opus / Sonnet / Haiku 分层 | 前沿模型开始系统化分层，不再只拼单一旗舰，而是形成速度、成本、能力分档的产品线。 |
| 2024-04-18 | **Llama 3** | 开源质量跃迁 | 开放权重模型在通用能力上进一步逼近闭源阵营，证明高质量开放生态已经成为长期力量。 |
| 2024-05-13 | **GPT-4o** | omni、端到端多模态、实时交互 | 文本、视觉、音频进入单模型统一处理阶段，多模态从“拼接流水线”转向“端到端模型”。 |
| 2024-06-20 | **Claude 3.5 Sonnet** | 编码、写作、Agent 工作流 | 这一代 Claude 明显强化代码、文档、工具协同能力，推动“用模型做持续工作流”而不是一次性问答。 |
| 2024-07 | **DeepSeek-Coder-V2** | 开源代码 MoE | 开源代码模型在性能上进一步逼近闭源强者，代码智能不再由少数闭源模型垄断。 |
| 2024-07-31 | **Llama 3.1 / 405B** | 超大开源旗舰、128K 上下文 | 405B 级开放权重模型让“开源也能有真正旗舰”成为现实，私有部署与蒸馏生态进一步扩张。 |
| 2024-09-12 | **OpenAI o1** | reasoning model、test-time compute | 把“思考更久换更强推理”正式产品化，reasoning model 从提示技巧升级为模型类别。 |
| 2024-09-19 | **Qwen2.5** | 中文强势、全尺寸家族、代码/数学增强 | Qwen 家族进入真正成熟期，成为中文和开源生态中的核心基础模型之一。 |
| 2024-09 | **Qwen2.5-Math** | 数学专门模型 | 说明大模型开始出现更细的专家化路线，不再只追求单一通用分数。 |
| 2024-11-15 | **Qwen2.5-Turbo 1M** | 百万上下文、低成本推理 | 长上下文能力进一步进入可用区间，并强调成本效率而不是只强调最大窗口。 |
| 2024-12-11 | **Gemini 2.0** | agentic era、原生工具使用、多模态输出 | 标志 Google 把大模型竞争重心从“更会答题”推进到“更会行动、会调用工具、会多模态输出”。 |
| 2024-12-13 | **DeepSeek-VL2** | MoE VLM、多模态理解 | 展示 DeepSeek 路线不只在文本推理推进，也开始在多模态理解上系统建模。 |
| 2024-12-27 | **DeepSeek-V3** | 671B MoE、MLA、低成本训练 | 以较低训练成本实现开放模型中的极强性能，强化“结构创新 + 工程效率”路线。 |
| 2025-01-22 | **DeepSeek-R1** | 纯 RL 激发推理、开放推理模型 | 证明强推理能力可以通过强化学习显式诱导，而不是只能依赖人类标注长推理链。 |
| 2025-02-24 | **Claude 3.7 Sonnet** | hybrid reasoning、可控思考深度 | 把普通响应与 extended thinking 结合，说明 reasoning 不再是独立模型，也可以成为混合交互模式。 |
| 2025-02-27 | **GPT-4.5** | 大规模预训练继续扩展 | 代表“更大、更有知识、更自然”的主线仍未结束，说明预训练扩展与 reasoning 路线仍在并行。 |
| 2025-03-27 | **Qwen2.5-Omni** | 端到端多模态输入输出 | 中文和开源生态也进入 omni 阶段，多模态不再是 GPT-4o 一家的形态创新。 |
| 2025-04-14 | **GPT-4.1** | 1M context、编码、指令遵循、Agent 适配 | 把长上下文与高质量 coding / instruction following 结合，明显朝 agent 基础模型方向优化。 |
| 2025-04-16 | **OpenAI o3 / o4-mini** | 工具调用推理、图像推理、agentic tool use | reasoning model 首次把“会思考”与“会调用工具”深度融合，向真正可执行任务的 agent 过渡。 |
| 2025-04-29 | **Qwen3** | thinking / non-thinking 双模式、Agent 能力、119 语言 | 开源阵营开始系统引入“思考模式切换”和推理预算控制，说明 reasoning 进入基础模型默认配置。 |
| 2025-05 | **Claude 4 / Sonnet 4 / Opus 4** | Agent、编码、长任务可靠性 | Claude 路线明确向软件工程和长期代理任务推进，模型能力开始围绕“稳定完成工作”定义。 |
| 2025-08-07 | **GPT-5** | coding-first、agentic workflows | OpenAI 把主线明确转向编码协作和 agent 工作流，说明“完成工作”压过“仅做聊天”。 |
| 2025-09 | **GPT-5-Codex** | 原生终端/IDE 工作流 | frontier 模型开始直接嵌入开发环境，模型从 API / Chat 界面深入到工程执行界面。 |
| 2025-12-17 | **Gemini 3 Flash** | 前沿智能 + 高速度 + Agent 工作流 | 速度与前沿能力开始同时成为卖点，agent 工作流不再只能依靠昂贵旗舰模型。 |
| 2026-02-05 | **Claude Opus 4.6** | 1M 上下文、编码、AI agents | Anthropic 把前沿大模型进一步推向高可靠编码与 Agent 执行，长上下文成为默认能力而非特色能力。 |
| 2026-03-05 | **GPT-5.4** | 主线 reasoning + coding + computer use 融合 | 代表 2026 年前沿模型的一个收敛方向：推理、编码、工具、长上下文、computer use 被并入单一主线模型。 |

## 这张细表反映出的 8 个趋势

1. **闭源旗舰仍在拉前沿**：GPT-4、GPT-4o、o1、o3、GPT-5、GPT-5.4、Claude 3.7、Claude 4.6、Gemini 2.0、Gemini 3 Flash。
2. **开源 / 开放权重不再只是跟随**：Llama 2、Llama 3、Llama 3.1、Mistral 7B、Mixtral、Qwen2.5、Qwen3、DeepSeek-V3、DeepSeek-R1。
3. **长上下文从特色功能变成基础配置**：Gemini 1.5、Qwen2.5-Turbo、GPT-4.1、Claude Opus 4.6、GPT-5.4。
4. **reasoning 从提示技巧变成模型品类**：o1、Claude 3.7、DeepSeek-R1、Qwen3、GPT-5.4。
5. **多模态从“能看图”升级为“端到端实时交互”**：GPT-4o、Qwen2.5-Omni、Gemini 2.0。
6. **Agent 化让模型竞争维度改变**：Deep Research、o3/o4-mini、GPT-5、Gemini 2.0、Claude 4、GPT-5.4。
7. **代码成为最先跑通的高价值场景**：Code Llama、Claude 3.5 Sonnet、DeepSeek-Coder-V2、GPT-4.1、GPT-5、GPT-5-Codex。
8. **结构效率越来越重要**：MoE、MLA、长上下文优化、参数高效后训练、推理预算控制，已经与单纯堆参数同等重要。

## 适合继续补充的 10 个专题簇

如果后续你要把这份底表继续扩成书稿，最值得继续加密的不是再随机加论文，而是沿下面 10 个簇继续补：

1. **视觉主线**：AlexNet, VGG, Inception, ResNet, EfficientNet, ViT, DETR, SAM
2. **语言模型主线**：word2vec, ELMo, ULMFiT, GPT-1, BERT, GPT-2, T5, GPT-3, LLaMA, GPT-4
3. **生成模型主线**：VAE, GAN, PixelCNN, DDPM, Latent Diffusion, Stable Diffusion, Sora
4. **强化学习主线**：DQN, PPO, AlphaGo, AlphaZero, MuZero, Decision Transformer
5. **对齐主线**：InstructGPT, RLHF, DPO, preference modeling, safety evaluation
6. **推理主线**：Chain-of-Thought, Self-Consistency, ReAct, o1, DeepSeek-R1
7. **多模态主线**：CLIP, DALL·E, Flamingo, LLaVA, GPT-4o, Sora
8. **AI for Science 主线**：AlphaFold 2, AlphaFold 3, 结构生物学与分子设计
9. **参数高效与部署主线**：Prefix-Tuning, LoRA, quantization, MoE
10. **知识增强与代理主线**：RAG, tool use, retrieval systems, agent workflows

## 代表性一手资料

- AlexNet: https://papers.nips.cc/paper_files/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html
- word2vec: https://arxiv.org/abs/1301.3781
- VAE: https://arxiv.org/abs/1312.6114
- Seq2Seq: https://arxiv.org/abs/1409.3215
- Attention for NMT: https://arxiv.org/abs/1409.0473
- GAN: https://arxiv.org/abs/1406.2661
- Batch Normalization: https://arxiv.org/abs/1502.03167
- DQN: https://www.nature.com/articles/nature14236
- U-Net: https://lmb.informatik.uni-freiburg.de/Publications/2015/RFB15a
- ResNet: https://openaccess.thecvf.com/content_cvpr_2016/html/He_Deep_Residual_Learning_CVPR_2016_paper.html
- WaveNet: https://arxiv.org/abs/1609.03499
- AlphaGo: https://www.nature.com/articles/nature16961
- Transformer: https://arxiv.org/abs/1706.03762
- PPO: https://arxiv.org/abs/1707.06347
- AlphaZero: https://arxiv.org/abs/1712.01815
- ELMo: https://arxiv.org/abs/1802.05365
- GPT-1: https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf
- BERT: https://arxiv.org/abs/1810.04805
- GPT-2: https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf
- RoBERTa: https://arxiv.org/abs/1907.11692
- T5: https://arxiv.org/abs/1910.10683
- MuZero: https://www.nature.com/articles/s41586-020-03051-4
- Scaling Laws: https://arxiv.org/abs/2001.08361
- GPT-3: https://arxiv.org/abs/2005.14165
- DDPM: https://arxiv.org/abs/2006.11239
- DETR: https://arxiv.org/abs/2005.12872
- SimCLR: https://arxiv.org/abs/2002.05709
- RAG: https://arxiv.org/abs/2005.11401
- NeRF: https://arxiv.org/abs/2003.08934
- ViT: https://openreview.net/forum?id=YicbFdNTTy
- CLIP: https://proceedings.mlr.press/v139/radford21a.html
- DALL·E: https://arxiv.org/abs/2102.12092
- AlphaFold 2: https://www.nature.com/articles/s41586-021-03819-2
- Switch Transformer: https://jmlr.org/papers/v23/21-0998.html
- LoRA: https://arxiv.org/abs/2106.09685
- Decision Transformer: https://arxiv.org/abs/2106.01345
- InstructGPT: https://arxiv.org/abs/2203.02155
- Chain-of-Thought: https://arxiv.org/abs/2201.11903
- Chinchilla: https://arxiv.org/abs/2203.15556
- PaLM: https://arxiv.org/abs/2204.02311
- FLAN: https://openreview.net/forum?id=gEZrGCozdqR
- Whisper: https://cdn.openai.com/papers/whisper.pdf
- ReAct: https://arxiv.org/abs/2210.03629
- Scaling Instruction-Finetuned LMs: https://arxiv.org/abs/2210.11416
- Latent Diffusion: https://arxiv.org/abs/2112.10752
- ChatGPT: https://openai.com/index/chatgpt/
- LLaMA: https://arxiv.org/abs/2302.13971
- GPT-4: https://openai.com/index/gpt-4-research/
- DPO: https://arxiv.org/abs/2305.18290
- Claude system cards: https://www.anthropic.com/system-cards/
- Llama 2: https://arxiv.org/abs/2307.09288
- Mistral 7B: https://arxiv.org/abs/2310.06825
- Mixtral: https://arxiv.org/abs/2401.04088
- Gemini 1.5: https://blog.google/innovation-and-ai/products/google-gemini-next-generation-model-february-2024/
- Claude 3 family: https://www-cdn.anthropic.com/c6a80a657af445f40e31afac050f3bf76d3b1404.pdf
- Llama 3 herd: https://arxiv.org/abs/2407.21783
- Qwen2.5: https://qwenlm.github.io/blog/qwen2.5/
- Qwen2.5-Turbo: https://qwenlm.github.io/blog/qwen2.5-turbo/
- Gemini 2.0: https://blog.google/innovation-and-ai/models-and-research/google-deepmind/google-gemini-ai-update-december-2024/
- DeepSeek-V3: https://arxiv.org/abs/2412.19437
- Claude 3.7 Sonnet: https://docs.anthropic.com/en/release-notes/api
- GPT-4.5: https://openai.com/index/gpt-4-5-system-card/
- Qwen2.5-Omni: https://qwenlm.github.io/blog/qwen2.5-omni/
- GPT-4.1: https://openai.com/index/gpt-4-1/
- SAM: https://arxiv.org/abs/2304.02643
- LLaVA: https://arxiv.org/abs/2304.08485
- Sora: https://openai.com/index/sora/
- GPT-4o: https://openai.com/index/hello-gpt-4o/
- AlphaFold 3: https://www.nature.com/articles/s41586-024-07487-w
- OpenAI o1: https://openai.com/index/introducing-openai-o1-preview/
- OpenAI o3 / o4-mini: https://openai.com/index/introducing-o3-and-o4-mini/
- Qwen3: https://qwenlm.github.io/zh/blog/qwen3/
- GPT-5: https://openai.com/index/introducing-gpt-5-for-developers/
- Gemini 3 Flash: https://blog.google/products-and-platforms/products/gemini/gemini-3-flash/
- Claude Opus 4.6: https://www.anthropic.com/claude/opus
- GPT-5.4: https://openai.com/index/introducing-gpt-5-4/
- DeepSeek-R1: https://arxiv.org/abs/2501.12948
