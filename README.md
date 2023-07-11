# AJtopaz.github.co

CREATE TABLE TripData
(ride_id VARCHAR(255), rideable_type VARCHAR(255), started_at VARCHAR (255), ended_at VARCHAR (255), start_station_name VARCHAR(255)
, start_station_id VARCHAR (255), end_station_name VARCHAR (255), end_station_id VARCHAR (255), start_lat INT, start_lng INT
, end_lat INT, end_lng INT, member_casual VARCHAR(255) ) ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202101-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202102-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202101-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202103-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202101-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202101-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202105-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';


LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202104-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';


SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202106-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202108-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202106-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202109-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202110-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202111-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT count(*)
FROM portfolioproject.tripdata ;

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\202112-divvy-tripdata.csv'
INTO TABLE portfolioproject.tripdata
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

SELECT *
FROM portfolioproject.tripdata ;

SELECT end_station_name, start_station_name
FROM portfolioproject.tripdata
WHERE end_station_name = ''
   AND start_station_name = '' ;
   
DELETE 
FROM portfolioproject.tripdata
WHERE end_station_name = ''
   AND start_station_name = '' ;
   
   
SELECT *
FROM portfolioproject.tripdata ;

SELECT *
FROM portfolioproject.tripdata
WHERE end_station_name = ''
 AND end_station_id = '' ;
 
DELETE
FROM portfolioproject.tripdata
WHERE end_station_name = ''
 AND end_station_id = '' ;
 
SELECT COUNT(*)
FROM portfolioproject.tripdata ;

SELECT 
substring_index(started_at,' ', 1) AS YearDate
, substring_index(Substring_index(started_at,' ', -1),' ', 1) AS TimeDate
From portfolioproject.tripdata ;

ALTER TABLE tripdata
ADD YearsplitDate date; 

UPDATE tripdata
SET  YearsplitDate = substring_index(started_at,' ', 1);

ALTER TABLE tripdata
ADD TimesplitDate Date; 

ALTER TABLE tripdata
DROP COLUMN TimesplitDate ;

ALTER TABLE tripdata
ADD TimesplitDate time; 

UPDATE tripdata
SET  TimesplitDate = substring_index(Substring_index(started_at,' ', -1),' ', 1);

SET PERSIST innodb_lock_wait_timeout = 150;


SELECT 
substring_index(ended_at,' ', 1) AS EYearDate
, substring_index(Substring_index(ended_at,' ', -1),' ', 1) AS ETimeDate
From portfolioproject.tripdata ;

ALTER TABLE tripdata
ADD EndedYearsplitDate date; 

UPDATE tripdata
SET  EndedYearsplitDate = substring_index(ended_at,' ', 1) ;

ALTER TABLE tripdata
ADD EndedTimesplitDate time; 

UPDATE tripdata
SET  EndedTimesplitDate =  substring_index(Substring_index(ended_at,' ', -1),' ', 1);

SELECT *
FROM portfolioproject.tripdata ;

SELECT SUBTIME(EndedTimeSplitDate, TimesplitDate) AS Ridelength
FROM portfolioproject.tripdata ;

ALTER TABLE tripdata
ADD Ridelength time ;

UPDATE tripdata
SET  Ridelength = SUBTIME(EndedTimeSplitDate, TimesplitDate);

SELECT *
FROM portfolioproject.tripdata
WHERE Ridelength <= '00:00:00' ;

DELETE 
FROM portfolioproject.tripdata
WHERE Ridelength <= '00:00:00' ;

SELECT MAX(Ridelength)
FROM portfolioproject.tripdata ;

ALTER TABLE portfolioproject.tripdata 
DROP COLUMN started_at ;

ALTER TABLE portfolioproject.tripdata 
DROP COLUMN ended_at ;

SELECT *
FROM portfolioproject.tripdata ;

SELECT weekday(YearsplitDate) AS WEEKDAY
FROM portfolioproject.tripdata ;

ALTER TABLE tripdata
ADD WEEKDAY int ;

ALTER TABLE tripdata
DROP COLUMN  WEEKDAY  ;

ALTER TABLE tripdata
ADD WEEKDAY int ; 

UPDATE tripdata
SET  WEEKDAY = weekday(YearsplitDate) ; 

SELECT WEEKDAY,
CASE WHEN WEEKDAY = 0 THEN 'Monday'
	 WHEN WEEKDAY = 1 THEN 'Tuesday'
     WHEN WEEKDAY = 2 THEN 'Wednesday'
     WHEN WEEKDAY = 3 THEN 'Thursday'
     WHEN WEEKDAY = 4 THEN 'Friday'
	 WHEN WEEKDAY = 5 THEN 'Saturday'
	 WHEN WEEKDAY = 6 THEN 'Sunday'
    ELSE WEEKDAY
    END AS DayOfWeek
FROM portfolioproject.tripdata ;

ALTER TABLE tripdata
ADD DayofWeek varchar(255) ; 

UPDATE tripdata
SET  DayofWeek = CASE WHEN WEEKDAY = 0 THEN 'Monday'
	 WHEN WEEKDAY = 1 THEN 'Tuesday'
     WHEN WEEKDAY = 2 THEN 'Wednesday'
     WHEN WEEKDAY = 3 THEN 'Thursday'
     WHEN WEEKDAY = 4 THEN 'Friday'
	 WHEN WEEKDAY = 5 THEN 'Saturday'
	 WHEN WEEKDAY = 6 THEN 'Sunday'
    ELSE WEEKDAY
    END ; 


##How to export files
/* Add column headers */
SELECT 'ride_id', 'rideable_type', 'start_station_name', 'start_station_id', 'end_station_name', 'end_station_id', 
'start_lat', 'start_lng','end_lat','end_lng', 'member_casual', 'YearsplitDate', 'TimesplitDate', 'EndedYearssplitDate',
'EndedTimesplitDate', 'Ridelength', 'DayofWeek'
UNION ALL
SELECT ride_id, rideable_type, start_station_name, start_station_id, end_station_name, end_station_id, 
start_lat, start_lng, end_lat, end_lng, member_casual, YearsplitDate, TimesplitDate, EndedYearsplitDate,
EndedTimesplitDate, Ridelength, DayofWeek
FROM portfolioproject.tripdata
INTO OUTFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\tripdata7.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

