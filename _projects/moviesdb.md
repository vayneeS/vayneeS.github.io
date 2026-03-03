---
layout: single
title: "MoviesDB - IMDb Data Engineering & Analytics"
excerpt: "A full data pipeline from raw IMDb files to an interactive graph exploration app."
header:
  overlay_color: "#1a4a3a"
  overlay_filter: 0.6
toc: true
toc_label: "Contents"
---

<p class="notice--info">
  <strong>Stack:</strong> Python · MySQL · Docker · Neo4j · Streamlit · SQL
</p>

## Overview

MoviesDB transforms raw IMDb data into a clean, queryable database exposed through an interactive graph exploration interface.

The pipeline runs end-to-end: raw TSV files → relational database → graph database → Streamlit UI.

**Primary objectives:**
- Ingest and structure the IMDb dataset into a relational MySQL database
- Write SQL queries to extract and transform subsets of interest (e.g., Marvel films)
- Import structured data into Neo4j to leverage graph queries for relationship exploration
- Build a Streamlit app for interactive visualization of movie-people relationships

---

## Architecture

| Stage | Tool | Rationale |
|---|---|---|
| Ingestion & storage | MySQL + Docker | Normalization, integrity constraints, efficient joins |
| Extraction & transformation | SQL | Structured filtering, aggregation, subset definition |
| Relationship modeling | Neo4j Aura | Multi-hop queries, graph traversal |
| Interactive front end | Streamlit | Lightweight UI, no heavy web overhead |

---

## Data Ingestion & Database Setup

Download IMDb TSV files from the official IMDb dataset page and place them in `data/raw/`.

```bash
# Preprocess raw files
python utils/preprocess.py

# Start MySQL via Docker
docker-compose up -d

# Install dependencies
pip install -r requirements.txt

# Open setup notebook
jupyter notebook notebooks/database_setup.ipynb
```

---

## Database Schema

| Table | Key columns |
|---|---|
| `titles` | `title_id`, `primary_title`, `genres`, `start_year` |
| `names` | `person_id`, `person_name` |
| `principals` | `title_id`, `person_id`, `job`, `category` |
| `ratings` | `title_id`, `average_rating`, `num_votes` |
| `characters` | `character_name`, `person_name`, `person_id` |

---

## SQL Analytics Layer

```sql
SELECT t.primaryTitle, r.averageRating
FROM titles t
JOIN ratings r ON t.tconst = r.tconst
WHERE t.genres LIKE '%Action%'
ORDER BY r.averageRating DESC;
```

The SQL layer handles complex joins, aggregations, franchise filtering, and clean CSV export for Neo4j.

---

## Graph Modeling - Neo4j

**Node and relationship types:**

```
(Movie) -[:ACTED_IN]- (Person)
(Movie) -[:DIRECTED_BY]- (Person)
(Movie) -[:HAS_GENRE]- (Genre)
```

**Import via Cypher:**

```cypher
LOAD CSV WITH HEADERS FROM 'file:///movies.csv' AS row
CREATE (:Movie {id: row.id, title: row.title});
```

Graph databases are suited to exploring multi-hop relationships that would be cumbersome in SQL - for example, finding all actors who worked with a given director across multiple genres.

---

## Streamlit Application

```bash
streamlit run app.py
```

Users can select movies, view connected actors, and explore relationship paths interactively.

---

## Project Structure

```
MoviesDB/
├── docker/
├── docker-compose.yml
├── notebooks/
├── utils/
├── tests/
├── docs/
└── requirements.txt
```

---

## Testing

```bash
pytest
```

Tests cover query correctness, pipeline stability, and schema validation.

---

## Future Improvements

- **dbt integration** - separate SQL transformation logic from infrastructure, benchmark performance
- **Marvel title extraction** - scrape the Marvel wiki to build a complete title list and join with the Movies table for precise franchise filtering