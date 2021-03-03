# Software Analytics Katas
Small exercises designed to train analytical thinking and the use of data-driven software analysis.

_If you want to get started with Python & pandas right away, you can do so by clicking this button right now!_ [![Binder](http://mybinder.org/badge.svg)](http://mybinder.org/repo/feststelltaste/software-analytics-katas)


## Motivation Problem
Data source: Stack Overflow  
Difficulty: easy  

### Problem Context
Developers in a software company use a version control system (VCS for short) called CVS (Concurrent Versions System).
Now developers have the idea to migrate to SVN (Subversion).
However, you believe that "Git" has become the standard in the software development community.
So you suggest Git as an alternative for the team.

### Your Task
Find data-driven facts that show that the software development community mainly uses the version control system Git!

### Additional Information
- You know that Stack Overflow is a platform that provides answers to questions regarding certain technologies.

### Starters
- File (~ 4 MB) with statistics about the questions asked on Stack Overflow about version control systems over several years.
  - `CreationDate`: The timestamp of the creation date of a Stack Overflow post (= question).
  - `TagName`: The tag name for a technology (in our case for only 4 VCSes: "cvs", "svn", "git" and "mercurial").
  - `ViewCount`: The number of views of a post
- Dataset URL: [`datasets/stackoverflow_vcs_data_subset.csv`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/stackoverflow_vcs_data_subset.csv)


## A Long Ping Pong Along
Data source: Log files  
Difficulty: medium  

### Problem Context
The control software for the "DependencyHell" ghost train attraction was implemented as a microservices architecture.
Since there were unexplained failures in spooky cases again and again, aping API was introduced for all services.
This allows services to call other services to see if they are currently reachable.
A convention was introduced for the API that any working service should acknowledge a call to `/healthy` with the HTTP status code 200.
However, there are still sporadic failures.

### Your Task

The development team would like to narrow down when and why the sporadic bugs occur. 
An analysis of the log files about the failure situations at the microservices should provide clarity.

### Additional Information
- There is an aggregated log file that logs the ping calls over several days.
- The log file format is the same for all services
- The operating software runs in the exhibitor's own data center.
- The showman usually operates from 1 p.m. and sometimes deep into the night.

### Starters
- Log file (~7 MB) with the recorded communication between the services of one week with the following information:
  - `timestamp`: timestamp of the log entry
  - `status`: Returned HTTP status code of a request
  - `method`: HTTP request method used
  - `url`: Called service URL
  - `ms`: Response time of the called service call
- Dataset URL: [`datasets/scarylog.csv`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/scarylog.csv)
  - Possible header string: `"timestamp", "status", "method", "url", "ms"`.


## Tests just Code, too
Data source: version control system  
Difficulty: medium  

### Problem Context
The developers of the integrated development environment "IntelliJ IDEA" have noticed that many developers check out the current version, make changes, but do not commit the changes back to the repo until days later in one big commit.
This leads so many merge conflicts thus conflicts among developers as well.
In most cases, developers also forget to check in newly written tests (or they don't even at all, which is only discovered later during the code review).

To improve the development process, the developers have agreed on the following measures:

- All commits must now contain less than 500 lines of code.
- The ratio of test code to source code must be at least 0.7:1 at the end of the day.

### Your Task
Show that developers are now working as they have agreed upon!
Track the commit activities and find out, if developers are now writing tests as they should.

### Additional Information
- Only source code written in Java or Kotlin is affected by the measure.
- IntelliJ IDEA uses the postfix "Test" as an identifier for test code.
- Source code is managed using the Git version control system.
- The software project uses a Continuous Integration Server.

### Starters
- A (preprocessed) Git Log Numstat file over a period of six months. Each line corresponds to a change to a source code file and contains the following content:
  - `ts_in_s`: the commit timestamp in seconds
  - `path`: The file path of the source code file
  - `add`: The number of lines added ("additions")
  - `del`: The number of deleted lines ("deletions")
- dataset URL: [`datasets/intellij_testing.csv`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/intellij_testing.csv)


## Under the hood
Data source: version control system  
Difficulty: medium  

### Problem Context
A customer management system for veterinary practices called PetClinic, written in Java, uses the JDBC (Java Database Connectivity) interface to access a database.
However, the enterprise architects have now determined that in the future all database access should be done via an object-relational mapping using the interface of JPA (Java Persistence API).
The development team must migrate the application from JDBC to JPA in addition to the normal feature development. 
The migration takes very long because many code passages have to be changed.
So the work has been dragging on for a long time now.
However, confidence on the part of product management seems to be slowly waning.

### Your Task
You would like to make the progress of the technology replacement transparent.
Visualize the respective amounts of code for the old and new libraries over time to show the progress of the migration.

### Additional Information

- The team has stored the code for the two interfaces (JDBC and JPA, respectively) in different Java packages (= directories) with the respective interface name.
- The source code is managed using the Git version control system.	
- The software project uses a Continuous Integration Server.

### Starters
- A (preprocessed) Git Log Numstat CSV file (~3 MB) with a Git Log Numstat output, which records the changes per line per file incl. changed number of lines of code.
- Dataset URL: [`datasets/db_api_refactoring.csv`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/db_api_refactoring.csv)


## Access Denied
Data sources: various kind of static and dynamic data
Difficulty: challenging  

### Problem Context
The internal insurance system "InsurHappy" is a web application that makes heavy use of mainframe operations.
However, sporadic authorization errors occur in the application when it is used.
It is suspected that individual access rights of individual users for the execution of COBOL routines are not available.
At the same time, mainframe administrators are very concerned that users are not given too many access rights. 

### Your Task
A list of missing user permissions is needed to show which reals users with which user ID needs which routines to work smoothly with InsurHappy. Create this list for the administrators!

### Starters
- The COBOL routines are wrapped by CICS transactions. These are defined in the file ([`datasets/access/TRANSACT.DEF`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/access/TRANSACT.DEF) and encoded with `EBCDIC 500` character set.
- The CICS transactions, in turn, are wired to the SOAP service methods via a mapping file. The definitions are in [`datasets/access/webservice_definition_v0.1.xml`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/access/webservice_definition_v0.1.xml) (for a simpler variant, see [`datasets/access/webservice_definition_v0.1.json`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/access/webservice_definition_v0.1.json)). These SOAP service methods are called by InsurHappy to communicate with the mainframe.
- There is a log file named [`datasets/access/calls.log`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/access/calls.log) from InsurHappy, which provides an overview of the services called in the past week.
- Furthermore, there is a so called "Access Matrix" ([`datasets/access/access_matrix.xlsx`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/access/access_matrix.xlsx)) which indicates which users are allowed to call which COBOL routines.
- In addition, a list of real names of users is available ([`datasets/access/user_list.csv`](https://raw.githubusercontent.com/feststelltaste/software-analytics-katas-de/master/datasets/access/user_list.csv) to break down user IDs
