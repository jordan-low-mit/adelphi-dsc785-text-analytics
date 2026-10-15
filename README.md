# DSC 785: Text Analytics

Adelphi University, Robert B. Willumstad School of Business · Graduate (MS in Business Analytics) · Summer sessions, 2024 to 2026

A graduate course on the modern text analytics pipeline: collecting data from the web and from SEC filings, storing documents in MongoDB, retrieving them with keyword, semantic and hybrid search, and building retrieval-augmented generation (RAG) that answers only from its sources. The examples come from finance (ETF holdings, 10-K filings and company research), and the projects ask students to act as analysts who must defend every number in front of a decision-maker. Most notebooks here are from the Summer 2026 offering; one is from 2024.

## What students learn

- Getting real data off the web: finding the data endpoint behind a page (the iShares IVV holdings file), and parsing HTML tables and embedded JSON with Beautiful Soup.
- Reading SEC filings programmatically: pulling company metadata and the key 10-K sections (Items 1, 1A and 7) with `edgartools`, and comparing the GICS and SIC industry classifications.
- Working with document data in MongoDB: regex parsing of messy, string-typed metrics; unique, compound, multikey, text and wildcard indexes; aggregation pipelines; and `explain()` to confirm an index is used.
- Search three ways: `$text`, BM25 through Atlas Search, and vector search on sentence-transformer embeddings, fused into hybrid retrieval with Reciprocal Rank Fusion (RRF), and scored with Retrieval@K against a truth set the students build and defend.
- Choosing an embedding model with evidence: a bake-off between `all-MiniLM-L6-v2` and `nomic-embed-text-v1.5`, with the evaluation standard written down before the experiments are run.
- Building and evaluating RAG: structure-aware chunking, prompts that require a citation for every claim and a fixed refusal when the answer is not in the sources, generation with DeepSeek or a local model through Ollama, and evaluation of faithfulness, relevance and coherence.
- Provenance: telling a fact stated in a filing from a judgment a model made about it, and tracing every claim back to its source.

## Highlights

| Notebook | What it covers | Open |
|---|---|---|
| [01_sp500_holdings_to_sec_filings](notebooks/01_sp500_holdings_to_sec_filings.ipynb) | Project 1 template, "S&P 500: From ETF Holdings to SEC Filings". Scrape and clean the IVV holdings file, sector and concentration analysis (cumulative weight, HHI), enrichment from EDGAR with error logging, GICS versus SIC, extraction of 10-K Items 1, 1A and 7, and a sector deep dive built on the group's own questions. Hypotheses must be written before the code is run. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jordan-low-mit/adelphi-dsc785-text-analytics/blob/main/notebooks/01_sp500_holdings_to_sec_filings.ipynb) |
| [02_mongodb_and_web_mining](notebooks/02_mongodb_and_web_mining.ipynb) | Notebook from the 2024 offering. SPDR ETF holdings from ssga.com stored as MongoDB documents (three document designs compared), indexes and `explain()`, then scraping an ETF list with Beautiful Soup from both the HTML table and the page's embedded JSON. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jordan-low-mit/adelphi-dsc785-text-analytics/blob/main/notebooks/02_mongodb_and_web_mining.ipynb) |
| [03_vector_search_and_hybrid_rrf](notebooks/03_vector_search_and_hybrid_rrf.ipynb) | Week 5 lesson. Embeddings as meaning, embedding a corpus in place, an Atlas Vector Search index and `$vectorSearch`, BM25 against vector search on the same query, Retrieval@10 against a hand-built truth set, and hybrid retrieval with RRF. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jordan-low-mit/adelphi-dsc785-text-analytics/blob/main/notebooks/03_vector_search_and_hybrid_rrf.ipynb) |
| [04_analyst_terminal_retrieval_and_rag](notebooks/04_analyst_terminal_retrieval_and_rag.ipynb) | Project 2 template, "The Analyst Intelligence Terminal". Thirteen parts in one build: load and clean LLM-extracted filing analyses, MongoDB indexes and queries, BM25, vector and hybrid search, an embedding bake-off, an investment-theme case study, then RAG with chunking, cited answers, a faithfulness audit and a live Q&A demo that must refuse an out-of-corpus question. Each part pairs working code with concept checks and "Investment Committee" questions on provenance and verification. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jordan-low-mit/adelphi-dsc785-text-analytics/blob/main/notebooks/04_analyst_terminal_retrieval_and_rag.ipynb) |

## How the course is taught

- **Group projects defended live.** Students work in groups of 3 to 5. Project 1 requires a live walkthrough in which the notebook runs cell by cell; in Project 2 working code is given on purpose, and the grade comes from the presentation and the group's ability to explain and defend what the code does and why, framed as a briefing to an investment committee.
- **AI as a junior analyst.** AI tools are expected, but the student is the senior analyst who verifies the output and owns every line. Every submission includes an AI disclosure: the tools used, what for, what the AI got wrong, and what was verified independently.
- **Think before you compute.** Project 1 asks for written hypotheses and predictions before the code is run, and the Project 2 bake-off requires the evaluation standard to be set before the experiments.
- **Real data and real infrastructure.** Students scrape live holdings files, read primary-source 10-K filings, and stand up and own their own MongoDB Atlas cluster.

## Data

- **01:** the iShares Core S&P 500 ETF (IVV) holdings file, which students download from ishares.com, and SEC EDGAR data retrieved through `edgartools`. Both are public.
- **02:** the SPDR product list and daily holdings files from ssga.com and the ETF list on stockanalysis.com, all downloaded by the notebook. Outputs that listed individual holdings were cleared.
- **03 and 04:** a course corpus of company analyses that an LLM extracted from SEC 10-K and 10-Q filings, one JSON document per company. It was shared privately with the class and is **not included** here. Each document holds `ticker`, `executive_summary`, `analyst_notes`, `key_metrics` (revenue, net income, diluted EPS, operating margin, free cash flow and total debt, with values and units stored as strings), `mda_deep_dive`, `risk_factor_changes`, a `swot` assessment, a `bull_bear_scorecard`, catalysts, `red_flags` with a severity, and `provenance` (the source filings and their dates). To follow along, build a similar collection from your own filings or summaries.

The connection strings in the notebooks are placeholders; use your own MongoDB Atlas cluster.

## Instructor

[Jordan Low](https://github.com/jordan-low-mit), adjunct professor at Adelphi University.

---

Materials © Jordan Low. Shared for reference; please ask before reusing in a course.
