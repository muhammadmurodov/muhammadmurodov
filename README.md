<div align="center">

# Assalom aleykum, I'm Muhammad 👋

**AI / ML developer** based in Tashkent, Uzbekistan 🇺🇿

I build machine-learning systems end-to-end — from messy raw data to evaluated, honest models.
I care about leakage-safe evaluation, documenting a model's information ceiling, and shipping things that actually run.

<a href="https://www.linkedin.com/in/muhammad-murodov"><img src="https://img.shields.io/badge/LinkedIn-Muhammad%20Murodov-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="https://t.me/Muhammad_Murodov"><img src="https://img.shields.io/badge/Telegram-@Muhammad__Murodov-26A5E4?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram"></a>
<a href="mailto:muhammad.murodov.2006@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
<a href="https://github.com/muhammadmurodov"><img src="https://img.shields.io/badge/GitHub-muhammadmurodov-181717?style=for-the-badge&logo=github" alt="GitHub"></a>

</div>

---

### 🧰 Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL%20+%20pgvector-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)

---

## 🚀 Featured Projects

### 🏛️ my.gov.uz RAG — Uzbek Government-Services Q&A
> Retrieval-augmented Q&A over the public service catalog of [my.gov.uz](https://my.gov.uz),
> answering **Uzbek & Russian** questions about documents, fees, deadlines, and steps —
> grounded strictly in the scraped corpus, and it **refuses rather than guesses** when out of scope.

- **Hybrid retrieval:** vector nearest-neighbour (`bge-m3`) **+** Postgres full-text search, fused with Reciprocal Rank Fusion, then re-ranked by the `bge-reranker-v2-m3` cross-encoder
- **Two-layer grounding gate:** a logistic-regression topic classifier refuses off-topic queries *before* any LLM call, and a grounding-score floor blocks answers from weak context — every answer cites its service name + URL
- **Multi-turn** query rewriting so follow-ups (*"narxi qancha?"*) resolve to standalone queries, plus trigram spell-correction and a hand-curated synonym map (*tonirovka*, *propiska*)
- Hand-rolled Python — **no LangChain, no vector-DB SaaS** — shipped as an OpenAI-compatible API behind an **Open WebUI** chat frontend (Docker)

`Python · Postgres/pgvector · bge-m3 · cross-encoder rerank · Open WebUI`
&nbsp;→ **[repo](https://github.com/muhammadmurodov/my-gov-chatbot)**

---

### 🏠 Tashkent Apartment Price Prediction
> Regression model predicting apartment prices from **~7,500 real listings**.

- Cleaned data-entry errors (column swaps, price typos) via a domain **\$/m² sanity check**
- Leakage-safe **out-of-fold target encoding** for 1,500+ micro-neighborhoods
- **MAPE 14.5% · R² 0.738** — beats a naive baseline by **25%**
- Documented the model's information ceiling instead of overfitting

`HistGradientBoosting · scikit-learn · pandas`
&nbsp;→ **[notebook](https://colab.research.google.com/drive/1XavMAtZnnur9kx9BFMqLJJkTeBhpnElF?usp=sharing)**

---

<div align="center">

### 📊 GitHub Stats

<img height="165" src="https://github-readme-stats.vercel.app/api?username=muhammadmurodov&show_icons=true&hide_border=true&count_private=true" alt="stats">
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=muhammadmurodov&layout=compact&hide_border=true" alt="top langs">

<br><br>

📫 **[Email](mailto:muhammad.murodov.2006@gmail.com)** · **[LinkedIn](https://www.linkedin.com/in/muhammad-murodov)** · **[Telegram](https://t.me/Muhammad_Murodov)** · Based in Tashkent, UZ

</div>
