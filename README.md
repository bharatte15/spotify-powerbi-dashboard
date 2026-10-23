# 🎧 Spotify Dashboard | Power BI

!\[Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi\&logoColor=black)
!\[DAX](https://img.shields.io/badge/DAX-Measures-0078D4)
!\[Power Query](https://img.shields.io/badge/Power%20Query-ETL-217346)
!\[Domain](https://img.shields.io/badge/Domain-Music%20Streaming-1DB954?logo=spotify\&logoColor=white)
!\[Tracks](https://img.shields.io/badge/Tracks%20Analyzed-953-1DB954)

An interactive, single-page Power BI dashboard that turns Spotify's top streamed songs into clear, explorable insights: which tracks and artists lead, how stream counts compare, how releases trend over time, and what the audio profile of each artist looks like.

!\[Dashboard Preview](assets/dashboard-preview.png)

<!-- Add a screenshot of the report at assets/dashboard-preview.png -->

\---

## 📌 Table of Contents

* [Overview](#-overview)
* [Dataset at a Glance](#-dataset-at-a-glance)
* [Dashboard Features](#-dashboard-features)
* [Data Model and Measures](#-data-model-and-measures)
* [Tech Stack](#-tech-stack)
* [Data Preparation and Quality Notes](#-data-preparation-and-quality-notes)
* [Getting Started](#-getting-started)
* [Business Questions Answered](#-business-questions-answered)
* [Project Structure](#-project-structure)
* [Future Enhancements](#-future-enhancements)
* [Author](#-author)

\---

## 🔍 Overview

Streaming platforms generate enormous volumes of data, but raw tables do not show what is trending or why. This project builds a polished Power BI report on top of a dataset of top streamed Spotify songs so that anyone can explore tracks, artists, stream counts and release trends through slicers and cross-filtering, with no queries required.

\---

## 📂 Dataset at a Glance

|Item|Detail|
|-|-|
|**File**|`spotify\_streaming.xlsx` (sheets: `Spotify Dataset`, `Data Dictionary`)|
|**Records**|953 tracks|
|**Fields**|25 columns|
|**Release years covered**|1930 to 2023 (most tracks released 2021 to 2023)|
|**Total streams**|about 489 billion across the dataset|
|**Source**|Most Streamed Spotify Songs 2023 dataset (Kaggle) `\[add link]`|

**Field groups**

* **Track details:** `track\_name`, `artist(s)\_name`, `artist\_count`, `released\_year`, `released\_month`, `released\_day`, `cover\_url`
* **Streaming and reach:** `streams`, `in\_spotify\_playlists`, `in\_spotify\_charts`
* **Cross-platform presence:** `in\_apple\_playlists`, `in\_apple\_charts`, `in\_deezer\_playlists`, `in\_deezer\_charts`, `in\_shazam\_charts`
* **Audio features:** `bpm`, `key`, `mode`, `danceability\_%`, `valence\_%`, `energy\_%`, `acousticness\_%`, `instrumentalness\_%`, `liveness\_%`, `speechiness\_%`

A full field list is also included in the `Data Dictionary` sheet.

\---

## ✨ Dashboard Features

The report is a single 1280 x 720 page with a banner title and the following components:

|Component|What it shows|
|-|-|
|**Total streams by track** (clustered bar)|Ranked view of the most streamed songs|
|**Streams by artist** (pie chart)|Each artist's share of total streams|
|**Tracks over time** (line chart)|Number of tracks across release dates, to spot temporal patterns|
|**Artist audio profile** (table)|Danceability, energy, acousticness, liveness and valence by artist|
|**KPI cards**|Total track count and the highest stream count (`Max\_Streams`)|
|**Summary card**|Highest streams, track name and contributing artist count together|
|**Most Streamed Track** (HTML content visual)|Album cover of the top track, rendered from the `cover\_url` data|
|**Slicers**|Filter by **Artist**, **Track**, **Date** and **Year**|

All visuals are cross-filtered: select a track, artist or year and the whole page updates.

### Highlights from the data

These figures come straight from the dataset:

* **Most streamed track:** *Blinding Lights* with about 3.70 billion streams, followed by *Shape of You* (about 3.56 billion) and *Someone You Loved* (about 2.89 billion).
* **Top artists by total streams (by credited artist name):** The Weeknd (about 14.2 billion), Taylor Swift (about 14.1 billion) and Ed Sheeran (about 13.9 billion).
* **Release timing:** 2022 has the most tracks in the dataset (402), ahead of 2023 (175) and 2021 (119).

\---

## 🧮 Data Model and Measures

* **Table:** `Spotify Dataset` (single fact table)
* **Calculated fields:** `Date` (built from the release year, month and day), `Year`
* **DAX measures:**

  * `Max\_Streams`: highest stream count in the current filter context
  * `Image HTML`: builds the HTML used to display the track's album cover in the HTML content visual
* **Aggregations used in visuals:** sum of streams, count of tracks, sum of artist count, and audio-feature fields by artist

\---

## 🛠 Tech Stack

|Layer|Tool|
|-|-|
|Reporting and visualization|Power BI Desktop|
|Data transformation|Power Query (M)|
|Calculations|DAX|
|Custom visual|HTML Content visual (for album cover display)|
|Data source|Excel workbook (`.xlsx`)|

\---

## 🧹 Data Preparation and Quality Notes

Cleaning is done in Power Query before the data reaches the report. Points worth knowing about the source data:

* **`streams` is stored as text** in the source file and must be converted to a numeric type before aggregating.
* **One malformed record:** the row for *Love Grows (Where My Rosemary Goes)* has audio-feature text pasted into the `streams` field instead of a number, so it needs to be corrected or excluded.
* **Missing values:** `in\_shazam\_charts` has 50 blanks and `key` has 95 blanks.
* **Missing cover art:** 225 tracks have `cover\_url` set to `Not Found`, so the HTML cover visual will not render an image for them.
* **Possible duplicates:** 4 repeated track and artist combinations.
* **Derived fields:** `Date` and `Year` are created from the release year, month and day columns for time-based analysis.

\---

## 🚀 Getting Started

### Prerequisites

* [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (latest version recommended)
* `spotify\_streaming.xlsx` (included in this repository)

### Run the Dashboard

1. **Clone the repository**

```bash
   git clone https://github.com/bharatte15/<repository-name>.git
   cd <repository-name>
   ```

2. **Open the report**
Open `Spotify\_Dashboard.pbix` in Power BI Desktop.
3. **Point to your data**
Go to **Transform data → Data source settings** and update the path to the location of `spotify\_streaming.xlsx` on your machine.
4. **Refresh**
Click **Refresh** to load the data into the model.
5. **Explore**
Use the slicers and click any visual to filter the page.

> The HTML content visual may prompt you to allow custom visuals the first time you open the report.

\---

## ❓ Business Questions Answered

* Which tracks have the highest stream counts?
* Which artists capture the largest share of total streams?
* How does release activity change across years and dates?
* How do artists differ in danceability, energy, acousticness, liveness and valence?
* What does the profile of the single most streamed track look like?

\---

## 🗂 Project Structure

```
├── assets/
│   └── dashboard-preview.png     # Dashboard screenshot
├── data/
│   └── spotify\_streaming.xlsx    # Source dataset (Spotify Dataset + Data Dictionary)
├── Spotify\_Dashboard.pbix        # Power BI report
└── README.md
```

\---

## 🔮 Future Enhancements

* Add playlist and chart-presence analysis across Spotify, Apple and Deezer.
* Add a drill-through page for individual artists and tracks.
* Add audio-feature analysis (BPM, key and mode) alongside stream counts.
* Add bookmarks for guided navigation and a mobile layout.
* Publish to Power BI Service with scheduled refresh.

\---

⭐ If you found this project useful, consider giving it a star.

