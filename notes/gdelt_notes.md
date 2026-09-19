# GDELT Research Notes

## 1. What is GDELT?

GDELT (Global Database of Events, Language, and Tone) is a large-scale open data project that monitors news and media sources from around the world.

It converts information from news coverage into structured data that can be used for analysis of events, actors, locations, themes, and media tone.

For disaster-related research, GDELT can provide a useful **news and event-data modality** that can complement social-media and satellite-based data.

---

## 2. What datasets/components does GDELT provide?

GDELT provides several major data components, including:

* **GDELT Events** — structured records of events extracted from global news coverage.
* **GDELT Global Knowledge Graph (GKG)** — document-level information including themes, entities, locations, organizations, and tone.
* **GDELT DOC 2.0 API** — search and retrieval interface for news coverage.
* **GDELT GEO** — geographic analysis and visualization of news-related information.
* **GDELT analysis and downloadable datasets** — datasets that can be processed locally or through other data-access methods.

The main component explored in this project was the **GDELT Events dataset**.

---

## 3. Dataset explored

The dataset explored was a downloadable GDELT Events export:

`20260917.export.CSV.zip`

The file was loaded directly from the ZIP archive using Python and pandas without manually extracting it.

Dataset dimensions:

* **Rows:** 116,212
* **Columns:** 58

The dataset was dominated by records associated with 17 September 2026, although a small number of records had different event dates.

The complete exploration is documented in:

`notebooks/gdelt_exploration.ipynb`

---

## 4. How is the data accessed?

GDELT data can be accessed through multiple approaches:

### API access

The GDELT DOC 2.0 API can be used to search news coverage programmatically.

During experimentation, requests to the DOC API returned:

`HTTP 429 — Too Many Requests`

This demonstrated the importance of respecting API rate limits.

### Downloadable datasets

A practical alternative is to download GDELT datasets directly and process them locally.

For this project, the downloadable Event dataset was used successfully.

### Other access methods

GDELT datasets can also be accessed through other large-scale data-analysis infrastructure, depending on the dataset and research requirement.

---

## 5. Data format

The explored Event dataset is provided as a tab-separated CSV file inside a ZIP archive.

The file initially contains 58 unnamed columns. Official GDELT field names were assigned to the columns before analysis.

The dataset was loaded using:

* Python
* pandas
* ZIP/CSV handling

The data can then be filtered, grouped, aggregated, and analyzed using standard data-analysis techniques.

---

## 6. Important fields

Some important fields explored in the Event dataset include:

| Field                | Purpose                                        |
| -------------------- | ---------------------------------------------- |
| `GLOBALEVENTID`      | Unique identifier for an event record          |
| `SQLDATE`            | Date associated with the event                 |
| `Actor1Name`         | Name of the first actor                        |
| `Actor2Name`         | Name of the second actor                       |
| `Actor1CountryCode`  | Country associated with Actor 1                |
| `Actor2CountryCode`  | Country associated with Actor 2                |
| `EventCode`          | CAMEO event code                               |
| `EventRootCode`      | Higher-level CAMEO event category              |
| `QuadClass`          | Broad event classification                     |
| `GoldsteinScale`     | Conflict/cooperation impact scale              |
| `NumMentions`        | Number of mentions associated with the event   |
| `NumSources`         | Number of sources associated with the event    |
| `NumArticles`        | Number of articles associated with the event   |
| `AvgTone`            | Average tone associated with the event         |
| `ActionGeo_FullName` | Geographic location associated with the action |
| `ActionGeo_Lat`      | Action latitude                                |
| `ActionGeo_Long`     | Action longitude                               |
| `SOURCEURL`          | Source article URL                             |

These fields make it possible to study relationships between events, actors, geography, media coverage, and tone.

---

## 7. Geographic information

The Event dataset contains geographic information for actors and event actions.

Important geographic fields include:

* `Actor1Geo_FullName`
* `Actor1Geo_CountryCode`
* `Actor1Geo_Lat`
* `Actor1Geo_Long`
* `Actor2Geo_FullName`
* `Actor2Geo_CountryCode`
* `ActionGeo_FullName`
* `ActionGeo_CountryCode`
* `ActionGeo_Lat`
* `ActionGeo_Long`

