**The Goal:**

Download Metadata from the Royal Danish Library’s COP API, parse each MODS XML record, and put the results in a pandas DataFrame, then export to Excel and CSV.

**How you get the URL:**

Open https://api.kb.dk/data/cop, choose an edition (e.g. “Billeder”), set a search term, and submit.

Copy the URL from the MODS field.

To fetch all hits in one response, set itemsPerPage to the total hit count (replace the default, often 30).

**What the notebook does:**

- Loads the MODS URL with requests, parses XML with BeautifulSoup (xml parser).
- Finds all <mods> elements.
- Functions get_text / get_all_text pull text from MODS nodes.
- parse_one_mod maps each record to columns: object id, collection link, titles, origin, dates, topics, persons, identifiers, IIIF/image/thumbnail links, dimensions, relations, access conditions, etc. Object ids also come from processing instructions <?cobject_id ...?> in the response.
- Builds df_alt from all records.
- Saves files named mods_data_<query_sanitized>_<timestamp>.xlsx and .csv (needs openpyxl for Excel).

**Libraries:**

pandas, requests, beautifulsoup4 (with lxml recommended for xml parsing), openpyxl for to_excel.

**Note:**

Change the url variable in the notebook to your search/collection; the example uses a “Cirkusplakater” query on the Billeder syndication feed.
