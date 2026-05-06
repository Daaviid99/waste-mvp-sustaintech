# MVP dataset pipeline - Data Engineering & Science

> The leading intelligence platform for industrial waste flows and valorisation 
> routes in Iberia, starting with the agri-food sector.

---

## What is this?

A data product that answers one question exceptionally well:

**"Where are industrial waste flows located, in what volume, and what is 
the best valorisation route for each of them?"**

Built for waste managers, valorisation plant developers, and sustainability 
consultants who need reliable, structured, and actionable data — not 
fragmented spreadsheets or outdated public registries.

---

## The problem we solve

Industrial waste data in Europe is:
- Scattered across 27 national registries, regional systems, and corporate reports
- Aggregated at sector level — rarely traceable to individual installations
- Unavailable as structured data for machine consumption
- Disconnected from valorisation capacity and market prices

This means that decisions worth millions (plant locations, feedstock contracts, 
circular economy strategies) are taken with incomplete information.

We fix that.

---

## Product vision

A SaaS data platform providing:

- **Waste flow intelligence**: who generates what, where, in what volume
- **Valorisation routes**: technically viable routes per waste type (biogas, 
  composting, animal feed, chemical extraction, biomass...)
- **Market prices**: secondary raw material prices by waste type and region
- **Valorisation capacity**: existing and planned treatment facilities and their 
  feedstock requirements
- **API access**: for waste managers and technology developers to integrate 
  data into their own systems

---

## MVP scope (Phase 1)

| Dimension       | Scope                                              |
|-----------------|----------------------------------------------------|
| Geography       | Spain + Portugal                                   |
| Sector          | Agri-food (olive, wine, dairy, meat, horticultural)|
| Waste types     | Non-hazardous organic valorisable waste            |
| Key residues    | Alperujo, olive stone, grape marc, whey, meat processing waste |
| Target clients  | Waste managers, valorisation plant developers      |

---

## Data sources

### Tier 1 — Pan-European, open
- **E-PRTR / Industrial Reporting (EEA)**: IPPC installations with name, 
  coordinates, NACE code and annual waste transfers
- **Eurostat** (env_wasgen, env_wastrt): aggregated generation and treatment 
  data by sector and NUTS region

### Tier 2 — Spain, public, dispersed
- **PRTR-España**: Spanish E-PRTR with slightly higher granularity
- **CCAA waste manager registries**: 17 sources, heterogeneous formats
- **SIRA Andalucía**: waste production data with installation-level detail
- **MITECO open data**: treatment plant catalogues
- **MAPA / IFAPA / INE**: agri-food sector censuses and production statistics

### Tier 3 — Portugal
- **APA — SILiAmb / SIRER**: producer and manager declarations
- **INE Portugal**: agri-food sector statistics

### Tier 4 — Sector-specific
- **AICA**: olive oil production by mill and campaign (key for alperujo estimation)
- **OIVE, INLAC, INTERPORC, FIAB**: sector interprofessional statistics

### Tier 5 — Corporate reports (LLM extraction)
- **EINF / CSRD reports**: structured waste data extracted from PDF corporate 
  disclosures using LLM pipelines
- **GRI / CDP databases**: voluntary sustainability disclosures

---

## Technical stack

| Layer            | Technology                                      |
|------------------|-------------------------------------------------|
| Database         | PostgreSQL + PostGIS                            |
| Transformations  | dbt-core                                        |
| Orchestration    | Dagster                                         |
| Data quality     | Great Expectations                              |
| Entity resolution| Splink                                          |
| LLM extraction   | Anthropic Claude (Sonnet) via API               |
| Backend API      | FastAPI + PostgREST                             |
| Frontend         | Next.js + Tremor + MapLibre                     |
| Infrastructure   | Hetzner + Supabase                              |
| Version control  | Git + GitHub + DVC (data versioning)            |

---

## Repository structure
waste-mvp-sustaintech/
│
├── data/
│   ├── raw/          # Never committed — see .gitignore
│   ├── processed/    # Never committed — see .gitignore
│   └── external/     # Never committed — see .gitignore
│
├── notebooks/        # Exploration and analysis
├── src/
│   ├── ingestion/    # Source-specific ingestion pipelines
│   ├── processing/   # Transformations and entity resolution
│   └── utils/        # Shared utilities
│
├── tests/            # Automated tests
├── docs/             # Project documentation
├── environment.yml   # Conda environment definition
├── .env.example      # Environment variable template (no real values)
└── README.md

---

## Local setup

### Prerequisites
- [Miniconda](https://docs.conda.io/en/latest/miniconda.html)
- Git (configured with `core.autocrlf=input` on Mac, `core.autocrlf=true` on Windows)

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/Daaviid99/waste-mvp-sustaintech.git
cd waste-mvp-sustaintech

# 2. Create and activate the conda environment
conda env create -f environment.yml
conda activate waste-mvp

# 3. Copy the environment variables template
cp .env.example .env
# Edit .env with your local values — never commit this file
```

### Daily workflow

```bash
# Always pull before starting work
git pull origin main

# Always push when finishing
git add .
git commit -m "type: description"
git push origin main
```

### Commit convention

| Prefix    | Use for                              |
|-----------|--------------------------------------|
| `feat:`   | New functionality                    |
| `fix:`    | Bug fix                              |
| `chore:`  | Config, dependencies, maintenance    |
| `docs:`   | Documentation only                   |
| `data:`   | Data pipeline or source changes      |

---

## Multi-machine setup (Mac + Windows)

This project is actively developed on both macOS and Windows.  
Line ending normalisation is handled automatically via `.gitattributes`.

**On Windows** (run once):
```bash
git config --global core.autocrlf true
```

**On Mac** (run once):
```bash
git config --global core.autocrlf input
```

---

## Environment variables

Copy `.env.example` to `.env` and fill in your values.  
**Never commit `.env` to the repository.**

---

## Roadmap

- [ ] Phase 1 — Iberian agri-food waste dataset MVP
- [ ] Phase 2 — Valorisation routes and market prices layer
- [ ] Phase 3 — API v1 with authentication and billing
- [ ] Phase 4 — Dashboard and map interface
- [ ] Phase 5 — Expansion to construction, WEEE, and hazardous waste
- [ ] Phase 6 — Pan-European coverage

---

## Team

Built by a team combining sustainability consulting expertise and data 
science / machine learning capabilities.

---

## Licence

Private — all rights reserved. Not for redistribution.