#### **Table of Contents:**
- [Repository purpose and scope](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#repository-purpose-and-scope)
- [What is HMDA](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#what-is-hmda)
- [HMDA Datasets](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#hmda-datasets)
- [Integration of Census Data with HMDA](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#integration-of-census-data-with-hmda)
- [Official HMDA documentation](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#hmda-data-documentation)
- [Official HMDA data publications](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#hmda-publications)
- [Working With HMDA Data](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#working-with-hmda-data)
- [Getting Started: Basic Requirements](https://github.com/mattlevitan/HMDA_Data_Science_Kit/blob/gschool/readme.md#basic-requirements-and-instructions)



#### Repository Purpose and Scope:
The primary goal of this repository is to provide data users with tools to enable them to produce accurate analytics results. The primary goal of this branch is to provide data users with tools to enable them to produce Geospatial visualizations from HMDA databases quickly and easily. Plotting the data on a map can aid users in confirming accurate attribution of records to geographies. Additionally, this repository provides an overview of HMDA resources, publications, and guidelines for proper use. This repository does not provide statutory interpretation or compliance assistance.


A note to the reader:

This branch was developed from  a public domain work of the _US Government_, including parts of this readme. Broken (missing) links from the master repository cfb/HMDA_Data_Science_Kit have not been removed, for illustrative purposes, you may find them noted with a strikethrough.

## What Is HMDA?
HMDA refers to the [Home Mortgage Disclosure Act of 1975](https://www.gpo.gov/fdsys/pkg/USCODE-2011-title12/pdf/USCODE-2011-title12-chap29.pdf).
HMDA requires many financial institutions to maintain, report, and publicly disclose loan-level information about mortgages. HMDA was originally enacted by Congress in 1975 and is implemented by [Regulation C](https://www.consumerfinance.gov/policy-compliance/rulemaking/final-rules/regulation-c-home-mortgage-disclosure-act/).

Congress amended HMDA in 2010 and the Bureau finalized a rule implementing changes to HMDA in 2015. Most of the rule's provisions affect data collected in 2018 and reported in 2019. However, beginning with data collected in 2017, depository institutions that originated fewer than 25 covered closed-end mortgages in either of the preceding two years are not required to report.

The senate bill S2155 modified some reporting requirements for the 2018 data collection. These changes will be outlined in upcoming publications.

#### **What is the purpose of HMDA?**
- To **provide the public with information** that will help show whether financial institutions are serving the housing credit needs of the neighborhoods and communities in which they are located.
- To **aid public officials in targeting public investments** from the private sector to areas where they are needed.
- The FIRREA amendments of 1989 require the collection and disclosure of data about applicant and borrower characteristics to assist in **identifying possible discriminatory lending** patterns and enforcing anti-discrimination statutes.

#### HMDA Datasets
Three raw data files are published annually under HMDA authority. File formats (and schemas) vary by data source. The National Archives (NARA) use a .DAT format, the FFIEC site maintained by the Federal Reserve Board (FRB) use a .CSV format (with Census data appended) and the FFIEC site maintained by the BCFP us a pipe-delimited .TXT format (with Census data appended). Links to HMDA datasets are available in this [file](https://github.com/cfpb/HMDA_Data_Science_Kit/blob/master/hmda_data_links.md).

These datasets include:
- The Loan Application Register (LAR): This dataset contains application and origination activity on covered transactions made by covered institutions. The LAR is distinct from many other mortgage datasets as it includes both application and origination data as well as borrower demographic information. The LAR has had several distinct schemas including a change from aggregate to transaction level data in 1990. LAR schemas are available in this [folder]() and a discussion of changes to underlying data (such as the benchmark for the rate spread variable) can be found in the [~~Working with HMDA Data~~]() document.

- The Transmittal Sheet (TS): This dataset contains information about the financial institutions that are covered by HMDA and submitted LAR data to the FFIEC. Transmittal sheet schemas can be found in this [~~folder~~]().

- The HMDA Reporter Panel: This dataset contains additional information regarding financial institutions such as identifier links to the National Information Center (NIC) and hierarchy information such as parent and top holder. The HMDA Reporter Panel is assembled by the Bureau on behalf of the FFIEC (beginning in 2017). Panel schemas can be found in this [~~folder~~]().


### Integration of Census Data with HMDA


##### For examples on how to handle Census data and join Census data to LAR data please see the [Census Directory](https://github.com/cfpb/HMDA_Data_Science_Kit/tree/master/census).

## [**HMDA Data Documentation**](https://github.com/cfpb/HMDA_Data_Science_Kit#hmda-data-documentation)

## HMDA Publications
##### For a list of HMDA publications, see [here](https://github.com/cfpb/HMDA_Data_Science_Kit/blob/master/federal_pubs.md)


## **Working With HMDA Data**
##### The HMDA data are complex and care must be taken to ensure that analytics results are accurate. Please see [~~Working With HMDA Data~~]() for explanations of how to load, segment the data, handle NA values, and create accurate time-series tabulations.


#### Basic Requirements and Instructions

#### Requirements
The resources in this repository assume that a database has been installed and is functioning properly. The SQL code is written for [PostgreSQL](https://www.postgresql.org/), other SQL versions may require modification to the code.

The Python resources assume that a functioning installation of [Python 3.5 or greater](https://www.python.org/downloads/) or greater is present. Convention in these instructions and code resources will use python3 to invoke python scripts. If two versions of Python are not present, this command may need to be changed to python, without the 3.

This repository has a requirements.txt file that can be used to install the Python libraries used in the repository:
- `pip install -r requirements.txt`

#### Downloading and Unzipping Data
To begin using the HMDA data you will first need to download the data. A list of data resources is available in [HMDA data links](https://github.com/cfpb/HMDA_Data_Science_Kit/blob/master/hmda_data_links.md).

These data can be downloaded manually from the links listed or the following script can be run from the HMDA_Data_Science_Kit directory:  
- `bash download_scripts/download_hmda.sh`

The script can download HMDA ultimate data files for LAR, Transmittal Sheet, and Panel for the years 2004 through 2017.

Running the script without flags will download all LAR, Transmittal Sheet, and Panel files that are not present.

The script accepts the following option flags:
- -a: Prints to console the available files for download.
- -s: Allows a specific file to be downloaded if it is not present. The name convention for specific files is as follows: lar_<year>, panel_<year>, or ts_<year>.
- -p: Downloads all Panel files that are not present.
- -t: Downloads all Transmittal Sheet files that are not present.
- -l: Downloads all LAR files that are not present.
- -F: Deletes the file or file types to be downloaded (the files are then redownloaded).
- -h: Prints to console the instructions for using the script.

Usage examples:
To download LAR files: `bash download_scripts/download_hmda.sh -l`
To download Panel files: `bash download_scripts/download_hmda.sh -p`
To download Transmittal Sheet files: `bash download_scripts/download_hmda.sh -t`
To download a specific file: `bash download_scripts/download_hmda.sh -s filename`
To delete and download Panel files: `bash download_scripts/download_hmda.sh -Fp`
To delete and download a specific file: `bash download_scripts/download_hmda.sh -Fs filename`
To delete and download LAR 2004: `bash download_scripts/download_hmda.sh -Fs lar_2004`

Download Troubleshooting:
Sometimes files from the National Archives fail to download correctly. An indicator that this happens is the presence of a file with the correct name (such as LAR_20013.zip) that has a filesize of 4kb. In these cases the file must be deleted and redownloaded. One way to do this is:
 - `bash download_scripts/download_hmda.sh -Fs <filename>`.

Unzipping Compressed Files:
All of the LAR files, and several of the Panel and Transmittal Sheets download as zip files. Prior to loading these data the files must be unzipped. To do so, run the following script:
- `bash download_scripts/unzip_all.sh`

The above script will unzip all the zipped files and standardize the names of the files.

Alternatively, the LAR, Panel, and Transmittal Sheet files can be unzipped as groups using the following commands:
- `bash download_scripts/unzip_and_rename_lar.sh`
- `bash download_scripts/unzip_panel.sh`
- `bash download_scripts/unzip_ts.sh`


### **Creating Postgres Tables and Loading Data**

The default installation of Postgres should create both a Postgres role (superuser account) and a Postgres database. The default behavior of the load scripts uses these for login. If the role or the database are not present then a user and/or database will need to be specified when running the load scripts. Examples are provided later in this section.

Available option flags for the load scripts are as follows:
- -u: Sets the user role for the Postgres connection, default is postgres.
- -p: Sets the password for the Postgres connection, default is blank.
- -d: Sets the database for connection, default is postgres.
- -h: Sets the database host, default is localhost.
- -o: Sets the database connection port, the default is 5432.
- --help: Displays the options available for the script.

The script below creates a HMDA database on an existing Postgres installation, creates the hmda_public schema, creates tables, and loads data:
- `bash load_scripts/create_hmda_db.sh`

To load subsets of the HMDA data (LAR, Transmittal Sheet, or Panel) use the scripts below. These scripts will create a database named 'hmda' if one does not exist. They will also create a hmda_public schema in which all the data tables will be created and populated.
- `bash load_scripts/create_and_load_lar_2004_2017.sh`
- `bash load_scripts/create_and_load_ts_2004_2017.sh`
- `bash load_scripts/create_andload_panel_2004_2017.sh`

Using Options Flags:
All of the load scripts support the same option flags. The example below use the create_hmda_db.sh script, but any script can be substituted.

To specify a username:
- `bash load_scripts/create_hmda_db.sh -u <username>`

To specify a password:
- `bash load_scripts/create_hmda_db.sh -p <password>`

To specify a database:
- `bash load_scripts/create_hmda_db.sh -d <database>`

To specify a username and password:
- `bash load_scripts/create_hmda_db.sh -u <username> -p <password>`


The SQL scripts provided in HMDA_Data_Science_Kit/load_scripts/SQL require an update to the path for the data sources before they can be used. The placeholder is {data_path}. This placeholder is replaced with the full path to the HMDA data when any of the load scripts are run. For example {data_path}HMDA_Data_Science_Kit/data/lar/lar_ult_2004.dat' on a Mac will become /Users/<username>/HMDA_Data_Science_Kit/data/lar/lar_ult_2004.dat'.

This change can be undone by running the following:
- `python3 load_scripts/reset_path.py`


## **Geospatial Plotting via Plotly**
```python
    import psycopg2 #Imports the Psycopg2 library
    import pandas as pd #Imports the Pandas library and renames it "pd"
```


Establish connection parameters.

If you have established a username and password, change user and password below to your own username and password.
```python3
connection_params = {"user":"postgres",
                 "password":"",
                 "dbname":"hmda",
                 "host":"localhost"}
```


This function accepts a dictionary of connection parameters that must include:
- user: the username to be used for the database session
- password: the user's password
- dbname: the name of the database for connection
- host: the host location of the database

```python
def connect(params):
    try:
        conn = psycopg2.connect(**params)
        print("I'm connected") #print a success message
        return conn.cursor() #return a cursor object
    except psycopg2.Error as e:
        print("I am unable to connect to the database: ", e)
        #print a fail message and the error, if any
```

Test the connection function, if everything is correct, it will print "I'm connected."

```python
cur = connect(params=connection_params)
cur.close()
```
Close the cursor. This is important as open cursors can interfere with updates to data tables.



When using Jupyter, it is best to open and close the cursor in the same code cell.
If there are coding errors that interrupt the execution, the cursor will need to be reestablished.

### Establishing a SQL Command String
In Python, SQL commands are handled as multi-line strings, denoted by three double quotes at the beginning
and 3 double quotes at the end for example:
```
"""
SELECT  
things
FROM  
data_table;
""" ```

These strings are then passed through a Psycopg2 cursor object (the connection function defined above) and executed by the Postgres database.



```python

sql_command = """
              SELECT activity_year, COUNT (*) AS filer_count
              FROM hmda_public.ts_2017
              GROUP BY
              activity_year;
              """

```
The SQL statement inside cur.execute(<sql_command>) will retrieve the year and count of institutions for the 2017 Transmittal Sheet.
```python
cur = connect(connection_params)
cur.execute(sql_command)
results = cur.fetchall() #Saves the query results.
cur.close()  
```

This implementation of psycopg2 performs four steps for each queury:
- Connects to the database using parameters established above.
- Uses the SQL statement above to pull year and count of filers for 2017.
- Saves the query results.
- Closes the connection to the database.


```python
results_df = pd.DataFrame(results, columns=[desc[0] for desc in cur.description])

```

Converts the output to a Pandas dataframe, The cursor object contains information about the SQL query.
In this instance we use the column names from the data table to name the columns in our dataframe. The use of the _df in naming variables indicates that it is of a pd.DataFrame type.




### Variabalizing a SQL Command String for Filtering
As demonstrated in the previous example, Python strings can contain markers which enable substitution of values. This allows use of the .format() command to change the table reference for the SQL query. The string below selects the activity year and the filer count, variabalizing the year.   

```python
sql_command = """SELECT
                    activity_year,
                    COUNT (*) AS filer_count
                 FROM
                    hmda_public.ts_{year}
                 GROUP BY
                    activity_year;"""
```

A SQL command string may be modified to select a count of filers by a given category. The command string below not only variabalizes the year of the file to be selected but also creates an extention to the query that may be modified by the user.  


```python
sql_base = """SELECT CONCAT(lar_{year}.state_code,lar_{year}.county_code) AS fips,
           count(case when lar_{year}.loan_purpose = '1' then 1 else null end) as prps_prch,
           count(case when lar_{year}.loan_purpose = '2' then 1 else null end) as prps_impr,
           count(case when lar_{year}.loan_purpose = '3' then 1 else null end) as prps_refi
            FROM lar_{year} {extention}
            ;"""

extention = "GROUP BY state_code,county_code"
```

```python
cur = connect(connection_params)
year = 2016
cur.execute(sql_base.format(year=year, extention=extention))
results = cur.fetchall() #Returns the query results.
results_df = pd.DataFrame(results, columns=[desc[0] for desc in cur.description])
cur.close()
results_df.head()
```

<div>
    <a href="https://plot.ly/~levitan.matt/28/?share_key=Qgcv0abNUbnj2qyHmyal7f" target="_blank" title="choropleth of us counties - purchase incidence LAR" style="display: block; text-align: center;"><img src="https://plot.ly/~levitan.matt/28.png?share_key=Qgcv0abNUbnj2qyHmyal7f" alt="choropleth of us counties - purchase incidence LAR" style="max-width: 100%;width: 900px;"  width="900" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="levitan.matt:28" sharekey-plotly="Qgcv0abNUbnj2qyHmyal7f" src="https://plot.ly/embed.js" async></script>
</div>
