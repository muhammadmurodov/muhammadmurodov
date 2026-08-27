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
![XGBoost](https://img.shields.io/badge/XGBoost-337AB7?style=flat-square)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Ultralytics](https://img.shields.io/badge/YOLO-Ultralytics-111F68?style=flat-square)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL%20+%20pgvector-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

---

## 🚀 Featured Projects

### 🏛️ my.gov.uz RAG — Uzbek Government-Services Q&A &nbsp;![WIP](https://img.shields.io/badge/status-actively%20developing-F59E0B?style=flat-square)
> Retrieval-augmented Q&A over the public service catalog of [my.gov.uz](https://my.gov.uz),
> answering **Uzbek & Russian** questions about documents, fees, deadlines, and steps —
> grounded strictly in the scraped corpus, and it **refuses rather than guesses** when out of scope.

- **Hybrid retrieval:** vector nearest-neighbour (`bge-m3`, 1024-dim, cosine) **+** Postgres full-text search, fused with Reciprocal Rank Fusion, then re-ranked by the `bge-reranker-v2-m3` cross-encoder that reads each *(query, chunk)* pair together
- **Two-layer grounding gate** — the source of the "no hallucination" guarantee: a logistic-regression topic classifier refuses off-topic queries *before* any retrieval or LLM call, and a grounding-score floor blocks answers built on weak context. Every answer that passes cites its service name + URL
- **Robust to real queries:** trigram spell-correction against the corpus vocabulary (*ikadastr → kadastr*) and a hand-curated synonym map so loanwords people actually type (*tonirovka*, *propiska*) stay findable
- **Multi-turn** aware — a cheap rewrite step turns a follow-up like *"narxi qancha?"* into a standalone query for retrieval, while the answer call still sees prior turns for natural tone
- Hand-rolled Python — **no LangChain, no vector-DB SaaS** — served as an OpenAI-compatible API behind an **Open WebUI** chat frontend (Docker); ships with a pytest suite

`Python · Postgres/pgvector · bge-m3 · cross-encoder rerank · OpenRouter · Open WebUI · Docker`
&nbsp;→ **[repo](https://github.com/muhammadmurodov/my-gov-chatbot)**

> 🚧 **Currently working on this** — actively refining retrieval quality, the grounding gate, and the corpus.

---

### 🏠 Tashkent Apartment Price Prediction
> Regression model predicting apartment prices from **~7,500 real Tashkent listings**, built end-to-end on the CRISP-DM workflow.

- **Data cleaning with a domain lens:** dropped `Договорная` ("negotiable") prices and land-plot rows (~1.3% invalid), then used a **\$/m² sanity check** to catch column swaps and price typos before trimming outliers (0.5–99.5% of price/m², size 15–400 m²)
- **Leakage-safe out-of-fold target encoding** (5-fold) for `district` and ~1,500 micro-neighborhoods parsed from the address — test rows encoded from *full-train* means only, never their own target
- **Engineered signal:** `first_floor` / `top_floor` discounts, `level_ratio`, `size_per_room`; `log1p(price)` to fix right-skew
- **Results (`HistGradientBoosting`):** **MAE \$9,965 · MAPE 14.5% · R² 0.738**, vs a district-median \$/m² baseline at MAE \$13,270 · MAPE 19.0% · R² 0.633 — **~25% lower error**
- Per-district error analysis showed accuracy tracks data volume (best in high-listing districts) — I documented the model's information ceiling instead of overfitting

`HistGradientBoostingRegressor · scikit-learn · pandas · numpy`
&nbsp;→ **[Colab notebook](https://colab.research.google.com/drive/1XavMAtZnnur9kx9BFMqLJJkTeBhpnElF?usp=sharing)**

---

### 🚇 Metro Passenger Flow Forecasting
> Short-term (15-minute) forecasting of station-level metro passenger inflow for crowd management — AI/ML Fundamentals capstone, with a live demo.

- **Data:** HZMetro (Hangzhou Metro) AFC tap records — 80 stations, Jan 2019 — aggregated to 15-min inflow/outflow per station
- **Leakage-controlled protocol:** strictly chronological split (train Jan 1–18 / val 19–20 / test 21–25), scalers fit on train only, lags computed per-station from past intervals, test touched once after model selection
- **Model gate:** compared Historical-Average baseline, Ridge, and XGBoost under MLflow; **XGBoost selected on validation MAE 22.42 vs baseline 29.34 (~24% better)**, test MAE **25.75**; a symmetric outflow model was also trained

| Model | Val MAE | Test MAE |
|---|---|---|
| Historical Average (baseline) | 29.34 | 37.55 |
| Ridge | 29.29 | 39.29 |
| **XGBoost (selected)** | **22.42** | **25.75** |

- Error analysis by peak/off-peak & station busyness, plus a **Responsible-AI write-up** (advisory-only, aggregate-count privacy, fairness across stations, no direct Tashkent transfer)

`XGBoost · scikit-learn · pandas · MLflow · Streamlit`
&nbsp;→ **[repo](https://github.com/muhammadmurodov/metro-flow-forecasting)** · **[live demo](https://metro-flow-forecasting.streamlit.app)**

---

### 🐝 Beekeeping — Bee Health Detection
> Computer-vision web app that detects elements inside beehives to support hive monitoring, deployed live on Streamlit.

- Trained an **Ultralytics YOLO** detector (`yolo11s`, 60 epochs, 640 px) to detect **12 hive classes** — honey, nectar, pupae stages, empty cells, and other structures
- **Streamlit app** accepts images or videos and draws bounding boxes + labels in the browser; runs on **CPU** so it deploys on Streamlit Cloud
- Structured for iteration — model retrains and class set expands as more labeled data is collected

`Ultralytics YOLO · PyTorch · OpenCV · Streamlit`
&nbsp;→ **[repo](https://github.com/muhammadmurodov/Beekeeping)** · **[live demo](https://beekeeping.streamlit.app)**

---

### 🐳 Docker Mini Project — Containerized Timetable App
> A Flask + PostgreSQL university-timetable web app, fully containerized — a hands-on take on the build → run → deploy loop.

- **Flask** app queries a **PostgreSQL** database (via `pg8000`) and renders a level-filtered timetable through Jinja templates
- **Dockerized** on `python:3.13-slim` with system deps and a reproducible `requirements.txt` install; DB runs as its own Postgres container
- Documents the full workflow — pulling the Postgres image, schema + seed SQL, and running the app in an isolated container

`Docker · Flask · PostgreSQL · pg8000`
&nbsp;→ **[repo](https://github.com/muhammadmurodov/docker-mini-project)**

---

<div align="center">

### 📊 GitHub Stats

<img height="165" src="https://github-readme-stats.vercel.app/api?username=muhammadmurodov&show_icons=true&hide_border=true&count_private=true" alt="stats">
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=muhammadmurodov&layout=compact&hide_border=true" alt="top langs">

<br><br>

📫 **[Email](mailto:muhammad.murodov.2006@gmail.com)** · **[LinkedIn](https://www.linkedin.com/in/muhammad-murodov)** · **[Telegram](https://t.me/Muhammad_Murodov)** · Based in Tashkent, UZ

</div>
