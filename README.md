# Open-data release of aggregated Australian school-level information. Edition 2016.1

This is a fork of Australian School data made available by [Monteiro Lobato](https://zenodo.org/record/46086).

Over time the intention is to extend the data release by including some R-files giving examples for the analysis of the data.

The SQLite file is a downloadable aggregation of information about Australian schools. The records cover the years 2008-2014 and include information on approximately 9500 primary and secondary school main-campuses and around 500 subcampuses. The records all relate to school-level data; no data about individuals is included. All the information has previously been published and is publicly available but it has not previously been released as a documented, useful aggregation. The information includes:

* the names of schools
* staffing levels, including full-time and part-time teaching and non-teaching staff
* student enrolments, including the number of boys and girls
* school financial information, including Commonwealth government, state government, and private funding
* test data, potentially for school years 3, 5, 7 and 9, relating to an Australian national testing programme

Documentation of this Edition 2016.1 is incomplete but the organization of the data should be readily understandable to most people.  Briefly, the data are organized as follows.

* Each school-related record is indexed by an identifer called 'ageid'. The ageid uniquely identifies each school and thereby serves as the appropriate variable for JOIN-ing records across tables.
* In addition to the variable 'ageid' each record is also identified by one or two 'year' variables. The most important purpose of a year identifier will be to indicate the year that is relevant to the record.
* The variables relating to years are given different names in each of the different tables ('studentsyear' in the _student_ table, 'financesummaryyear' in the _financesummary_ table). Despite the different names, the year variables provide the second-level means for joining information acrosss tables. For example, if you wanted to relate the enrolments at a school in each year to its financial state, you might wish to JOIN records using 'ageid' in the two tables and, secondarily, matching 'studentsyear' with 'financialsummaryyear'.
* The manipulation of the data is most readily done using the SQL language with the SQLite database but it can also be done in a variety of statistical packages.
