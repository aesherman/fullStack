## Logs Analysis Project - Udacity Full Stack Web Developer Nanodegree - Andrew Sherman

#### DESCRIPTION
For this project, my task was to create a reporting tool that prints out reports( in plain text) based on the data in the given database. This reporting tool is a Python program using the `psycopg2` module to connect to the database. This project sets up a mock PostgreSQL database for a fictional news website. The provided Python script uses the psycopg2 library to query the database and produce a report that answers the following three questions:

1. What are the most popular three articles of all time?
2. Who are the most popular article authors of all time?
3. On which days did more than 1% of requests lead to errors?

##  How to access the project?

Follow the steps below to access the code of this project:

 1. If you don't already have the latest version of python download it from the link in requirements.
 2. Download and install Vagrant and VirtualBox.
 3. Download this Udacity [folder](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/59822701_fsnd-virtual-machine/fsnd-virtual-machine.zip) with preconfigured vagrant settings.
 4. Clone this repository.
 5. Download [this](https://d17h27t6h515a5.cloudfront.net/topher/2016/August/57b5f748_newsdata/newsdata.zip) database.
 6. Navigate to the Udacity folder in your bash interface and inside that cd into the vagrant folder.
 7. Open Git Bash and launch the virtual machine with`vagrant up`
 8. Once Vagrant installs necessary files use `vagrant ssh` to continue.
 9. The command line will now start with vagrant. Here cd into the /vagrant folder.
 10. Unpack the  database folder contents downloaded above over here. You can also copy the contents of this repository here.
 11.  To load the database type `psql -d news -f newsdata.sql`
 12. To run the database type `psql -d news`
 13. You must run the commands from the Create views section here to run the python program successfully.
 14. Use command `python log-results.py` to run the python program that fetches query results.

##  Create Views

Views were created to answer the third query in the project with the purpose of leaving the original database unchanged. They also helped break the question down into comprehensible portions.

The first view code is as follows:

    CREATE VIEW logstar AS
    SELECT count(*) as stat, 
    status, cast(time as date) as day
    FROM log WHERE status like '%404%'
    GROUP BY status, day
    ORDER BY stat desc limit 3;

The second view code is as follows:

    CREATE VIEW totalvisitors AS
    SELECT count(*) as visitors,
    cast(time as date) as errortime
    FROM log
    GROUP BY errortime;

The third and last view code is as follows:

    CREATE VIEW errorcount AS
    SELECT * from logstar join totalvisitors
    ON logstar.day = totalvisitors.errortime;








