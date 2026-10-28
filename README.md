<div align="center">

# Imran Nazir

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=20&pause=1200&color=58A6FF&center=true&vCenter=true&width=650&lines=AI+Applied+Engineer+II+%40+QuillBot+(Learneo);Building+GPU+Inference+Infra+at+Scale;LLM+Serving+%C2%B7+vLLM+%C2%B7+SGLang+%C2%B7+Triton;Civil+Engineer+%E2%86%92+ML+Systems+Engineer)](https://meimran.netlify.app/)

**AI Applied Engineer · LLM Serving · GPU Inference Infrastructure**

[![Portfolio](https://img.shields.io/badge/Portfolio-meimran.netlify.app-0A0A0A?style=flat-square&logo=vercel&logoColor=white)](https://meimran.netlify.app/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-meimran-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/meimran/)
[![Medium](https://img.shields.io/badge/Medium-%40imrannaz326-12100E?style=flat-square&logo=medium&logoColor=white)](https://medium.com/@imrannaz326)
[![Email](https://img.shields.io/badge/Email-imrannaz326%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:imrannaz326@gmail.com)

</div>

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
      <a href="https://github.com/vllm-project/vllm-metal/pull/1182"><img src="https://avatars.githubusercontent.com/u/136984999?v=4" width="52" height="52" alt="vLLM official GitHub avatar" /></a>
    </td>
    <td valign="top">
      <b>vLLM · vllm-metal</b><br/>
      <sub>Multimodal serving · MLX/Metal · paged attention</sub><br/>
      LFM2-VL image input · vision-tower adapter · first-token parity<br/>
      <a href="https://github.com/vllm-project/vllm-metal/pull/1182"><b>View work →</b></a>
    </td>
  </tr>
  <tr>
    <td width="84" align="center" valign="middle">
      <a href="https://github.com/huggingface/transformers/pull/49135"><img src="https://avatars.githubusercontent.com/u/25720743?v=4" width="52" height="52" alt="Hugging Face official GitHub avatar" /></a>
    </td>
    <td valign="top">
      <b>Hugging Face · transformers</b><br/>
      <sub>Attention correctness · SDPA · seq2seq training</sub><br/>
      Decoder causality fix · root-cause trace · regression tests<br/>
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
| **vllm-metal** | [#1182](https://github.com/vllm-project/vllm-metal/pull/1182) — LFM2-VL image input on the paged path | `LFM2.5-VL-*` served text-only and silently dropped images. Now served end-to-end on Apple Silicon with EXACT first-token parity against native mlx-vlm, reproduced on a second independent setup |
| **transformers** | [#49135](https://github.com/huggingface/transformers/pull/49135) — UMT5 decoder self-attention was not causal under SDPA | The decoder could attend to future positions during teacher forcing, silently affecting every UMT5 model trained through the default `Seq2SeqTrainer` path. Position-0 logit drift fell from ~1e-1 to ~2e-6 |
| **CTranslate2** | [#2103](https://github.com/OpenNMT/CTranslate2/pull/2103) — UMT5 inference support via per-layer relative attention bias | Made UMT5 servable for the first time, closing a 2+ year feature request, with existing T5/mT5 conversions left byte-identical |

</details>

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

**Serving** · vLLM · SGLang · Triton Inference Server · Ray Serve · SageMaker
**Infrastructure** · Kubernetes · Docker · Helm · Terraform · AWS · GitHub Actions
**Data** · Spark · Kafka · Airflow · Databricks · Snowflake
**ML** · PyTorch · Hugging Face · LangGraph · MLflow
**Languages** · Python · SQL · C++ · TypeScript · Bash

## Contributions

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/the-cross-art/the-cross-art/main/dist/github-snake-dark.svg" />
  <img alt="Contribution grid snake" src="https://raw.githubusercontent.com/the-cross-art/the-cross-art/main/dist/github-snake.svg" />
</picture>
