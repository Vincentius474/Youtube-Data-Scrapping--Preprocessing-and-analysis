# YouTube Channel Data Collection & Visualization

A Python data-analysis project that collects publicly displayed video metadata from selected YouTube channels and explores channel performance through visualizations. The notebooks cover the collection workflow and the analysis of exported CSV files, with a focus on video view counts and upload recency.

## Project goals

- Collect video titles, view counts, and upload-time labels from selected YouTube channel video pages.
- Convert abbreviated view counts such as `1.2K` and `3.4M` into numeric values.
- Export collected records to CSV and Excel files.
- Explore video performance using interactive Plotly charts and Matplotlib charts.
- Compare view activity across channels and posting dates.

## Project structure

The notebooks expect exported datasets to be stored in an `Output Files/` directory.

```text
.
├── YouTube_Channels_Data_Collection.ipynb
├── Channels data visualization.ipynb
└── Output Files/
    ├── TheHustlersCornerSA_Podcast.csv
    ├── TheHustlersCornerSA_Podcast.xlsx
    ├── podcastandchillnetwork_Podcast.csv
    ├── kingdavidstudio1_Podcast.csv
    ├── culturespotlight_Podcast.csv
    ├── Majit_AMonday_Podcast.csv
    ├── justifyworldwide_Podcast.csv
    ├── SMWX_Podcast.csv
    └── konvo_za_Podcast.csv
```

The dataset filenames above reflect paths referenced in the visualization notebook; your local folder may contain only the files you have collected so far.

## Notebooks

### 1. `YouTube_Channels_Data_Collection.ipynb`

Uses Selenium with Microsoft Edge WebDriver to open the video pages for the configured channel URLs, scroll to load more videos, and extract:

- `title` — video title
- `views` — displayed view count, converted from abbreviated forms such as `K` and `M` to a numeric value
- `posted` — YouTube's displayed upload-time label (for example, “2 weeks”); unavailable values are recorded as `N/A`

The notebook exports the collected data to CSV and Excel. The channel URL list and output filename are configured in the notebook.

### 2. `Channels data visualization.ipynb`

Loads the exported CSV files with pandas and explores views by posting-time label. The notebook includes:

- Interactive Plotly scatter plots for individual channels.
- Aggregation of views by the `posted` field.
- Matplotlib bar and scatter charts comparing selected channels.
- A pie chart showing the distribution of aggregated views across posting labels.

The visualizations are exploratory. Since `posted` is a relative text label rather than a precise date, it should not be interpreted as a fully normalized time series.

## Requirements

Use Python 3 with Jupyter Notebook or JupyterLab. The notebooks use these libraries:

- `pandas`
- `selenium`
- `XlsxWriter` (`xlsxwriter`)
- `matplotlib`
- `seaborn`
- `plotly`
- `bokeh`

You also need Microsoft Edge and a compatible Microsoft Edge WebDriver (`msedgedriver`). The WebDriver version should match your installed Edge browser version.

## Setup

1. Clone or download this repository.
2. Create and activate a Python environment.
3. Install the dependencies:

   ```bash
   python -m pip install pandas selenium XlsxWriter matplotlib seaborn plotly bokeh jupyter
   ```

4. Install Microsoft Edge if it is not already installed.
5. Download the matching Edge WebDriver and update the `Service(...)` path in the collection notebook. The current notebook contains a machine-specific Windows path, so it must be changed for your environment.
6. Create the output directory:

   ```text
   Output Files/
   ```

7. Launch Jupyter:

   ```bash
   jupyter notebook
   ```

## How to use

1. Open `YouTube_Channels_Data_Collection.ipynb`.
2. Edit the `urls` list to select the YouTube channel video pages you want to collect.
3. Update the WebDriver path and output filename to match your setup.
4. Run the notebook cells in order. The browser automation scrolls through the channel page to load videos before extracting their visible metadata.
5. Confirm that the CSV and Excel files were created in `Output Files/`.
6. Open `Channels data visualization.ipynb`.
7. Ensure its CSV paths match the files you collected, then run the cells to generate the charts.

## Important considerations

- **Website changes:** YouTube can change its page structure, so Selenium selectors may need maintenance.
- **Collection limits:** The notebook uses a maximum of 70 scroll attempts. This may not load every video on a channel.
- **Dynamic content:** Loading time and network conditions affect which videos are available when the page is inspected.
- **Relative upload labels:** Labels such as “3 days ago” are not converted into absolute dates in the current workflow.
- **View-count formats:** The conversion helper handles plain numeric values and common `K`/`M` abbreviations; other localized formats may need additional handling.
- **Notebook paths:** Paths and channel URLs are configured directly in notebook cells. Keep them consistent across collection and visualization.
- **Responsible use:** Collect only publicly displayed information, respect YouTube's terms and applicable policies, and avoid excessive requests.

## Current scope and possible improvements

The notebooks provide a practical workflow for browser-based data collection and exploratory visualization. Potential next steps include:

- Move channel URLs, output paths, and collection settings into a configuration file.
- Normalize upload labels to dates where reliable data is available.
- Add validation, logging, retries, and more robust element selectors.
- Deduplicate videos and include channel names in a combined dataset.
- Build a dashboard with channel filters and consistent comparison metrics.
- Add summary statistics and automated data-quality checks.

## Disclaimer

This project is for educational and portfolio purposes. It is not affiliated with or endorsed by YouTube. Collected values reflect what the website displays at collection time and may change later.
