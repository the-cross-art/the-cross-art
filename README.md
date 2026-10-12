<div align="center">

# Imran Nazir

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=20&pause=1200&color=58A6FF&center=true&vCenter=true&width=650&lines=AI+Applied+Engineer+II+%40+QuillBot+(Learneo);Building+GPU+Inference+Infra+at+Scale;LLM+Serving+%C2%B7+vLLM+%C2%B7+SGLang+%C2%B7+Triton;Civil+Engineer+%E2%86%92+ML+Systems+Engineer)](https://meimran.netlify.app/)

**AI Applied Engineer · LLM Serving · GPU Inference Infrastructure**

I build and operate the infrastructure that serves LLMs in production, and work upstream on the inference stacks that run them.

<p>
  <img alt="Profile views" src="https://komarev.com/ghpvc/?username=the-cross-art" />
  <a href="https://github.com/pulls?q=is%3Apr+is%3Amerged+author%3Athe-cross-art+archived%3Afalse"><img alt="Merged upstream PRs" src="https://img.shields.io/badge/Merged_upstream_PRs-2-2ea44f" /></a>
  <img alt="Users served" src="https://img.shields.io/badge/Serving-50M%2B_users-2ea44f" />
  <img alt="Focus" src="https://img.shields.io/badge/Focus-LLM_Inference_%26_ML_Platform-8A2BE2" />
</p>

[![Portfolio](https://img.shields.io/badge/Portfolio-meimran.netlify.app-0A0A0A?style=flat-square&logo=vercel&logoColor=white)](https://meimran.netlify.app/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-meimran-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/meimran/)
[![Medium](https://img.shields.io/badge/Medium-%40imrannaz326-12100E?style=flat-square&logo=medium&logoColor=white)](https://medium.com/@imrannaz326)
[![Email](https://img.shields.io/badge/Email-imrannaz326%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:imrannaz326@gmail.com)

</div>

## About

I design and operate the infrastructure that serves LLMs at production scale — currently supporting **50M+ users** as an AI Applied Engineer at QuillBot (Learneo). My work sits at the intersection of GPU inference internals, distributed systems, and ML platform engineering.

Trained originally as a civil engineer (B.Tech, BIT Sindri, 2023), I moved into ML systems through self-directed study and have since focused on the operational side of AI: making inference fast, reliable, and cheap at scale.

## Research & Focus Areas

- **LLM serving at scale** — throughput/latency trade-offs across vLLM, SGLang, and Triton Inference Server
- **GPU inference internals** — batching strategies, KV-cache management, capacity-aware scheduling
- **ML systems architecture** — designing platforms that stay reliable under production load
- **Kubernetes-native orchestration** for asynchronous, high-throughput inference workloads

## Open Source

<div align="center">
<table width="100%">
  <tr>
    <td width="84" align="center" valign="middle">
      <a href="https://github.com/huggingface/transformers/pull/49135"><img src="https://avatars.githubusercontent.com/u/25720743?v=4" width="52" height="52" alt="Hugging Face official GitHub avatar" /></a>
    </td>
    <td valign="top">
      <b>Hugging Face · transformers</b><br/>
      <sub>Attention correctness · SDPA · seq2seq training</sub><br/>
      UMT5 decoder causality fix · root-cause trace · regression tests<br/>
      <a href="https://github.com/huggingface/transformers/pull/49135"><b>View work →</b></a>
    </td>
  </tr>
  <tr>
    <td width="84" align="center" valign="middle">
      <a href="https://github.com/OpenNMT/CTranslate2/pull/2103"><img src="https://avatars.githubusercontent.com/u/23035727?v=4" width="52" height="52" alt="OpenNMT official GitHub avatar" /></a>
    </td>
    <td valign="top">
      <b>OpenNMT · CTranslate2</b><br/>
      <sub>Inference runtime · model conversion · C++</sub><br/>
      UMT5 support · per-layer attention bias · validated on a 2.9B checkpoint<br/>
      <a href="https://github.com/OpenNMT/CTranslate2/pull/2103"><b>View work →</b></a>
    </td>
  </tr>
</table>
</div>

<details>
<summary><b>Selected upstream impact — PR evidence</b></summary>

| Project | Contribution | Product / user impact |
| --- | --- | --- |
| **transformers** | [#49135](https://github.com/huggingface/transformers/pull/49135) — UMT5 decoder self-attention was not causal under SDPA | Restored causality for every UMT5 model trained or evaluated through the default `Seq2SeqTrainer` path; position-0 logit drift fell from ~1.03e-1 to ~1.91e-6 |
| **CTranslate2** | [#2103](https://github.com/OpenNMT/CTranslate2/pull/2103) — UMT5 inference support via per-layer relative attention bias | Made UMT5 servable on CTranslate2 for the first time, closing a 2+ year feature request with byte-identical output for existing T5/mT5 conversions |

**transformers [#49135](https://github.com/huggingface/transformers/pull/49135) — fix UMT5 decoder self-attention not being causal**

- **Problem:** `UMT5LayerSelfAttention` never passed `is_causal` to `UMT5Attention`. Under SDPA the causal mask is skipped when there is no padding, so during full-sequence teacher forcing — the path `DataCollatorForSeq2Seq` and `Seq2SeqTrainer` produce by default — the decoder could attend to future positions. `generate()` was unaffected, since it decodes one position at a time.
- **Root cause:** introduced in [#47014](https://github.com/huggingface/transformers/pull/47014), which moved the T5 family to SDPA and added the `is_causal` parameter without updating the call sites. v5.14.1 was correct; v5.15.0 onward was not.
- **Fix:** pass `is_causal=config.is_decoder` as T5/MT5 already do, and set `is_causal=False` explicitly on cross-attention. Added regression tests for the `is_causal` flag across all three attention types and for position-0 logit stability.
- **Verified:** log-probability drift at position 0 dropped from ~1.03e-1 to ~1.91e-6, matching the last known-good release.
- Merged into `main`; filed as [#49134](https://github.com/huggingface/transformers/issues/49134).

**CTranslate2 [#2103](https://github.com/OpenNMT/CTranslate2/pull/2103) — add UMT5 support (per-layer relative attention bias)**

- **Problem:** CTranslate2 could not convert UMT5. Unlike T5/mT5, which compute a relative attention bias at layer 0 and share it, UMT5 gives every self-attention layer its own bias table — a layout neither the converter nor the runtime stacks supported.
- **Fix:** added a `UMT5Loader` that preserves per-layer bias tables and overrides `get_vocabulary` so `<extra_id_*>` sentinels are not duplicated, and taught the encoder/decoder stacks to select a per-layer bias path only for models that need it — detected by pointer identity on aliased variables, so no config flag or model-format change was required.
- **Context:** closed a 2+ year-old request ([#1478](https://github.com/OpenNMT/CTranslate2/issues/1478)) that had stalled because the obvious fix risked slowing existing T5/mT5 models. `t5-small` `model.bin` is byte-identical before and after the converter change.
- **Verified:** added runtime regression tests using distinct, non-constant bias tables per stack, which fail when the runtime is forced to share layer 0's bias; validated end-to-end on a 2.9B-parameter UMT5 checkpoint on an NVIDIA L4.
- Merged into `master`. The parity gap that surfaced during review is what led to the `transformers` fix above.

</details>

> **Current footprint:** 2 merged PRs across 2 upstream inference projects — one correctness fix, one new model family — both traced from a single numerical discrepancy.
> I care about landing changes maintainers can trust more than PR volume.

## How I Contribute

<table width="100%">
  <tr>
    <td width="50%" valign="top"><b>Root cause over symptom</b><br/><sub>Trace a numerical mismatch to the line that causes it, even across repos.</sub></td>
    <td width="50%" valign="top"><b>Evidence before claims</b><br/><sub>Quantify the before/after and pin the first bad commit.</sub></td>
  </tr>
  <tr>
    <td width="50%" valign="top"><b>Narrow, reversible diffs</b><br/><sub>Keep existing models bit-identical; no config flags or format changes.</sub></td>
    <td width="50%" valign="top"><b>Tests that would have caught it</b><br/><sub>Regression tests that fail on the old behavior, not just pass on the new.</sub></td>
  </tr>
</table>

## Tech Stack

**LLM Serving & Inference**

![vLLM](https://img.shields.io/badge/vLLM-000000?style=flat-square) ![SGLang](https://img.shields.io/badge/SGLang-000000?style=flat-square) ![Triton Inference Server](https://img.shields.io/badge/Triton_Inference_Server-76B900?style=flat-square&logo=nvidia&logoColor=white) ![Ray Serve](https://img.shields.io/badge/Ray_Serve-028CF0?style=flat-square&logo=ray&logoColor=white) ![SageMaker](https://img.shields.io/badge/SageMaker-232F3E?style=flat-square&logo=amazonaws&logoColor=white)

**Orchestration & Infrastructure**

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white) ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

**Data Engineering**

![Apache Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white) ![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white) ![Airflow](https://img.shields.io/badge/Airflow-017CEE?style=flat-square&logo=apacheairflow&logoColor=white) ![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white) ![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=flat-square&logo=snowflake&logoColor=white)

**ML / AI**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![Hugging Face](https://img.shields.io/badge/Hugging_Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black) ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square) ![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square) ![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=flat-square&logo=mlflow&logoColor=white)

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white) ![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

## Contributions

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/the-cross-art/the-cross-art/main/dist/github-snake-dark.svg" />
  <img alt="Contribution grid snake" src="https://raw.githubusercontent.com/the-cross-art/the-cross-art/main/dist/github-snake.svg" />
</picture>

## Education

**B.Tech, Civil Engineering** — BIT Sindri, Dhanbad · 2019–2023 · CGPA 8.99

<div align="center">

[![Portfolio](https://img.shields.io/badge/Read_more_at_meimran.netlify.app-black?style=for-the-badge&logo=vercel&logoColor=white)](https://meimran.netlify.app/)

</div>
