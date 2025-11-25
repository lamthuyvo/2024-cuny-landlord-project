# Analysis of NYC landlord Tax Commission Income and Expense data (2021)
This repository contains data, analytic code, and findings that support a portion of the Advanced Data class' final project from Dashiell Allen, Génesis Dávila Santiago, María Mónica Fernández, Deidre Foley, Yi Liu, Nicholas Morgan, Jonnathan Pulla, Rebecca Redelmeier, Liz Rosenberg and Impu Sehgal.


## Data sets

The repository contains data for three analyses. To improve access to this data, we also included raw data of landlord Tax Commission Income and Expense filings, released to CUNY through public records requests.

#### Tax Commission Income and Expense (TCIE) data

Every year landlords of properties that produce income, that are assessed at $40,000 or more, and that consist of at least 10 units have to file a Real Property Income and Expense ([RPIE) ](https://www1.nyc.gov/assets/finance/downloads/pdf/rpie/2020_forms/rpie-2020_worksheet.pdf)form with the NYC Department of Finance. These forms contain detailed income and spending by landlords but are private and exempt from FOIL.

However, a lot of the very same landlords may often file forms, tax certiorari, if they wish to dispute their tax bills, a process during which they[ have little to lose](https://ibo.nyc.ny.us/iboreports/btn-tax-commission.pdf), [according to the Independent Budget Office](https://ibo.nyc.ny.us/iboreports/btn-tax-commission.pdf). When an owner files a tax certiorari to challenge their tax bill, they must also file a [TCIE with their Tax Commission Application for Correction](https://www1.nyc.gov/assets/taxcommission/downloads/pdf/tc201.pdf). ([Here is a key to all of the fields in TCIE data](https://drive.google.com/file/d/1jz6u0iyTXfOtp5T4KlRJpiFzwJZKNDcE/view?usp=sharing).)And these  TCIE forms are FOILable.

The Craig Newmark J-School has received some of the TCIE-based data from 2004 through 2023. The data includes landlords' income and expenses for 29,000 rent-stabilized buildings in NYC (there are currently 38,026 rent-stabilized buildings in NYC), for the years of 2004 through 2019.The school received the missing years of data for 2012, 2016, 2020 and 2021 in January of 2023 from the NYC Dept of Taxation. These data sets are included in the data folder `landlord_data`.



#### TCIE data and other spreadsheets used in the first Analysis
The first analysis is based on two spreadsheets calculates capitalization rates for buildings in the TCIE data.

The spreadsheets needed for the analysis are:

  - [`acris_sales_2020-2022.csv`](data/acris_sales_2020-2022.csv): Raw data on 2,003 building sales in New York City from the years 2020-2022. These data are based on the BIP Database from the University Neighborhood Housing Program.
  - [`file_201_data_sm_tract.csv`](file_201_data_sm_tract.csv): Raw data from the Tax Commission Income & Expenses forms, submitted by building owners to the tax commission seeking revisions on their tax payments. This file contains information from 26,887 forms submitted to the tax commission in the year 2021.

These spreadsheets contain, among others, the following columns relevant to the analysis:

- `price_per_bldg` — The sale price of the buildings represented in the acris file.
- `TOTAL INCOME FROM REAL ESTATE` — The annual business income for building owners in the 201 file, including rents, billboards, and ancillary services.
- `TOTAL EXPENSES` — The total annual expenses for owners represented in the 201 file, such as maintenance and management expenses.
- Borough, Block, and Lot: both files contain information on the BBL of each building, a unique identifier for property plots in New York City.

#### TCIE data and other spreadsheets used in the second analysis

The second analysis looks into spending as a percentage of income and uses the `rent-data.csv`, which represents TCIE data from 2021, and `buildings_list.csv` spreadsheets.

The spreadsheets come from the following sources:

- New York City Tax Commission
  - `data/rent-data.csv`: This includes raw data from forms landlords file with the city's Tax Commission when applying to dispute their tax bills. Not every landlord files this form every year, but many do to request lower tax rates.

- Just Fix (nonprofit group)
  - `data/buildings_list.csv`: This is a list of buildings tied to Robert Izsak, including their BBL indicators, compiled by other teammates.

The `rent-data.csv` contains among others, the following columns:

- `TOTAL EXPENSES` — Total expenses landlords spent on the buildings, self-reported to tax commission
- `TOTAL INCOME FROM REAL ESTATE` — Total income landlords receive from the building, elf-reported to tax commission
- `REPAIRS AND MAINT.` - Total landlords spend specifically on repairs and maintenance of the building, self-reported to tax commission

The  `buildings_list.csv` contains, among others, the following columns:

- `BBL` – the borough, block, and lot number for each building, which is a unique identifier

The exported analyses include:
`output/tax_data_analysis.csv`: This includes total expenses percent of income and total repairs as percent of maintenance for all buildings where income is more than $500,000 and whose expense values are not NULL

`output/relevant_buildings_expenses.csv`: This includes total expenses percent of income and total repairs as percent of maintenance for buildings tied to Iszak.

For context: The [Rent Guidelines Board did a study](https://rentguidelinesboard.cityofnewyork.us/wp-content/uploads/2023/03/2023-IE-Study.pdf) to examine landlords’ costs as compared to their income. One data point relevant to the two landlords we are investigating shows that on average landlords spend 17.6 percent on maintenance. Complimentary to this data are another group’s findings that these buildings have an inordinate amount of HPD violations, something one would expect when not enough money is being spent to maintain and repair buildings. 

#### Data for third analysis

The third analysis looks into building violations and uses two spreadsheets that list Class B and C housing maintenance code violations from the New York City Department of Housing Preservation and Development (HPD).

The spreadsheets come from [“Open HPD Violations” from NYC Open Data](https://data.cityofnewyork.us/Housing-Development/Housing-Maintenance-Code-Violations/wvxf-dwi5/explore/query/SELECT%0A%20%20%60violationid%60%2C%0A%20%20%60buildingid%60%2C%0A%20%20%60registrationid%60%2C%0A%20%20%60boroid%60%2C%0A%20%20%60boro%60%2C%0A%20%20%60housenumber%60%2C%0A%20%20%60lowhousenumber%60%2C%0A%20%20%60highhousenumber%60%2C%0A%20%20%60streetname%60%2C%0A%20%20%60streetcode%60%2C%0A%20%20%60zip%60%2C%0A%20%20%60apartment%60%2C%0A%20%20%60story%60%2C%0A%20%20%60block%60%2C%0A%20%20%60lot%60%2C%0A%20%20%60class%60%2C%0A%20%20%60inspectiondate%60%2C%0A%20%20%60approveddate%60%2C%0A%20%20%60originalcertifybydate%60%2C%0A%20%20%60originalcorrectbydate%60%2C%0A%20%20%60newcertifybydate%60%2C%0A%20%20%60newcorrectbydate%60%2C%0A%20%20%60certifieddate%60%2C%0A%20%20%60ordernumber%60%2C%0A%20%20%60novid%60%2C%0A%20%20%60novdescription%60%2C%0A%20%20%60novissueddate%60%2C%0A%20%20%60currentstatusid%60%2C%0A%20%20%60currentstatus%60%2C%0A%20%20%60currentstatusdate%60%2C%0A%20%20%60novtype%60%2C%0A%20%20%60violationstatus%60%2C%0A%20%20%60rentimpairing%60%2C%0A%20%20%60latitude%60%2C%0A%20%20%60longitude%60%2C%0A%20%20%60communityboard%60%2C%0A%20%20%60councildistrict%60%2C%0A%20%20%60censustract%60%2C%0A%20%20%60bin%60%2C%0A%20%20%60bbl%60%2C%0A%20%20%60nta%60/page/filter) downloaded with the following filters:
- `Housing_Maintenance_Code_Violations-6.csv`
  - Class: B and C only
  - Dates: 1/1/18-12/31/2022
- `Notable_buildings.csv`
  - Class: B and C only
  - Dates: 1/1/18-12/31/2022
  - BuildingID: IDs of buildings tied to Izsak
    - We obtained the building IDs from the 13 buildings connected to Robert Izsak from [JustFix](https://whoownswhat.justfix.org/en/address/BROOKLYN/3030/OCEAN%20AVENUE/portfolio).

Each of the spreadsheets contain, among others, the following columns relevant to the analysis:
- ViolationID — Unique identifier of a violation against conditions in rental dwelling units and buildings.
- BuildingID — Unique identifier of a building.
- Class — Indicator of seriousness of the violations, where A is the least serious and C is the most serious.

**For the purpose of this analysis, we decided to use only the [Class B and C violations](https://www.lawhelpny.org/resource/hpd-violations-checklist) because they represent a greater hazard to the health and safety of tenants.**
- Class B violations are classified as hazardous and include but are not limited to:
  - Roaches or mice
  - Bedbug infestation
  - Mold on ceilings or walls
  - Cracks in tile floor, shower tub; defective wood floors
  - No smoke detector and/or carbon monoxide detector in apartment
  - Broken or defective cabinets, door handles, air ventilators  
- Class C violations are classified as immediately hazardous and include but are not limited to:
  - Holes in the wall/floor and rats/mice are coming in (especially if minors in the house)
  - No hot water (or not consistent).
  - No heat during the heating season.
  - Broken/defective faucets, shower, toilet (e.g., doesn’t flush)
  - Broken stove top, oven, refrigerator (doesn’t cool food)
  - Lead-based paint (if minor age 7 or younger)
  - No window guards (if minors in house).
  - No lock on an entrance door to the building.


## Analyses

#### Cap rate analysis
The notebook [`notebooks/01-cap-rate-analysis.ipynb`](notebooks/01-cap-rate-analysis.ipynb) performs the following analyses:

##### Part 1: Import and Cleaning
- Both spreadsheets were imported into Python and cleaned of duplicates. Both files contained unexpected duplicates--perhaps due to erroneous filings or multiple sales within the two-year period. In order to simplify the analysis, we omitted these data using the drop_duplicates() function.

##### Part 2: Calculation of Cap Rates
- The two data sets were merged into a single data frame for the 241 unique BBLs that are represented on both data sets. Using the combined dataframe, the columns for income, expenses, and building cost were used to calculate the capitalization ratio for each building, using the formula CR=(I-E)/BC.
Buildings that do not have enough information to calculate a capitalization rate were dropped using the dropna() function.

##### Part 3: Analysis by Borough
Using these results, we computed the mean and median capitalization rates for each of the four boroughs. Staten Island was not included. The analysis was exported to [`output/ResultsbyBoro.csv`](output/ResultsbyBoro.csv).

Our analysis showed:

  **Brooklyn**: On average borough 3 has the highest capitalization rates (12.6%) all NYC boroughs excluding Staten Island making them the riskiest investments. The low median cap rate (3.8%),however, means the majority of buildings don't possess a high risk for investors.

  **Manhattan**: this borough contains the second highest cap rate (3.44%) on average. Investments here promise lower return but also lower risks for investors. Also the numbers show that most buildings here have an even lower cap rate (2.19%), meaning large inventory of low-profit buildings.

  **Bronx**: on average the Bronx has a low cap rate (3.14%). The majority of buildings have a slightly higher cap rate (3.27%). Investors will have an easier time finding similar buildings here.

  **Queens**: this borough has the lowest cap rate (3.08%) and the majority of buildings has a slightly higher cap rate (3.73%). Conditions in Queens are similar to the Bronx.

It's worth noting this is only a limited sample and doesn't represent the state of all cap rates in NYC.

The notebooks output this spreadsheet which contains the merged data from the two spreadsheets, and the capitalization rate for 241 buildings represented on both sheets : [`output/capitalizationrates.csv`](output/capitalizationrates.csv).
Another file, [`output/ResultsByBoro.csv`](output/ResultsbyBoro.csv) contains the mean and median capitalization rates for buildings in this analysis, sorted by borough. Staten Island was not included.


#### Expenditure analysis

The notebook [`notebooks/02-tax-data-analysis.ipynb`](notebooks/02-tax-data-analysis.ipynb) performs the following analyses:

**Part 1: Finds expense cost as percent of income, repairs and maintenance cost as percent of income, and repairs and maintenance as percent of total expenses** 

Looks at how much landlords have been spending on expenses, and specifically on repairs, including: 

- Calculates percentage of total expense cost spent on expenses
- Calculates percentage of total expense cost spent on repairs
- Calculates percentage of expenses spent on repairs

This section also uses a describe() function to look at the min, max, mean, and median of spending on repairs as percent of income in this data.

**Part 2: Filters data to remove buildings with very low income**

This filters out buildings where landlords’ income is less than $500,000, to get rid of landlords that have reported $0 or other minimal amounts of rental income. 

This also filters out buildings with NULL values for expenses.

This section also uses a describe() function to look at the min, max, mean, and median of spending on repairs as percent of income in this data after it has been filtered.

This section outputs the expense and repair spending as percentage of income for the filtered building list into the file [`output/tax_data_BuildingAnalysis.csv`].

**Part 3: Looks specifically at the landlords’ buildings and expense and repairs spending as percent of income for only those buildings** 

By merging the `rent_data.csv` with the list of buildings owned by the specific landlords we are investigating, we found how much those landlords have been spending on expenses and repairs.

This section also uses a `.describe()` function to look at the min, max, mean, and median of the landlords’ spending on repairs as percent of income.

This section outputs the landlords’ expense and repair spending as percentage of income in the file `output/relevant_buildings_expenses.csv`


#### Building violations analysis
The notebook `03-building-violations-analysis.ipynb` performs two analyses:

**Part 1: Find the average number of violations per building in NYC.**
- Upload `Housing_Maintenance_Code_Violations-6.csv` to the Jupyter Notebook.
- Use the “GroupBy” function to view how many “ViolationIDs” (a unique ID tagged to every violation) were associated with each “BuildingID” (a single ID used for all violations in a building).
- Use “describe” to view the average number of “ViolationIDs” per “BuildingID” (i.e. violations per building).

**Part 2: Find the average of violations for the 13 buildings tied to Robert Izsak**
- Upload `notable_buildings.csv` to the Jupyter Notebook.
- Use the “GroupBy” function to view how many “ViolationIDs” (a unique ID tagged to every violation) were associated with each “BuildingID” (a single ID used for all violations in a building).
- Use “describe” to view the average number of “ViolationIDs” per “BuildingID” (i.e. violations per building).

The third analysis output this spreadsheet which contains both citywide averages for Class B and C violations as well as those for buildings tied to Izsak: `output/izsak_building_violation_tallies.csv`


## Running the analysis yourself
You can run the analysis yourself. To do so, you'll need the following installed on your computer:
- Python 3
- Pandas, a Python library

## Licensing
All code in this repository is available under the [MIT License](https://opensource.org/licenses/MIT). The data file in the output/ directory is available under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0) license. All files in the data/ directory are released into the public domain.


## Feedback / Questions?
Contact Lam Thuy Vo (lam.vo@journalism.cuny.edu) or Barbara Gray (barbara.gray@journalism.cuny.edu).
