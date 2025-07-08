**BC AF Trade Tool**
by: Leila Bautista (leila.bautista@gov.bc.ca)

The BC AF Trade Tool is an agriculture and food-specific tool to view trade value (e.g., domestic export, imports and trade balance) for all Canadian provinces and territories by country and state destination and commodity type using various classification systems.

**Steps to building an AF Trade Tool**
1. Run BC_AF_Trade_Tool_Build.Rmd which requires HS8X_2022_AAFC_REF.csv to:

   a. Loop through 2003-2024 and load data from https://search.open.canada.ca/opendata/?sort=metadata_modified+desc&search_text=cimt&page=1

   b. Filter export data for agrifood HS8 codes using HS8X_2022_AAFC_REF.csv

   c. Filter import data for agrifood HS10 codes using HS10X_2022_AAFC_REF.csv

   d. Bind all years of export together and create "Estimate" variable to identify exports

   e. Bind all years of import together, aggregate commodities up to HS8,  and create "Estimate" variable to identify imports

   f. Bind both export and import data together by unique date, province, country, state, estimate

   g. Unpivot and calculate trade balance

   h. Write and store TradeFULL.csv into shared location
   
3. Load data into PowerBI (or any other data visualization software)
   
   a. Load TradeFULL.csv using the M query, TradeFULL.txt

   b. Load Commodity_Classification.csv using the M query, Commodity Classification.txt

   c. Load ODPF_6_CtyDesc.TXT using the M query, TradeREF_Country.txt

   d. Load ODPF_7_StateDesc.TXT using the M query, TradeREF_Province.txt

   e. Load ODPF_8_ProvDesc.TXT using the M query, TradeREF_Province.txt

   f. Load ODPF_9_UOMDesc.TXT

   g. Create relationships between reference tables from stebs b to f and TradeFULL.csv

4. Run BC_AF_Trade_Tool_Update.Rmd to

   a. Load [specify year] export and import value data

   b. Filter for agrifood HS8 and HS10 codes then aggregate to HS8 accordingly

   c. Bind export and import data to calculate trade balance

   d. Load TradeFULL.csv from shared location

   e. Bind updated data with TradeFULL.csv

   f. Write and store TradeFULL.csv into shared location

5. Refresh PowerBI dataset and publish
