# Islamabad plot prices (Zameen.com listings)

Raw scrape of plot-for-sale listings in Islamabad from Zameen.com.
Source: https://www.kaggle.com/datasets/saroshkhann/islamabad-plots-prices-dataset

Columns in the raw file: title, price (text, lakh/crore), location, area (marla/kanal), link, page_scraped.

## The main thing to know

The raw file has 18,700 rows but only 25 distinct listings. The same 25 listings are repeated on every one of 748 scraped pages, so 18,675 rows (99.87%) are repeats. The analysis is therefore a description of 25 adverts, not of the Islamabad market. Prices are asking prices from listings, not transaction prices.

## Headline numbers (25 distinct listings)

- Asking price per marla: 3.2 to 76.25 lakh PKR, median 16.51, mean 22.89
- Asking price: 32 lakh to 15.25 crore, median 2.1 crore; 18 of 25 ask one crore or more
- 17 localities after standardising 22 raw location strings; 12 of them have a single listing
- Median price per marla by group: lettered sectors 22.94 lakh (n=10), DHA Defence 19.38 (n=4), other societies 12.40 (n=11)
- Rank correlation of area with total price 0.58, with price per marla 0.06

## Highest / lowest / most

- Highest asking price and highest per marla: D-12, 15.25 crore for a 1 kanal corner plot (76.25 lakh per marla)
- Second highest per marla: F-11, 7 crore for 9.3 marla (75.27 lakh)
- Then Margalla Enclave (49.00 lakh) and E-12 (47.73 lakh)
- Lowest asking price: 32 lakh, shared by three listings (C-15, PECHS, AWT)
- Lowest per marla: AWT, 32 lakh for 10 marla (3.2 lakh per marla)
- 1 kanal plots range from 1.3 crore (Faisal Hills) to 15.25 crore (D-12), an 11.7x gap
- The four DHA Defence plots are all 1 kanal and range from 1.8 crore (Phase 6) to 7.25 crore (Phase 2 corner)
- Smallest plot: 4.4 marla in E-12, asking 2.1 crore
- Most common size: 1 kanal (12 of 25), then 5 marla (5)
- Most listings in one locality: DHA Defence (4), then Faisal Hills (3)
- Localities with 2+ listings, median lakh per marla: I-12 29.06, DHA Defence 19.38, Gulberg Residencia 16.76, C-16 14.25, Faisal Hills 9.82

## Caveats

- 25 listings only. No location ranking is reliable; the 2+ listings table is indicative at best.
- Asking prices, not sale prices.
- No date in the data, so the scrape period is unknown and there are no trends.
- The 25 are what appeared on one results page, so not a random sample. Why the scrape repeated is not documented.
- Some listings are not like-for-like and are flagged, not removed: a pair of plots in Park Enclave listed as 1 kanal (unclear whether the price covers one or both), a plot file (C-15), a commercial plot (Sky Gardens), one mentioning instalments (Margalla Enclave), one titled as a residence (D-18).
- D-12 and F-11 are outliers on price per marla by the 1.5 x IQR rule. They were kept; medians are used.
- Marla taken as 225 sq ft and 1 kanal as 20 marla. This fits the six titles that quote dimensions (one of them, in I-12, lists 5 marla where the dimensions give 5.6).
- "Lettered sector" is just a name pattern (E-12, F-11 ...) and says nothing about the developer.

## Folder layout

    islamabad_raw.csv                 original file, untouched
    islamabad_plots_cleaned.csv       25 rows, one per listing, parsed prices/areas, locality, flags
    islamabad_plots_analysis.ipynb    the analysis, saved with outputs
    islamabad_plots_report.pdf        4-page written report
    README.md
    charts/                           PNG charts written by the notebook

## How to run

From this folder, with the shared environment:

    ../.venv/bin/python -c "import nbformat; from nbclient import NotebookClient; nb = nbformat.read('islamabad_plots_analysis.ipynb', 4); NotebookClient(nb, kernel_name='python3').execute(); nbformat.write(nb, 'islamabad_plots_analysis.ipynb')"

or open the notebook in Jupyter / VS Code and run all cells. It needs pandas, numpy and matplotlib, reads `islamabad_raw.csv` and rewrites the cleaned CSV and the charts.
