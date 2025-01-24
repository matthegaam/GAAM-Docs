# ESG

Documentation of Project [ESG](https://github.com/matthegaam/ESG).

## Table of Contents
+ [About](#about)
+ [Getting Started](#getting_started)
+ [Usage](#usage)

## About <a name = "about"></a>
ESG-related data projects in Grand Alliance Asset Management. 

## Getting Started <a name = "getting_started"></a>

### Prerequisites

The project is based on `Python 3.12.8` (Tested: `Python<3.8` not able to run due to lack of dependencies).

[ODBC](https://docs.databricks.com/en/integrations/odbc/dsn.html) is required for external connection to S&P Global Databricks workbench. 

### Installing

Install the python dependencies before starting running the program. 

```
pip install -r requirements.txt
```

Follow the instructions to install ODBC server.

#### ODBC Environment Setup

1. Create a token in your S&P workbench `User->Settings->Developer->Access tokens`.
2. Use the token along with the params in `.gitconfig` to setup the ODBC DSN configuration.
   - Use **HTTP** as **Thrift Transport**.
   - Setup **HTTP Options** using `httppath` provided in `.gitconfig`.
   - **Enable SSL** in **SSL Options**.

End with an example of getting some data out of the system or using it for a little demo.

## Usage <a name = "usage"></a>

Add notes about how to use the system.
