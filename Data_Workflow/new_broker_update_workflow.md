# New broker update workflow
Documentation of workflow: updating Broker in database

### Project Location:
   - [Database](https://github.com/changwookshimgaam/database.git) -  `C:\Users\data\PycharmProjects\database`

## Table of Contents
+ [About](#about)
+ [Getting Started](#getting_started)
+ [Usage](#usage)
+ [Debugging Tips](#debugging_tips)
+ [Contributors](#contributors)
## About <a name = "about"></a>
To update the `Broker` and make sure it won't interrupt the update of `portfolio_asset` in tables

## Getting Started <a name = "getting_started"></a>

### Prerequisites
a test NAV files with new broker

### Running Machine:
- `Dobby`

### Installation Steps
- No

### Configuration Files
- No

### Key Scripts
  - `portfolio_asset_updater.py`
    - `pa_update_from_nav(r_date)`

## Usage <a name = "usage"></a>
### Task Steps
1. Edit `broker` tables by adding `broker_name` and `broker_shortname` in database
2. Copy a NAV file to be test file with new broker for the same portfolio having same excel structure
3. Change the variable `{update_df_dict}` in func `pa_update_from_nav(r_date)` to the testing file location.
   e.g.```'sv': {'file': 'F:/BBG04/test_nav_20250101_file.xlsx'
               'pa': get_sv_pa,
               'pd': get_sv_aum}```


## Debugging Tips <a name = "debugging_tips"></a>
### Common Errors
- No
## Log file location
`database/src/updater/logger.txt`
## Contributors<a name = "contributors"></a>
[**Michael Ng**](mailto:mikeng@gaamhk.com)