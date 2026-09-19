# GDELT Research: News & Event Data Exploration for Disaster Research

> **Hands-on exploration of GDELT for extracting, structuring, filtering, and analysing global news and event data for disaster-related research.**

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)](https://pandas.pydata.org/)
[![GDELT](https://img.shields.io/badge/Data-GDELT-orange)](https://www.gdeltproject.org/)
[![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)](https://jupyter.org/)

---

## Overview

This repository documents a practical exploration of **GDELT (Global Database of Events, Language, and Tone)** as a potential data source for disaster-related research.

The exploration focuses on understanding how large-scale global news and event data can be accessed, structured, filtered, and interpreted using Python.

Rather than building a complete disaster prediction system, this project focuses on **research-oriented data exploration and methodology**.

The work investigates:

* GDELT data structure and components
* Programmatic API access
* Downloadable event datasets
* Geographic and temporal information
* Event and actor metadata
* News-source relationships
* Disaster-related candidate identification
* Article-level deduplication
* Media-tone analysis
* Practical data-access limitations

---

## Research Context

This project is part of a broader exploration of **multimodal data sources for disaster research**.

The long-term research direction is to investigate how different data modalities can provide complementary information about disaster events:

```text
                 Multimodal Disaster Research
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       GDELT            Bluesky         Sentinel / GEE
          │                │                │
     News & Events     Social Signals   Satellite Data
          │                │                │
          └────────────────┼────────────────┘
                           │
                  Multimodal Analysis
```

Within this framework, GDELT represents the **news and event-data modality**.

---

## Objectives

The primary objectives of this exploration were to:

1. Understand the GDELT ecosystem and its major data components.
2. Explore programmatic access to GDELT data.
3. Work with a real downloadable GDELT Event dataset.
4. Understand the structure and meaning of important event fields.
5. Extract India-associated records.
6. Identify disaster-related candidate records.
7. Investigate the relationship between event records and source articles.
8. Perform article-level deduplication.
9. Analyse basic event-coverage and media-tone statistics.
10. Document practical limitations relevant to future research.

---

## Dataset Explored

The primary dataset explored in this repository is a downloadable **GDELT Events export**:

```text
20260917.export.CSV.zip
```

### Dataset dimensions

| Property              |             Value |
| --------------------- | ----------------: |
| Records               |           116,212 |
| Columns               |                58 |
| Format                | Tab-separated CSV |
| Archive               |               ZIP |
| Primary analysis tool |            Pandas |

The dataset was loaded directly from the ZIP archive using Python without manually extracting the file.

> **Note:** The dataset is an event-level dataset. It should not be interpreted as a one-row-per-news-article dataset.

---

## Technologies Used

### Programming & Analysis

* **Python**
* **Pandas**
* **Jupyter Notebook**

### Data Source

* **GDELT Events**
* GDELT DOC 2.0 API explored for programmatic news retrieval

### Research Techniques

* Data loading and inspection
* Schema exploration
* Filtering
* Geographic association
* Keyword-based candidate generation
* Deduplication
* Descriptive statistics
* Limitation analysis

---

## Repository Structure

```text
GDELT-Research/
│
├── notebooks/
│   └── gdelt_exploration.ipynb
│
├── notes/
│   └── gdelt_notes.md
│
├── data/
│   └── 20260917.export.CSV.zip
│
├── .gitignore
├── README.md
└── requirements.txt
```

### Directory Description

| Directory/File     | Purpose                                       |
| ------------------ | --------------------------------------------- |
| `notebooks/`       | Hands-on GDELT experiments and analysis       |
| `notes/`           | Research notes and conceptual understanding   |
| `data/`            | Downloaded GDELT dataset used for exploration |
| `README.md`        | Project documentation                         |
| `requirements.txt` | Python dependencies                           |

---

## Key GDELT Fields Explored

The Event dataset contains 58 fields. Some of the most relevant fields explored include:

| Field                | Description                             |
| -------------------- | --------------------------------------- |
| `GLOBALEVENTID`      | Event record identifier                 |
| `SQLDATE`            | Event date                              |
| `Actor1Name`         | First actor                             |
| `Actor2Name`         | Second actor                            |
| `Actor1CountryCode`  | Country associated with Actor 1         |
| `Actor2CountryCode`  | Country associated with Actor 2         |
| `EventCode`          | CAMEO event code                        |
| `EventRootCode`      | Higher-level event category             |
| `QuadClass`          | Broad event classification              |
| `GoldsteinScale`     | Event impact/cooperation-conflict scale |
| `NumMentions`        | Number of mentions                      |
| `NumSources`         | Number of sources                       |
| `NumArticles`        | Number of associated articles           |
| `AvgTone`            | Average media tone                      |
| `ActionGeo_FullName` | Action/event geographic location        |
| `ActionGeo_Lat`      | Action latitude                         |
| `ActionGeo_Long`     | Action longitude                        |
| `SOURCEURL`          | Source article URL                      |

---

## Exploration Workflow

The practical workflow followed in the notebook was:

```text
GDELT API Exploration
        │
        ▼
HTTP 429 Rate-Limit Observation
        │
        ▼
Downloadable GDELT Event Dataset
        │
        ▼
Load 116,212 Records
        │
        ▼
Assign Official Column Names
        │
        ▼
Explore Temporal & Event Structure
        │
        ▼
Identify India-Associated Records
        │
        ▼
Generate Flood-Related Candidates
        │
        ▼
34 Event Records
        │
        ▼
Deduplicate by SOURCEURL
        │
        ▼
8 Unique Source Articles
        │
        ▼
Geographic / Keyword Refinement
        │
        ▼
2 Potential India-Focused Flood Articles
        │
        ▼
Descriptive Analysis & Limitation Assessment
```

---

## Key Findings

### 1. Large-scale event data

The explored GDELT Event export contained:

**116,212 event records across 58 fields.**

This provided hands-on experience with a large structured news-event dataset rather than a small sample dataset.

### 2. Geographic filtering

An India-associated subset was created using actor-country and action-geography fields.

```text
India-associated records: 6,952
Percentage of dataset: 5.98%
```

The experiment also demonstrated that **geographic association does not necessarily mean that the event itself occurred in that country**.

An article may involve a country's actors, organizations, or locations while discussing an event elsewhere.

### 3. Event records vs. articles

A flood-related URL filter produced:

```text
34 event records
        ↓
8 unique source articles
```

This demonstrated that a single news article can generate multiple GDELT event records.

Therefore:

> **Event-level records should not automatically be treated as individual news articles.**

Article-level analysis may require deduplication or aggregation using source identifiers such as `SOURCEURL`.

### 4. Disaster candidate filtering

The flood candidate analysis initially identified 8 unique articles.

After a simple geographic/content refinement, 2 potential India-focused flood articles remained.

These were treated as **exploratory candidates**, not as a validated ground-truth disaster dataset.

### 5. Media tone

For the two potential India-focused flood articles:

| Metric           |         Result |
| ---------------- | -------------: |
| Average mentions |              6 |
| Average sources  |              1 |
| Average articles |              6 |
| Average tone     |          -4.79 |
| Tone range       | -5.91 to -3.68 |

The tone values were treated as a media-coverage signal.

They were **not interpreted as a direct measure of disaster severity**.

---

## API Access Experiment

The GDELT DOC 2.0 API was also explored for programmatic retrieval of disaster-related news.

During the experiment, API requests returned:

```text
HTTP 429 — Too Many Requests
```

This provided a practical observation about API rate limiting.

Instead of repeatedly requesting the endpoint, the exploration was redirected toward an official downloadable GDELT Event dataset.

This demonstrated an important research practice:

> **When one access method is constrained, use an alternative supported data-access method rather than fabricating or assuming unavailable results.**

---

## Research Applications

GDELT could contribute to disaster-related research in several ways.

### Disaster Event Monitoring

Identify and analyse news coverage surrounding:

* Floods
* Earthquakes
* Cyclones
* Wildfires
* Droughts
* Landslides

### Temporal Analysis

Study how disaster-related media attention changes over time.

### Geographic Analysis

Analyse geographic associations between events, actors, organizations, and locations.

### Event Analysis

Investigate relationships between actors and event categories.

### Media Analysis

Use media tone and coverage volume as additional signals for studying disaster-related information environments.

### Multimodal Research

GDELT can provide the **news/event modality** alongside other data sources:

```text
GDELT
News & Event Data
       │
       ├──────────────┐
       │              │
Bluesky          Sentinel / GEE
Social Data      Satellite Data
       │              │
       └───────┬──────┘
               │
       Multimodal Dataset
               │
        Disaster Analysis
```

---

## Limitations Identified

This exploration identified several important limitations:

### API Rate Limiting

The DOC API returned HTTP 429 during experimentation.

### Event-Level Representation

Multiple event records may originate from a single news article.

### Lack of Full Article Text

The Event dataset provides structured event metadata and source URLs rather than the complete source article text.

### Keyword Filtering

Searching for terms such as `"flood"` in URLs is useful for candidate generation but is not sufficient for reliable disaster classification.

### Geographic Ambiguity

Country associations may refer to actors, organizations, or locations mentioned in coverage rather than the physical location of the disaster.

### Source Availability

Source URLs may change, become unavailable, or have access restrictions.

### Exploratory Dataset

The flood-related subset generated during this project should not be considered a validated disaster ground-truth dataset.

---

## Research Takeaways

This project provided practical experience with:

* Working with large-scale real-world datasets
* Understanding a complex event-data schema
* Handling compressed data files
* Performing geographic filtering
* Working with event taxonomies
* Generating research candidates from noisy data
* Deduplicating event records at the article level
* Interpreting media metadata
* Identifying false-positive and geographic ambiguity issues
* Documenting API limitations
* Designing a reproducible data-exploration workflow

The exploration reinforced that **data interpretation and validation are as important as data acquisition** in research workflows.

---

## Future Research Direction

The next stage of the broader research project is to explore complementary disaster-data modalities.

Potential sources include:

```text
News / Events
    └── GDELT

Social Signals
    └── Bluesky

Satellite / Geospatial
    └── Google Earth Engine
    └── Sentinel
```

The eventual research direction is to investigate how these heterogeneous sources can be aligned around the same disaster event and used for **multimodal disaster analysis**.

---

## Project Status

**Status:** Completed — Initial GDELT Exploration

The repository currently represents an exploratory research phase rather than a production-ready disaster-analysis system.

### Completed

* [x] GDELT ecosystem exploration
* [x] DOC API experimentation
* [x] API rate-limit observation
* [x] Downloaded Event dataset
* [x] Loaded and structured 116,212 records
* [x] Explored event schema
* [x] Analysed temporal information
* [x] Analysed geographic associations
* [x] Generated flood-related candidates
* [x] Deduplicated source articles
* [x] Performed exploratory statistics
* [x] Documented limitations
* [x] Identified multimodal research relevance

---

## Author

**Sumaira K**

B.Tech — Computer Science Engineering / AI & Data Science

---

## References

* **GDELT Project:** https://www.gdeltproject.org/
* **GDELT Documentation:** https://www.gdeltproject.org/

---

## Disclaimer

This repository documents an exploratory research exercise using GDELT data.

The analyses presented here are intended to demonstrate **data acquisition, exploration, methodology, and research potential**. The disaster-related filtering performed in the notebook is exploratory and should not be interpreted as a validated disaster detection or classification system.
