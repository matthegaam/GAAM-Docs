# New index update workflow
Documentation of workflow: updating new index into multiple systems.

### Project Location: 
 - Dobby: 
   - [Database](https://github.com/changwookshimgaam/database.git) -  `C:\Users\data\PycharmProjects\database `
   - [MSCI_API_to_BPM](https://github.com/GAmikeng/MSCI_API_to_BPM.git) - `C:\Users\data\PycharmProjects\MSCI_API_to_BPM`
 - BBG03: 
   - [eze_daily_index_file_delivery](https://github.com/GAmikeng/eze_daily_index_file_delivery) - `C:\Users\bbg03\PycharmProjects\eze_daily_index_file_delivery`
## Table of Contents
+ [About](#about)
+ [Getting Started](#getting_started)
+ [Usage](#usage)
+ [Debugging Tips](#debugging_tips)
+ [Contributors](#contributors)

## About <a name = "about"></a>
  - To add the new index in all of the index related script and data
  - Be aware that Barra use Portfolio to build **composites** as **Index**

## Getting Started <a name = "getting_started"></a>

### Prerequisites

##### MSCI_API_to_BPM
- `python >= 3.10`
- `requirements.txt` 
- `msci.bdt-1.1.2-py3-none-any.whl`

##### eze_daily_index_file_delivery
- `python >= 3.11`
- `requirements.txt`
- Winds API
- Factset API

##### database - `index_ticker.py`
- `python >= 3.8`
- `requirements.txt`

### Running Machine: 
- `BBG02`
- `Dobby`

### Installation Steps
1. `pip install -r requirements.txt`
2. `pip install ./msci.bdt-1.1.2-py3-none-any.whl`
3. Install Wind API on python (`BBG03` installed)
   Click Start > repair python API > select python path in running `venv`

### Configuration Files
##### database
- `.gitconfig`

##### barra update template

- `1_new_index_template_portfolio_create.csv`
- `2_new_composite_create.xlsx`


### Key Scripts
  -  `database/index_ticker_updater.py` (database)
  -  `eze_daily_index_file_delivery.py` (BBG03) 
  -  `MSCI_API_to_BPM/upload_index_breakdown.py` (database)

### Key Variables to change
###### `1_new_index_template_portfolio_create.csv`
   - \<portfolio\>
   - \<portfolio owner\>
   - index breakdown into table
###### `2_new_composite_create.xlsx`
   - Id
   - Asset Name
   - Owner
   - Portfolio

### Key Functions
##### `MSCI_API_to_BPM/upload_index_breakdown.py`
  - `get_latest_index_breakdown(date)`: To update the job 
##### `eze_daily_index_file_delivery/get_daily_bbg.py`
  - `create_bbg_excel_file`: To create excel file with bloomberg formula to run Bloomberg API
##### `index_ticker_updater.py`
  - update the `index_ticker` table for Daily index breakdown


## Usage <a name = "usage"></a>
### Task Steps
1. Manual fill in the Index related data into `index` table
2. Create portfolio by upload position file on Barra Portfolio Manager:
   - Upload Files > Data Type: 
     - BPM Position > select `port_position.csv` > BASE Model > Upload
     `1_new_index_template_portfolio_create.csv`
3. Set up the Index as composite by upload file
   Upload Files > Data Type:
   - BPM User Assets > BASE Model > Upload
         `2_new_composite_create.xlsx`
4. Check the query in `MSCI_API_to_BPM\upload_index_breakdown.py` `get_latest_index_breakdown`
5. Update the script in project - `eze_daily_index_file_delivery`
   - If it is GAAM index, usually edit `bloomberg_excel/open_excel.py`
   - If it is other index, check whether Winds cover or not

## Debugging Tips <a name = "debugging_tips"></a>
### Common Errors
- Index Error - To check whether ticker is in db or not [Some common way to solve the script]
- S&P API or Factset API is not fully run
## Log file location
### Common Errors
- `weight` is not in df 
- To check whether API is timeout or not

## Contributors<a name = "contributors"></a>
[**Michael Ng**](mailto:mikeng@gaamhk.com)