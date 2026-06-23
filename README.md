# Volve Production EDA

Exploratory data analysis on Equinor's Volve field production data. The well bled gas more than oil, and the numbers tell that story plain, once you clean them up and look.

## The Data

Source: `Volve production data.xlsx`, the Equinor open-release file, included in this repo.

Seven unique wells, daily records, with a `FLOW_KIND` column splitting production wells from injection wells. Eight columns dropped early — well bore codes, NPD facility fields, well type, choke unit of measure — since they carried no analytical weight. What's left: dates, well names, on-stream hours, oil/gas/water volumes, choke size, and the flow kind flag.

Missing data and column types were checked before anything else got built on top. No work happens on a foundation you haven't tested.

## What's Done So Far

The notebook (`Volve_Production_EDA_Q&A.ipynb`) runs clean through data prep and into the first two question groups from the EDA question bank.

**Setup and cleaning**
- Loaded the Excel file, set date as index, dropped eight non-analytical columns.
- Checked missing-data percentage per column and confirmed data types.
- Built a well-level summary grouped by well name and flow kind — total entries, oil/gas/water totals, on-stream hours.

**Finding: the field is gas-dominant.** Total gas volume across production wells dwarfs both oil and water. This shaped how every later question got read.

**Section 1 — Production Trends & Decline**
- *How does oil rate change over each well's life?* Plotted decline curves for all seven wells. Two patterns emerged: steady gradual decline (15/9-F-12, 15/9-F-14) versus sharp staged drops followed by flat stretches (15/9-F-1 C, 15/9-F-11, 15/9-F-15 D) — likely tied to choke changes or well interventions, not pure reservoir depletion.
- *Which wells gave the most/least cumulative oil?* Ranked all seven. 15/9-F-4 sits at zero — it's an injector, not a producer, so the number means nothing about reservoir quality. 15/9-F-5 is genuinely low, suggesting minimal or intermittent flow.

**Section 2 — Water & Gas Behavior**
- *When does water cut climb, and is the climb the same shape across wells?* Computed water cut (water volume over total fluid volume) per well per day. Most wells start dry, water cut rises months to a year+ in, but the timing and steepness of that rise differ well to well.
- *Does gas volume track oil volume, or split apart?* Plotted both series per well. They diverge over the long run — gas dominates and decays on its own curve, separate from oil, which tracks back to the gas-dominant field finding up top.
- *Which wells flood early, which stay dry longest?* Water cut calculation is in place; the comparison across wells is the next thing to close out.

## More Questions to Answer

The following sections are still open to be explored.

**Pressure & Temperature**

**Data Quality**

**Field-Level Questions**


## Predictive Modeling — Next Phase

Once the open EDA questions are closed, the cleaned, well-level time series feeds a forecasting model. The goal: predict short-term oil rate per well from production history and operating conditions.

This sits as a third, later phase. The EDA has to finish first; a forecasting model built on questions still half-answered would just be guessing dressed up in code.

## Tools

- **Python** (pandas, NumPy, Matplotlib, seaborn) — cleaning, analysis, visualization, and the modeling phase ahead.
- **Power BI** — dashboard reporting layer once the cleaned, flagged dataset is exported to CSV.

## Repo Contents

| File | What it is |
|---|---|
| `Volve production data.xlsx` | Raw production data, Equinor open release |
| `Volve_Production_EDA_Q&A.ipynb` | Main analysis notebook — cleaning, EDA, question answers |
| `README.md` | This file |
