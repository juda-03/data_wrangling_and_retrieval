# Do FIFA World Cups Create Lasting Economic Benefits?

## Introduction

This project examines whether hosting the FIFA World Cup creates lasting economic and tourism benefits or mainly produces a temporary boost accompanied by higher public costs. It combines four host-country case studies, with each notebook representing one team member's contribution:

- Germany (2006), compared with France
- South Africa (2010), compared with Morocco
- Brazil (2014), compared with Mexico
- Russia (2018), compared with Poland

Each host is compared with a non-host control country to distinguish changes associated with the tournament from broader regional or global trends. The project covers the five years before each World Cup, the event year, and the following five years.

## Data and Data Sources

The analysis uses annual country-level data for:

- GDP in current US dollars
- Annual GDP growth
- Inflation
- Unemployment
- Government gross debt as a percentage of GDP
- International tourism receipts
- International tourist arrivals
- Tourism receipts as a percentage of GDP, calculated in the notebooks

The main data sources are:

- [World Bank Open Data](https://data.worldbank.org/indicator) for GDP, GDP growth, inflation, unemployment, tourism receipts, and most tourism-arrival data
- [World Bank API](https://api.worldbank.org/v2/) for programmatic data collection
- [IMF DataMapper](https://www.imf.org/external/datamapper/) for government gross debt as a percentage of GDP
- [Our World in Data: International Tourist Trips](https://ourworldindata.org/grapher/international-tourist-trips) for consistent tourist-arrival data where the World Bank series did not cover the complete comparison period, especially for the France/Germany and Russia/Poland comparisons
- Wikipedia pages for the [2006](https://en.wikipedia.org/wiki/2006_FIFA_World_Cup), [2010](https://en.wikipedia.org/wiki/2010_FIFA_World_Cup), [2014](https://en.wikipedia.org/wiki/2014_FIFA_World_Cup), and [2018](https://en.wikipedia.org/wiki/2018_FIFA_World_Cup) FIFA World Cups, used to retrieve visual assets and tournament information for the presentation

## Research Questions and Conclusions

### 1. Did host countries experience stronger economic growth after the World Cup?

Not consistently. Germany and Russia improved relative to their control countries in average GDP growth, while South Africa underperformed Morocco slightly and Brazil underperformed Mexico substantially. Hosting therefore did not guarantee stronger long-term economic growth.

### 2. Did hosting produce a lasting tourism benefit?

Tourism was the clearest area of improvement for Germany, South Africa, and Russia when measured by tourist arrivals relative to their control countries. However, Brazil recorded a smaller rise in arrivals and tourism receipts than Mexico, and Russia's tourism revenue declined more than Poland's in the post-2018 period. The tourism effect was therefore visible in arrivals but not always in revenue.

### 3. Did the host countries' fiscal and labor-market positions improve?

The evidence is mixed. Germany performed better than France in relative debt and unemployment changes, while South Africa, Brazil, and Russia experienced less favorable labor-market and debt outcomes than their controls. This suggests that hosting alone did not reliably improve public finances or employment.

### Overall Conclusion

The findings do not support the idea that hosting a World Cup automatically creates broad, lasting economic gains. Germany shows the strongest relative post-event performance, while South Africa's clearest benefit is tourism rather than wider economic development. Brazil shows the weakest post-event macroeconomic results, and Russia shows a mixed result: better relative GDP growth and tourist arrivals, but worse relative unemployment, debt, and tourism revenue. The results are observational and should not be interpreted as proof that the World Cup alone caused these changes.

## Methodology

### Data Collection and Cleaning

1. Reusable Python functions requested each indicator from the World Bank and IMF APIs.
2. API responses were reduced to standardized `year` and indicator-value columns.
3. Years were converted to integers and filtered to an 11-year window for each case study.
4. Indicator tables were merged by year using outer joins so that incomplete observations were retained rather than silently removed.
5. Host and control data were combined into one analysis-ready table.
6. Tourist-arrival gaps were checked and supplemented with the Our World in Data international tourist trips CSV where needed, including the Germany/France and Russia/Poland comparisons.
7. Missing Russia/Poland tourism values were filled from the cleaned CSV where possible, and remaining tourism-revenue gaps were forward-filled inside each country to keep the comparison table usable.
8. Tourism receipts as a share of GDP were calculated as:

   `tourism receipts / GDP × 100`

### Analysis

- Years before the tournament were labeled `Before`; the event year and later years were labeled `After`.
- Mean values were calculated for every indicator, country, and period.
- The change from the before-period mean to the after-period mean was calculated for each country.
- A comparative-impact estimate was produced by subtracting the control country's change from the host country's change. This resembles a simple difference-in-differences comparison, although it is not a full causal model.
- Year-by-country pivot tables were created to inspect trends and support the presentation.

### Visualization

The notebooks organize GDP, growth, debt, tourism receipts, tourist arrivals, and tourism's share of GDP into comparable annual tables. World Cup visual assets were collected with `requests` and `BeautifulSoup`, and the key trends and comparisons were incorporated into the project presentation.

## Main Findings and Insights

| Host and control | Relative post-event result for the host |
|---|---|
| Germany vs. France | GDP growth improved by 1.61 percentage points more; average tourist arrivals increased by about 2.90 million more; unemployment fell by 1.65 percentage points more; debt increased by 3.92 percentage points less. |
| South Africa vs. Morocco | Average tourist arrivals increased by about 1.67 million more, but GDP growth changed by 0.38 percentage points less favorably, unemployment by 2.71 points less favorably, and debt by 6.16 points less favorably. |
| Brazil vs. Mexico | GDP growth changed by 4.03 percentage points less favorably, unemployment by 3.98 points less favorably, and debt by 5.75 points less favorably. Tourism also grew less than in the control country. |
| Russia vs. Poland | GDP growth improved by 1.21 percentage points more and tourist arrivals changed by about 22.91 million more favorably, but unemployment changed by 3.39 points less favorably, debt by 4.92 points less favorably, and tourism revenue by about $5.23 billion less favorably. |

Additional insights:

- Tourism benefits can occur without broader improvements in growth, employment, or public debt.
- Germany provides the most positive case, but its study period overlaps with the 2008–2009 global financial crisis, which complicates interpretation.
- Brazil's weak post-2014 performance also overlaps with a major domestic recession and political instability.
- Russia's post-2018 period overlaps with COVID-19 and the war in Ukraine, so its later tourism and macroeconomic indicators should be interpreted with extra caution.
- Control-country comparisons improve the analysis, but France, Morocco, Mexico, and Poland are not perfect counterfactuals for their respective hosts.
- Differences in national tourism-reporting practices may affect direct cross-country comparisons.

## Further Questions and Next Steps

- Add more World Cup host countries to compare the results.
- Use more control countries to make the comparisons stronger.
- Include stadium and infrastructure costs in the analysis.
- Separate short-term tourism effects from long-term economic effects.

## Project Links

- [Project presentation](https://docs.google.com/presentation/d/1p3RL0VyDrwbaLa2Aw5mMIbnnC8CKKLP46TAex14dvDg/edit?usp=sharing)
- [Trello board](https://trello.com/b/Ll64HGZb)
