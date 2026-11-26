# Grok vs Groq: two different AI companies

> **Answer first:** They only sound alike. **Grok** is a family of AI *models* (and the chatbot built on them) made by Elon Musk's AI company, **xAI**, now called **SpaceXAI** and part of SpaceX. **Groq** (with a "q") is an AI *inference* company: it builds the **LPU chip** and runs **GroqCloud**, a fast API that serves other people's models. One makes the brain; the other makes the engine that runs brains fast.

*Facts checked on 26 Nov 2026. This area moves fast, so re-check dates and versions.*

---

## 1. At a glance

| | **Grok (xAI / SpaceXAI)** | **Groq** |
|---|---|---|
| **What it is** | AI models plus a chatbot | AI inference chips plus a cloud API |
| **Layer of the AI stack** | Software: the model (training + product) | Hardware and infrastructure: running models (inference) |
| **Main product** | Grok models, the Grok app, Grok Build, a developer API | LPU (Language Processing Unit) chips, GroqCloud |
| **Founded** | xAI: March 2023 | 2016 |
| **Founder** | Elon Musk | Jonathan Ross (an inventor of Google's TPU) |
| **Owner today** | SpaceX (acquired xAI in Feb 2026; rebranded SpaceXAI in July 2026) | Independent company (see Nvidia deal below) |
| **What you buy** | Access to Grok models (app subscriptions, API tokens) | Fast, low-cost model serving via API (and LPU systems) |
| **Whose models run** | Its own Grok models | Mostly open-weight models (e.g., Llama) |
| **Selling point** | Model capability, especially coding/agents, plus X integration | Very low latency and efficient inference |

## 2. Grok in more detail

- **Origin:** xAI was founded by Musk in March 2023. The Grok chatbot launched in November 2023.
- **Corporate changes:** SpaceX acquired xAI in February 2026 (reported combined value about $1.25 trillion), SpaceX went public in June 2026, and the AI unit was rebranded **SpaceXAI** in July 2026.
- **Direction:** a coding and agentic-work push, including SpaceXAI's acquisition of the AI coding startup **Cursor** (reported ~$60B). Grok 4.5 (July 2026) was priced at $2 per million input and $6 per million output tokens.
- **Model cadence:** Grok 4.5 (July 2026), Grok 4.6 (Aug 2026), Grok 4.7 (Sept 2026), with a stated plan to ship new models roughly monthly. Newer versions may exist.
- **Name origin:** "grok" is a word from Robert Heinlein's 1961 novel *Stranger in a Strange Land*, meaning to understand something deeply.

## 3. Groq in more detail

- **Core idea:** a chip built only for inference. The **LPU** has a deterministic design and keeps hundreds of MB of on-chip SRAM as the primary weight storage (not a cache), which cuts memory latency. Groq says this gives predictable latency and lower power use than GPUs (company claims).
- **Products:** the LPU Inference Engine, and **GroqCloud**, a fully managed, OpenAI-compatible API for running models.
- **December 2025 Nvidia deal:** Groq signed a **non-exclusive licensing agreement** with Nvidia for its inference technology. Founder Jonathan Ross, president Sunny Madra and other team members joined Nvidia. The deal was reported at about $20B (a figure from an investor via CNBC, not disclosed by Groq).
- **After the deal:** Groq says it continues as an independent company, with Simon Edwards as CEO, and **GroqCloud keeps operating**.
- **Name note:** "Groq" predates Grok (2016 vs 2023), and the similar name has caused confusion since Grok launched.

## 4. How they relate

- **Not direct competitors.** Grok competes with models like GPT, Claude and Gemini. Groq competes with GPU-based inference providers and chip makers like Nvidia.
- **Complementary in principle.** Groq's cloud is built to serve models, so it could host a model like Grok if the model's owner allowed it. SpaceXAI is not known to rely on Groq's chips.
- **Link to training vs inference:** Grok is a product of **training** a model. Groq's business is **inference**. See `inference-vs-training.md`.

## 5. Memory aid

> **Grok = the brain (model). Groq = the engine (chip + cloud) that runs brains fast.**
> Spelling trick: Groq with a **q**, like *quick*.

---

## Sources
- [Groq: Nvidia non-exclusive licensing agreement](https://groq.com/newsroom/groq-and-nvidia-enter-non-exclusive-inference-technology-licensing-agreement-to-accelerate-ai-inference-at-global-scale)
- [Tom's Hardware: Nvidia confirms $20B Groq deal](https://www.tomshardware.com/tech-industry/semiconductors/nvidia-confirms-20-billion-groq-deal-to-bolster-ai-inference-dominance)
- [SiliconANGLE: Nvidia to license Groq technology](https://siliconangle.com/?p=726081)
- [Latent Space: Groq](https://latent.space/wiki/groq-94887790/)
- [Axios: SpaceXAI releases Grok 4.5](https://axios.com/2026/07/08/spacexai-grok-new-model)
- [The Star: Grok 4.5, SpaceX acquired xAI in February](https://www.thestar.com.my/tech/tech-news/2026/07/09/spacexai-launches-grok-45-model-for-coding-agentic-tasks)
- [Quartz: What is SpaceXAI](https://qz.com/what-is-xai-spacexai-elon-musk)
- [SiliconANGLE: SpaceXAI releases Grok 4.6](https://siliconangle.com/2026/08/12/spacexai-releases-flagship-grok-4-6-model-advanced-reasoning-capabilities/)
- [SiliconANGLE: SpaceX launches Grok 4.7](https://siliconangle.com/2026/09/21/spacex-launches-grok-4-7-with-long-horizon-processing-safety-upgrades/)
- [Quartz: Grok 4.5 launch and Cursor deal](https://qz.com/spacexai-grok-45-coding-model-launch-070926)