For the experiment, an India-associated subset was created using:

* `ActionGeo_CountryCode == "IN"`
* `Actor1CountryCode == "IND"`
* `Actor2CountryCode == "IND"`

This produced **6,952 India-associated event records**, representing approximately **5.98%** of the explored dataset.

It is important to note that an India-associated record does not necessarily mean that the disaster itself occurred in India. The association may come from an actor, location, or other event relationship.

---

## 8. Temporal information

The dataset contains several temporal fields, including:

* `SQLDATE`
* `MonthYear`
* `Year`
* `FractionDate`
* `DATEADDED`

The explored dataset had:

* Minimum `SQLDATE`: `20160919`
* Maximum `SQLDATE`: `20260917`

The majority of records were associated with 2026, particularly 17 September 2026.

This temporal structure can support research involving:

* Event frequency over time
* Disaster-related news trends
* Changes in media attention
* Event timelines
* Comparison between different periods

---

## 9. Text/news information

The GDELT Event dataset does **not** contain the complete text of the source news article.

Instead, it provides structured event information extracted from news coverage and a `SOURCEURL` that points to the underlying source article.

This distinction is important.

During the experiment, flood-related candidates were identified by searching for the keyword `"flood"` in source URLs.

The process produced:

* **34 flood-related event records**
* **8 unique source articles**

This showed that multiple event records can originate from the same news article.

After removing candidates whose URLs explicitly referenced Nepal, **2 potential India-focused flood articles** remained.

The two articles were treated as exploratory candidates rather than as a validated disaster dataset.

Therefore, URL keyword filtering should not be considered a reliable disaster-classification method by itself.

For research requiring richer textual information, GDELT's other components, particularly document/knowledge-graph data, may be more appropriate.

---

## 10. Potential research applications

GDELT can be useful for several disaster-related research tasks.

### Disaster event monitoring

Identify and analyse news coverage associated with disasters such as:

* Floods
* Earthquakes
* Cyclones
* Wildfires
* Droughts
* Landslides

### Geographic analysis

Study where disaster-related events and media coverage are geographically associated.

### Temporal analysis

Measure changes in disaster-related media attention over time.

### Event and actor analysis

Analyse organizations, governments, communities, and other actors appearing in disaster-related events.

### Media-tone analysis

Use `AvgTone` as one signal for analysing the tone of media coverage.

### Multimodal disaster research

GDELT can serve as the **news/text modality** in a multimodal disaster-analysis system.

For example:

**GDELT → News/Event Signals**

**Bluesky → Social-Media Signals**

**Sentinel/GEE → Satellite/Geospatial Signals**

These complementary sources could potentially be combined to study disaster events from different perspectives.

---

## 11. Limitations

Several limitations were observed during the exploration:

1. **API rate limiting**
   The DOC API returned HTTP 429 during experimentation.

2. **Event records are not equivalent to articles**
   A single article can generate multiple event records.

3. **The Event dataset does not contain full article text**
   `SOURCEURL` provides a connection to the original source.

4. **Simple keyword filtering can produce false positives**
   Searching for `"flood"` in URLs does not guarantee that the article describes a flood occurring in the target region.

5. **Geographic association requires careful interpretation**
   An India-associated event may concern another country while involving Indian actors, locations, or organizations.

6. **Source availability can vary**
   Original news URLs may change, become unavailable, or have access restrictions.

7. **The explored sample is not a validated disaster ground-truth dataset**
   Further research would require stronger disaster-event identification and validation methods.

---

## 12. My conclusion

The practical exploration demonstrated that GDELT can provide large-scale structured news and event data for research.

The downloadable Event dataset was successfully loaded and analysed using Python and pandas. The experiment also demonstrated an important characteristic of GDELT: event-level records should not automatically be interpreted as individual news articles.

The disaster exploration showed that geographic filtering and keyword-based candidate generation can be useful for initial investigation, but additional validation is necessary for reliable disaster classification.

The most important research value identified for this project is GDELT's potential role as a **news/event modality** within a larger multimodal disaster-analysis framework.

The hands-on exploration also highlighted practical considerations such as API rate limiting, dataset structure, article deduplication, geographic ambiguity, and the distinction between structured event metadata and full article text.
