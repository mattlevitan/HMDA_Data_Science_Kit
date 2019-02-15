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

This branch was developed from  a public domain work of the _US Government_, including much of this readme. Broken (missing) links from the master cfb/HMDA_Data_Science_Kit have not been removed, you may find them noted with a strikethrough.

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
