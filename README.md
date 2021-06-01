# Working-HIVE
Complete installation and using Hadoop, hive and basic commands.

## HADOOP

### These softwares should be installed before using hive.

* Download Hadoop 2.8.0 
* Java JDK 1.8.0.zip 


#### Java is downloaded from the link:

https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html


#### Hadoop is downloaded from the link:

https://hadoop.apache.org/release/2.8.0.html

### Set Path

* Set the path HADOOP_HOME Environment variable on windows 7 as “C:\Hadoop-2.8.0\bin".

* Set the path JAVA_HOME Environment variable on windows 7 as C:\Java\bin".

### Creation of folders

* Create folder “data” under “C:\Hadoop-2.8.0”
* Create folder “datanode” under “C:\Hadoop-2.8.0\data”
* Create folder “namenode” under “C:\Hadoop-2.8.0\data”

## START HADOOP

Open cmd and change directory to “C:\Hadoop-2.8.0\sbin” and type 
“start-all.cmd” 

## HIVE
### Install derby by the following link:

https://archive.apache.org/dist/db/derby/db-derby-10.12.1.1/

### Install hive by the following link:

https://archive.apache.org/dist/hive/hive-2.1.0/

### Set path

* set DERBY_HOME="C:/dreby/bin"

* set HIVE_HOME="C:/hive/bin"

### Start Hive

* Start the cmd ,change the directory to c:/derby/bin and run the command: startNetworkServer -h 0.0.0.0

* Start the cmd, change the directory to c:/hive/bin and run the command: hive

## WORKING WITH HIVE

### HIVE QUERIES

### CREATE DATABASE:

* Create database project;
* Use project;

### CREATE TABLE:

* CREATE TABLE vaccine (entity string, code string, day date,total_vaccinations_per_hundred float) row format delimited fields terminated by ',';

* CREATE TABLE peoplevaccine (entity string, code string, day date,people_vaccinated double) row format delimited fields terminated by ',';

### LOADING THE DATA INTO THE TABLE:

* LOAD DATA LOCAL INPATH 'C:\Users\sasi\hive\covid-vaccination.csv' OVERWRITE INTO TABLE vaccine;

 * LOAD DATA LOCAL INPATH 'C:\Users\sasi\hive\people-vaccinated.csv' OVERWRITE INTO TABLE peoplevaccine;


### DESCRIBE THE TABLE:
* describe vaccine
* describe peoplevaccine


### PARTITIONS:

* create table part_vaccine(entity string, day date, total_vaccination_per_hundred float) partitioned by(code string);

hive> load data local inpath 'C:\Users\sasi\hive\covid-vaccination.csv' into table part_vaccine
. . > partition(code = "AFG");

### VIEWS:

create view vaccine_1cr as
. . > select * from peoplevaccine
. . > where people_vaccinated>700000;

### JOINS

#### INNER JOIN

select v.code,v.total_vaccinations_per_hundred,p.code,p.people_vaccinated from vaccine v join peoplevaccine p on (v.code=p.code);

#### LEFT OUTER JOIN

select v.code,v.total_vaccinations_per_hundred,p.code,p.people_vaccinated from vaccine v left outer join peoplevaccine p on (v.code=p.code);

#### RIGHT OUTER JOIN

select v.code,v.total_vaccinations_per_hundred,p.code,p.people_vaccinated from vaccine v right outer join peoplevaccine p on (v.code=p.code);

#### FULL OUTER JOIN

select v.code,v.total_vaccinations_per_hundred,p.code,p.people_vaccinated from vaccine v full outer join peoplevaccine p on (v.code=p.code);

### SELECTION(CLUSTER BY,DISTRIBUTE BY==SORT BY)

1. SHOW DATABASES;
2. SHOW TABLES;
3. SELECT * FROM part_vaccine;
4. SELECT * FROM vaccine;
5. SELECT * FROM peoplevaccine;
6. SELECT * FROM vaccine SORT BY code DESC;
7. SELECT code,people_vaccinated FROM peoplevaccine CLUSTER BY day;
8. SELECT TYPE,COUNT(*) FROM vaccine GROUP BY code;
9. SELECT code,day FROM peoplevaccine DISTRIBUTE BY people_vaccinated;


### ALTER:

ALTER TABLE HOSPITAL RENAME TO HOSPITALS; 

##### Refer the installation file for more details on configuration files and errors.
