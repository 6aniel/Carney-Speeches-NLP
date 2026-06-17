# Themes in Mark Carney's First Year

This project analyzes official speeches from Prime Minister Mark Carney's first year in office using natural language processing in R.

The goal is to provide a readable recap of the core themes in Carney's public rhetoric so far: what topics appeared most often, how they clustered, and what kind of governing narrative emerged from the speeches.

## Public Report

Start here:

- `carney_first_year_report.qmd` - polished reader-facing Quarto report
- `NLP_draft1.qmd` - technical notebook with scraping and modeling proof-of-work

The public report covers:

- motivation
- data source
- methods
- key visuals
- topic model results
- main findings
- limitations

## Data

The main dataset is `Data/carney_pm_speeches_raw.csv`.

It contains 81 official speeches from the Prime Minister of Canada website, covering June 9, 2025 through June 4, 2026. Each record includes the speech date, title, source URL, source metadata, and scraped speech text.

## Methods

The analysis uses a lightweight text-mining workflow:

1. Scrape official speech pages from the Prime Minister of Canada website.
2. Tokenize speech text into words.
3. Remove common English stop words.
4. Group a small number of related word forms, such as `projects` into `project`.
5. Remove generic high-frequency terms, including `canada` and `build`, because they dominated every topic.
6. Fit a four-topic Latent Dirichlet Allocation model.
7. Label topics based on their highest-probability words.

## Topic Names

The current four suggested topic labels are:

- Housing, Infrastructure, and Economy
- National Security and Sovereignty
- Defence, Trade, and Global Partnerships
- AI, Communities, and Major Projects

These labels are interpretive and should be read as summaries of the model output, not definitive categories.

## Reproducing the Report

Install Quarto and the required R packages:

```r
install.packages(c(
  "tidyverse",
  "tidytext",
  "topicmodels",
  "scales",
  "knitr"
))
```

Render the public report:

```bash
quarto render carney_first_year_report.qmd
```

Render the technical notebook:

```bash
quarto render NLP_draft1.qmd
```

## Repository Structure

```text
.
├── Data/
│   ├── Carney 5 speech sample.csv
│   ├── carney_pm_speeches_raw.csv
│   └── carney_speech_urls.csv
├── NLP_draft1.qmd
├── carney_first_year_report.qmd
├── NLP-Project-1.Rproj
└── README.md
```

## Publishing Notes

For GitHub, this repository can serve two audiences:

- The README explains the project at a high level.
- The Quarto report presents the public-facing analysis.
- The draft notebook preserves the technical trail behind the data collection and modeling.

For a simple public page, render `carney_first_year_report.qmd` to HTML and publish the HTML with GitHub Pages or Quarto Pub.

## Limitations

This analysis only uses official speeches from one source. It does not include interviews, parliamentary debate, social media, press coverage, opposition responses, or policy outcomes. Topic modeling is exploratory, and the selected number of topics affects the results.
