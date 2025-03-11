# New ticker update workflow

Documentation of workflow: updating new ticker into database
Related Projects:
+ [Database](https://github.com/changwookshimgaam/database.git)

## Table of Contents
+ [About](#about)
+ [Getting Started](#getting_started)
+ [Usage](#usage)
+ [Debugging Tips](#debugging_tips)
+ [Contributors](#contributors)

## About <a name = "about"></a>
  - To update the tickers that not covered in database.
  - To find out its information across different platform

## Getting Started <a name = "getting_started"></a>

### Project Location: 
`F:\BBG04\ticker_data_update`

### Prerequisites
- `new_tickers.py`
- `python >= 3.7`
- `pandas` and `openpyxl`(NO `requirements.txt`) 
- Excel API 
  - CIQ API
  - Factset API
- Barra Portfolio Manager

### Running Machine: 
- BBG02
- Dobby

### Installation Steps
1. Follow the instruction in [database](https://github.com/changwookshimgaam/database.git)

### Configuration Files
- Barra Identity files - 
  - `EFMGEMTR_Asset_Identity.20241129` or
  - `F:\BBG04\ticker_data_update\EFMGEMTR_Asset_Identity.yymmdd`
- `new_tickers.xlsx` - The excel contains ticker information

### Key Scripts
  - `F:/BBG04/ticker_data_update/new_tickers.py`
  - `src/updaters/new_ticker_updater.py`

### Key Variables to change
- `new_tickers.xlsx`
  - `id_barra`
  - `MacIssuerID`

### Key Functions
- `new_tickers.py`
  - `new_tickers()`: To create the new_tickers.xlsx by the input of running program
- `new_ticker_updater.py`
  - `new_ticker_updater(engine)`:To update the DataFrame by new_tickers.xlsx

## Usage <a name = "usage"></a>
### Task Steps

#### Check the missing ticker is not in database ticker table
1. Go to `F:\BBG04\ticker_data_update`
2. run `F:\BBG04\ticker_data_update\new_tickers.py` in any machine
3. Log in `BBG02` pc and open `F:\BBG04\ticker_data_update\new_tickers.xlsx` (directly type in path as only this folder is allowed to access via BBG02)
4. Update `Factset` (whole workbook) and `CapIq` with Excel API
5. Login to `bpm -> workspaces -> Select Grand Alliance Asset Management -> MNg's Workspace Folder -> identifier`
6. Find the new asset by input the `local ID` in the form - `TW2330` / `CN600013` / `USNVDA`
7. Get the `MacIssuerID` and `id Barra`, copy paste into the excel file
8. Login to dobby Add two columns at end for `StartDate` and `EndDate`.
   - Find those values in Barra Identity files 
   i.`efmgemtr\GMD_EFMGEMTR_LOCALID_ID_yymmdd.zip`
   ii.`D:/msci_barra/gemtr/daily/gemtr_<latest_date>`
9. Update and save the identifier excel
   `F:\BBG04\sambbg04\17_Identifier and Classification\Identifier and Classification_NEW.xlsx`
10. Run `new_ticker_updater.py` in `database` updater folder

## Debugging Tips <a name = "debugging_tips"></a>
### Common Errors
- Index Error - To check whether ticker is in db or not
- `S&P` or `Factset` API is not fully run
### Log file location
`src/updaters/new_ticker_updater.log`

## Contributors<a name = "contributors"></a>
[**Michael Ng**](mailto:mikeng@gaamhk.com)