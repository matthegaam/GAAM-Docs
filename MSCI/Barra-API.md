# Barra API Automation

Documentation of Project [Barra-API](https://github.com/matthegaam/Barra-API).

## Table of Contents

+ [About](#about)
+ [Getting Started](#getting-started)
+ [Usage](#usage)
    + [Import](#import)
    + [Export](#export)
+ [Contributors](#contributors)

## About

Utilize MSCI Barra Portfolio Manager API for automation.

## Getting Started

### Prerequisites

The project is based on `Python 3.13`.

[MSCI Barra Developer Toolkit](https://developer.msci.com/apis/barraone-developer-s-toolkit-bdt) is required for
accessing API.

### Installing

Install the python dependencies before starting to run the program.

```
pip install -r requirements.txt
pip install msci.bdt-1.4.0-py3-none-any.whl
```

## Usage

### `Import`

```shell
python ./import/main.py {start_date} {end_date} -p {portfolio} [-pri] [-pos] [-mod]
```

Scripts for importing data from database to Barra Portfolio Manager using Barra API. The importing process include
following steps:

1. **Future Modelling** (Optional): `-mod`/`--future_modeling`
    + Construct future on Barra Portfolio Manager using Bloomberg future ID (e.g., 2330=X4 TT Equity) as identifier.
    + Set default as `False`.
2. **Position Uploading**: `-pos`/`--update_position`
    + Upload unit prices for user defined data, i.e., future, composite(index).
    + Set default as `False`.
3. **Price Uploading**: `-pri`/`--update_price`
    + Upload positions for all holding assets.
    + Set default as `False`.

### `Export`

Scripts for exporting reports from Barra Portfolio Manager using Barra API.

1. `load_report`
    + `load_risk_report`: Download **one** risk snapshot report per run and store it as `csv` in the `output` folder
      (Fast).
    + `load_pa_report`: Download **multiple** portfolio analytics time-series reports and store them as `csv` in the
      `output` folder (**Usually slow**, depending on the timespan of time-series).
2. `process_report` (Optional)
    + `process_sa`: Add MAC Issuer ID/Name and Bloomberg ticker to asset reports.

## Contributors

[**Matt He**](mailto:ziyanghe@gaamhk.com)
