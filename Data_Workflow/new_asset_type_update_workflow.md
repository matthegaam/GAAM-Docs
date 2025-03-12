# New asset type update workflow
Documentation of workflow: updating new asset type into multiple systems.

### Project Location: 
 - Dobby: 
   - [Database](https://github.com/changwookshimgaam/database.git) -  `C:\Users\data\PycharmProjects\database`
   - [MSCI_API_to_BPM](https://github.com/GAmikeng/MSCI_API_to_BPM.git) - `C:\Users\data\PycharmProjects\MSCI_API_to_BPM`
## Table of Contents
+ [About](#about)
+ [Getting Started](#getting_started)
+ [Usage](#usage)
+ [Debugging Tips](#debugging_tips)
+ [Contributors](#contributors)

## About <a name = "about"></a>
  - To be able to add a new asset type in all system include database

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
3. Install Wind API on python (`BBG03` installed)
   Click Start > repair python API > select python path in running `venv`

### Configuration Files
##### database
- `.gitconfig`

### Key Scripts
  -  `database/asset_linedata_updater.py` (database)
  -  `database/trade_updater.py` (database)
  -  `database/trade_ssc.py` (database)
  -  DB View:`bpm_position_import` (MSCI_API_to_BPM)

### Key Variables to change
  - `update_path`: change the path that result stored

### Key Functions
##### `asset_linedata_updater.py`
  - `asset_linedata_updater(df, connection)`: map each asset identifier with id_asset and update asset_linedata table
##### `trade_updater.py`
  - `new_asset_uploader(engine, df_ticker, df_future, df_swap, df_rights, df_linedata)`: to update the new_asset to db with their own updater and update asset table with new primary key id
##### `trade_ssc.py`
- `trade_ssc(filepath, date)`: 
   1. Get data from downloaded trade file
   2. separate and return the data into preprocessed dfs by `asset_type`

## Usage <a name = "usage"></a>
### Task Steps
1. Manual create a table on database with the new asset type (if needed)
2. Edit `trade_ssc` and `trade_updater` to recognise the new asset type and its underlying
3. Run `trade_ssc.py` and `trade_updater.py` to update the new asset type into database
4. Edit the query in `asset_linedata_updater` to map its underlying with its unique identifier
5. Update the modeling way in `MSCI_API_to_BPM` if needed
## Debugging Tips <a name = "debugging_tips"></a>
No

## Log file location
No

## Contributors<a name = "contributors"></a>
[**Michael Ng**](mailto:mikeng@gaamhk.com)