# Open-data release of aggregated Australian school-level information. Edition 2016.1

This is a fork of Australian School data made available by [Monteiro Lobato](https://zenodo.org/record/46086).

Over time the intention is to exyend the datya release by including some R-files giving examples for the analysis of the data.

The SQLite file is a downloadable aggregation of information about Australian schools. The individual files represent a series of tables which, when considered together, form a relational database. The records cover the years 2008-2014 and include information on approximately 9500 primary and secondary school main-campuses and around 500 subcampuses. The records all relate to school-level data; no data about individuals is included. All the information has previously been published and is publicly available but it has not previously been released as a documented, useful aggregation. The information includes:

* the names of schools
* staffing levels, including full-time and part-time teaching and non-teaching staff
* student enrolments, including the number of boys and girls
* school financial information, including Commonwealth government, state government, and private funding
* test data, potentially for school years 3, 5, 7 and 9, relating to an Australian national testing programme know by the trademark 'NAPLAN'

Documentation of this Edition 2016.1 is incomplete but the organization of the data should be readily understandable to most people. If you are a researcher, the simplest way to study the data is to make use of the SQLite3 database called 'school-data-2016-1.db'. If you are unsure how to use an SQLite database, ask a guru.

The database was constructed directly from the other included files by running the following command at a command-line prompt:
  sqlite3 school-data-2016-1.db < school-data-2016-1.sql
Note that a few, non-consequential, errors will be reported if you run this command yourself. The reason for the errors is that the SQLite database is created by importing a series of '.csv' files. Each of the .csv files contains a header line with the names of the variable relevant to each column. The information is useful for many statistical packages but it is not what SQLite expects, so it complains about the header. Despite the complaint, the database will be created correctly.

Briefly, the data are organized as follows.

* The .csv files ('Comma Separated Values') do not actually use a comma as the field delimiter. Instead, the vertical bar character '|' (ASCII Octal 174 Decimal 124 Hex 7C) is used.
* Each school-related record is indexed by an identifer called 'ageid'. The ageid uniquely identifies each school and thereby serves as the appropriate variable for JOIN-ing records in different data files. For example, the first school-related record after the header line in file 'students-headed-bar.csv' shows the ageid of the school as 40000. The relevant school name can be found by looking in the file 'ageidtoname-headed-bar.csv' to discover that the the ageid of 40000 corresponds to a school called 'Corpus Christi Catholic School'.
* In addition to the variable 'ageid' each record is also identified by one or two 'year' variables. The most important purpose of a year identifier will be to indicate the year that is relevant to the record. For example, if one turn again to file 'students-headed-bar.csv', one sees that the first seven school-related records after the header line all relate to the school Corpus Christi Catholic School with ageid of 40000. The variable that identifies the important differences between these seven records is the variable 'studentyear'. 'studentyear' shows the year to which the student data refer. One can see, for example, that in 2008, there were a total of 410 students enrolled, of whom 185 were girls and 225 were boys (look at the variable names in the header line).
* The variables relating to years are given different names in each of the different files ('studentsyear' in the file 'students-headed-bar.csv', 'financesummaryyear' in the file 'financesummary-headed-bar.csv'). Despite the different names, the year variables provide the second-level means for joining information acrosss files. For example, if you wanted to relate the enrolments at a school in each year to its financial state, you might wish to JOIN records using 'ageid' in the two files and, secondarily, matching 'studentsyear' with 'financialsummaryyear'.
* The manipulation of the data is most readily done using the SQL language with the SQLite database but it can also be done in a variety of statistical packages.
* It is our intention for Edition 2016-2 to create large 'flat' files suitable for use by non-researchers who want to view the data with spreadsheet software. The disadvantage of such 'flat' files is that they contain vast amounts of redundant information and might not display the data in the form that the user most wants it.
* Geocoding of the schools is not available in this edition.
* Some files, such as 'sector-headed-bar.csv' are not used in the creation of the database but are provided as a convenience for researchers who might wish to recode some of the data to remove redundancy.
* A detailed example of a suitable SQLite query can be found in the file 'school-data-sqlite-example.sql'. The same query, used in the context of analyses done with the excellent, freely available R statistical package (http://www.r-project.org) can be seen in the file 'school-data-with-sqlite.R'.
