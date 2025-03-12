# New portfolio update workflow
Documentation of workflow: updating new portfolio into multiple systems.

### Project Location: 
 - Dobby: 
   - [Database](https://github.com/changwookshimgaam/database.git) -  `C:\Users\data\PycharmProjects\database `
   - [MSCI_API_to_BPM](https://github.com/GAmikeng/MSCI_API_to_BPM.git) - `C:\Users\data\PycharmProjects\MSCI_API_to_BPM`

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

##### database - `index_ticker.py`
- `python >= 3.8`
- `requirements.txt`

### Running Machine:
- `Dobby`

### Installation Steps
1. `pip install -r requirements.txt`
2. `pip install ./msci.bdt-1.1.2-py3-none-any.whl`

### Configuration Files
##### database
- `.gitconfig`

### Key Scripts
  -  `database/src/preprocess/nav_preprocessor/{new_portfolio}_preprocessor.py` (database)
  -  `database/src/updater/nav_file_metadata_updater.py`
  -  `database/src/updater/portfolio_asset_updater.py`
  -  `database/src/updater/portfolio_daily_updater.py`

### Key Functions
#### database:
##### `src/preprocess/nav_preprocessor/NEWPORT`
   - `get_fund_pa(file)` - return `portfolio_asset` compatible df
   - `get_fund_aum(file)` - return `portfolio_daily` compatible df
###### `nav_file_metadata_updater.py`
   - `nav_keyword_list` - add the file name pattern of new portfolio
###### `portfolio_asset_updater.py`
   - `update_df_dict` - add new portfolio with get_pa and get_aum function
###### `portfolio_daily_updater.py`
   - `pd_update_dict` - add new portfolio with get_nav_file_from_db and get_aum function
#### MSCI_API_to_BPM
##### `main.py`
   - `future_modeling_port`
   - `long_short_port`
##### `get_portfolio_data_from_db.py`
   - `allowed_ports` - add the new portfolio short name and the bpm name 
## Usage <a name = "usage"></a>
### Task Steps
### Update Database Daily Script
1. Fill in the information of portfolio in Database portfolio table
   key columns: `bpm_portfolio_name`, `bpm_nav_attr`, `linedata_portfolio_name(checklinedata)`
2. `database/config/py_config.ini`: Add the nav path and nav file format
3. Add the new portfolio with the path in `py_config.ini`:
   - `nav_dir`
   - `nav_dir_date_format` with ops team folder naming way
4. Create new module with functions and inherit class under `src/preprocess/nav_preprocessor`:
   - Long_only: `NavPreprocessor`
   - Long_Short: `SvNavPreprocessor` / `LhNavPreprocessor`
   - `get_fund_pa(file)`: return `portfolio_asset` compatible df
   - `get_fund_aum(file)`: return `portfolio_daily` compatible df
5. Update `src/updaters/nav_file_metadata_updater.py` variable - `nav_keyword_list` with NAV file nav keyword
6. From new module import `get_fund_pa` adn `get_fund_aum` function and add `gaapf` in `update_df_dict`
7. Edit `str/updater/portfolio_daily_updater.py` - `pd_update_dict`
### UPDATE BARRA
8. Build composite with port name `_{portfolio_shortname}` using `MSCI_upload\ref\gaapf\gaapf_comp_modeling_20250207.xlsx`
9. Login BPM and upload the modeling xlsx
   1. Data Type: `BPM User Assets`
   2. Preferred Model: `BASE`
10. Edit `MSCI_API_to_BPM` add new port to below variable:
    1. `main.py`
       - `parser.add_argument("-new_port")`
       ##### if new port would buy index or index
       - `future_modeling_port`
       - `long_short_port`
    2. `get_portfolio_data_from_db.py`
       - `allowed_ports = {'new_port': 'bpm_port_name'}`

## Debugging Tips <a name = "debugging_tips"></a>
### Common Errors
- Ops team may edit the nav file format, which may cause the script to fail. Ensure that the nav file format is correct and matches the expected format.
- Sheet name of swap may be changed
## Log file location
`logger.txt`

## Contributors<a name = "contributors"></a>
[**Michael Ng**](mailto:mikeng@gaamhk.com)