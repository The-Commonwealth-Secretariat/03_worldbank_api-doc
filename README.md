## World Bank Open Data
<br/>

**1. Overview**
The world bank serves as a good source for development indicators covering a broad set of thematic areas, it houses data from other UN divisions in a better-structured format that can be queried through their API.
<br/>

**2. Developers Page** 
The Indicators API supports two basic ways to build queries: a URL based structure and an argument based structure. For example, the following two requests will return the same data, a list of countries with income level classified as low income:
**World Bank API:** https://datahelpdesk.worldbank.org/knowledgebase/articles/898581
<br/>

**3. Using the API** 
To get the data in relational format there are multiple methods to follow outlined in the JSTAT open documentation: https://json-stat.org/

**3.1 Commonwealth member countries sample call**
- `[iso3]`: this is the country/ies iso3 codes, for specifying multiple countries `;` is used as a separator
- `[indicator_code]`: this is the code as defined on the <a href="https://data.worldbank.org/">open data website</a>

```php
http://api.worldbank.org/v2/country/ATG;AUS;BGD;BHS;BLZ;BRB;BRN;BWA;CAN;CMR;CYP;DMA;FJI;GBR;GHA;GMB;GRD;GUY;IND;JAM;KEN;KIR;KNA;LCA;LKA;LSO;MDV;MLT;MOZ;MUS;MWI;MYS;NAM;NGA;NRU;NZL;PAK;PNG;RWA;SGP;SLB;SLE;SWZ;SYC;TON;TTO;TUV;TZA;UGA;VCT;VUT;WSM;ZAF;ZMB;TGO;GAB/indicator/[indicator_code]?format=jsonstat
```
```php
Output Format: The API supports the following four output formats.

- XML format: http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=xml (paginated)
- JSON format: http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=json (paginated)
- JSONP format: http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=jsonP&prefix=Getdata (invalid response) Note: For JSONP format, prefix parameters must be specified.
- JSON-stat format: http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=jsonstat (usable - not paginated)
```

**3.2 Sample Queries)**
pyjstat is a python library for JSON-stat formatted data manipulation which allows reading and writing JSON-stat [1] format with python,using the DataFrame structures provided by the widely accepted pandas library [2]. The JSON-stat format is a simple lightweight JSON format for data dissemination, currently in its 2.0 version. Pyjstat is inspired in rjstat [3], a library to read and write JSON-stat with R, by ajschumacher. Note that, like in the rjstat project, not all features are supported (i.e. not all metadata are converted). pyjstat is provided under the Apache License 2.0.

**Project:** https://pypi.org/project/pyjstat/
1. Installation `pip install pyjstat`
2. Python script:
```python
from pyjstat import pyjstat

EXAMPLE_URL = 'http://json-stat.org/samples/galicia.json'

# read from json-stat
dataset = pyjstat.Dataset.read(EXAMPLE_URL)

# write to dataframe
df = dataset.write('dataframe')
print(df)

# read from dataframe
dataset_from_df = pyjstat.Dataset.read(df)

# write to json-stat
print(dataset_from_df.write())

from pyjstat import pyjstat

indicators_url = '<replace_with_url_cw-members'

# read from json-stat
dataset = pyjstat.Dataset.read(indicators_url)

# write to dataframe
data_frame = dataset.write('dataframe')

# read from dataframe
indicators_dataset = pyjstat.Dataset.read(data_frame)
```








