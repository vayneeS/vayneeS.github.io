---
layout: single
title: "Movie database - IMDb Data Engineering & Analytics (ongoing project)"
excerpt: "A full data pipeline from raw IMDb files to an interactive graph exploration app."
header:
  teaser: /assets/images/marvel_teaser.jpg
  overlay_color: "#dde3ea"
toc: true
toc_label: "Contents"
---

<p class="notice--info">
  <strong>Stack:</strong> Python · MySQL · Docker · Neo4j · Streamlit · SQL
</p>


[View Code](https://github.com/vayneeS/MoviesDB)

---
## Overview

This project is a collaborative work with [Tarik Anouar](https://fr.linkedin.com/in/anouartarik), a data analyst, mentor, and educator. This project explores how raw public data can be transformed into a structured analytical resource using modern data engineering practices. Using the IMDb open datasets as a source, I built an end-to-end data pipeline that ingests, cleans, and loads the data into a relational database designed for efficient querying. The curated dataset is then exposed through an interactive graph interface, enabling exploration of relationships between movies, actors, and characters.

The pipeline runs end-to-end: raw TSV files → relational database → graph database → Streamlit UI.

**Primary objectives:**
- Data prep & ingestion: 
  - Ingest and structure the IMDb dataset into a relational MySQL database
- SQL queries 
  - Write SQL queries to extract and transform subsets of interest; which is Marvel films released from 2008 till today.
- No-Code database: 
  - Import structured data into Neo4j to leverage graph queries for relationship exploration
- Visualization: 
  - Build a Streamlit app for interactive visualization of Marvel movie , actor and director relationships
- Testing and automation: 
  - Experiment with different frameworks to benchmark performance
  - Develop CI/CD pipelines to test and deploy code after testing
---

## Architecture

| Stage | Tool | 
|---|---|
| Ingestion & storage | MySQL + Docker | 
| Extraction & transformation | SQL | 
| Relationship modeling | Neo4j Aura | 
| Interactive front end | Streamlit |

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

## Future Improvements

- **Marvel title extraction** - scrape the Marvel wiki to build a complete title list and join with the Movies table for precise franchise filtering

- **dbt integration** - separate SQL transformation logic from infrastructure, benchmark performance