<div align="center">

# Imran Nazir

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=20&pause=1200&color=58A6FF&center=true&vCenter=true&width=650&lines=AI+Applied+Engineer+II+%40+QuillBot+(Learneo);Building+GPU+Inference+Infra+at+Scale;LLM+Serving+%C2%B7+vLLM+%C2%B7+SGLang+%C2%B7+Triton;Civil+Engineer+%E2%86%92+ML+Systems+Engineer)](https://meimran.netlify.app/)

[![Portfolio](https://img.shields.io/badge/Portfolio-meimran.netlify.app-0A0A0A?style=flat-square&logo=vercel&logoColor=white)](https://meimran.netlify.app/)
[![GitHub](https://img.shields.io/badge/GitHub-the--cross--art-0A0A0A?style=flat-square&logo=github&logoColor=white)](https://github.com/the-cross-art)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-meimran-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/meimran/)
[![Medium](https://img.shields.io/badge/Medium-%40imrannaz326-12100E?style=flat-square&logo=medium&logoColor=white)](https://medium.com/@imrannaz326)
[![Email](https://img.shields.io/badge/Email-imrannaz326%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:imrannaz326@gmail.com)

[![Merged Upstream PRs](https://img.shields.io/badge/Merged_Upstream_PRs-2-2EA44F?style=flat-square&logo=github&logoColor=white)](https://github.com/pulls?q=is%3Apr+is%3Amerged+author%3Athe-cross-art+archived%3Afalse)
![Profile Views](https://komarev.com/ghpvc/?username=the-cross-art&color=58A6FF&style=flat-square&label=Profile+Views)

</div>

## About

I design and operate the infrastructure that serves LLMs at production scale — currently supporting **50M+ users** as an AI Applied Engineer at QuillBot (Learneo). My work sits at the intersection of GPU inference internals, distributed systems, and ML platform engineering.

Trained originally as a civil engineer (B.Tech, BIT Sindri, 2023), I moved into ML systems through self-directed study and have since focused on the operational side of AI: making inference fast, reliable, and cheap at scale.

## Research & Focus Areas

- **LLM serving at scale** — throughput/latency trade-offs across vLLM, SGLang, and Triton Inference Server
- **GPU inference internals** — batching strategies, KV-cache management, capacity-aware scheduling
- **ML systems architecture** — designing platforms that stay reliable under production load
- **Kubernetes-native orchestration** for asynchronous, high-throughput inference workloads

## Featured Collaborations

While adding UMT5 inference support to CTranslate2, I hit a numerical mismatch against Hugging Face's output — tracing it to its root cause meant fixing a bug upstream in `transformers` itself, closing the loop across both projects.

<table>
<tr>
<td width="72" align="center"><img src="https://github.com/huggingface.png" width="56" height="56"/></td>
<td>

**🤗 Hugging Face — `transformers`**  
*Correctness · SDPA attention · seq2seq training*

Fixed a decoder self-attention bug in UMT5 that silently broke causality under SDPA — a regression affecting `Seq2SeqTrainer`-based training/eval for every UMT5 model since v5.15. Verified fix cut logit drift from ~1e-1 to ~2e-6.

[View work →](https://github.com/huggingface/transformers/pull/49135)

</td>
</tr>
<tr>
<td width="72" align="center"><img src="https://github.com/OpenNMT.png" width="56" height="56"/></td>
<td>

**OpenNMT — `CTranslate2`**  
*Inference runtime · model conversion · C++*

Added UMT5 inference support by detecting per-layer vs. shared relative-attention-bias layout at conversion time — closing a 2+ year open feature request with zero regression to existing T5/mT5 models. Validated on a 2.9B-parameter checkpoint.

[View work →](https://github.com/OpenNMT/CTranslate2/pull/2103)

</td>
</tr>
</table>

**How I contribute:** trace numerical discrepancies to their root cause instead of patching symptoms · back fixes with reproducible, quantitative evidence · keep changes narrowly scoped and backward-compatible.

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

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

## Education

**B.Tech, Civil Engineering** — BIT Sindri, Dhanbad · 2019–2023 · CGPA 8.99

## Connect

<div align="center">

[![Portfolio](https://img.shields.io/badge/Read_more_at_meimran.netlify.app-black?style=for-the-badge&logo=vercel&logoColor=white)](https://meimran.netlify.app/)

</div>
