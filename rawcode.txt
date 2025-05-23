CREATE TABLE `lsoa` (
    `lsoa_code` VARCHAR(9),
    `lsoa_name` VARCHAR(30),
    PRIMARY KEY (`lsoa_code`)
);

CREATE TABLE `coordinates` (
    `location` VARCHAR(30),
    `longitude` DOUBLE(8, 6),
    `latitude` DOUBLE(8, 6),
    PRIMARY KEY (`location`)
);

CREATE TABLE `area` (
    `postcode` CHAR(8),
    `location` VARCHAR(30),
    FOREIGN KEY (`location`)
        REFERENCES `coordinates` (`location`),
    `lsoa_code` CHAR(9),
    FOREIGN KEY (`lsoa_code`)
        REFERENCES `lsoa` (`lsoa_code`),
    PRIMARY KEY (`postcode`)
);

CREATE TABLE `constabulary` (
    `constabulary_code` CHAR(3),
    `reported_by` VARCHAR(50),
    `falls_within` VARCHAR(50),
    PRIMARY KEY (`constabulary_code`)
);

CREATE TABLE `individual` (
    `criminal_name` CHAR(6),
    `full_name` VARCHAR(40),
    `gender` CHAR(1),
    `age_range` VARCHAR(10),
    `selfdefined_ethnicity` VARCHAR(40),
    `officerdefined_ethnicity` VARCHAR(40),
    PRIMARY KEY (`criminal_name`)
);

CREATE TABLE `stop_search` (
    `crime_id` CHAR(8),
    `criminal_name` CHAR(6),
    FOREIGN KEY (`criminal_name`)
        REFERENCES `individual` (`criminal_name`),
    `legislation` VARCHAR(50),
    `object_of_search` VARCHAR(40),
    `outcome_linked_to_object_of_search` BOOL,
    `removal_of_more_than_just_outer_clothing` BOOL,
    PRIMARY KEY (`crime_id`)
);

CREATE TABLE `crime` (
    `case_no` INT(10),
    `crime_id` CHAR(8),
    FOREIGN KEY (`crime_id`)
        REFERENCES `stop_search` (`crime_id`),
    `crime_type` VARCHAR(40),
    `date` DATETIME,
    `constabulary_code` CHAR(3),
    FOREIGN KEY (`constabulary_code`)
        REFERENCES `constabulary` (`constabulary_code`),
    `postcode` CHAR(8),
    FOREIGN KEY (`postcode`)
        REFERENCES `area` (`postcode`),
    `outcome` VARCHAR(100),
    `court_outcome` VARCHAR(100),
    PRIMARY KEY (`case_no`)
);

INSERT INTO lsoa (lsoa_code, lsoa_name) VALUES
('E01012607', 'Blackburn with Darwen 001A'),
('E01012608', 'Blackburn with Darwen 001B'),
('E01012633', 'Blackburn with Darwen 001C'),
('E01012634', 'Blackburn with Darwen 001D'),
('E01012663', 'Blackpool 001A'),
('E01012664', 'Blackpool 001B'),
('E01012665', 'Blackpool 001C'),
('E01012716', 'Blackpool 001D'),
('E01004888', 'Bolton 004C'),
('E01004789', 'Bolton 006D'),
('E01004780', 'Bolton 009B'),
('E01024859', 'Burnley 001A'),
('E01024861', 'Burnley 001B'),
('E01024862', 'Burnley 001C'),
('E01024891', 'Burnley 001D'),
('E01005016', 'Bury 001C'),
('E01004982', 'Bury 004E'),
('E01018651', 'Cheshire East 007F'),
('E01018539', 'Cheshire West and Chester 010C'),
('E01024951', 'Chorley 001A'),
('E01024952', 'Chorley 001B'),
('E01024953', 'Chorley 001C'),
('E01024954', 'Chorley 001D'),
('E01027576', 'Craven 004C'),
('E01027586', 'Craven 007D'),
('E01019332', 'Eden 003B'),
('E01024993', 'Fylde 001A'),
('E01025026', 'Flyde 001B'),
('E01025027', 'Flyde 001C'),
('E01025028', 'Flyde 001D'),
('E01012385', 'Halton 009A'),
('E01025060', 'Hyndburn 001A'),
('E01025061', 'Hyndburn 001B'),
('E01025062', 'Hyndburn 001C'),
('E01025063', 'Hyndburn 001D'),
('E01025088', 'Lancaster 001A'),
('E01025096', 'Lancaster 001B'),
('E01025097', 'Lancaster 001C'),
('E01025098', 'Lancaster 001D'),
('E01005255', 'Manchester 012D'),
('E01025191', 'Pendle 001A'),
('E01025192', 'Pendle 001B'),
('E01025193', 'Pendle 001C'),
('E01025194', 'Pendle 001D'),
('E01025278', 'Preston 001A'),
('E01025279', 'Preston 001B'),
('E01025282', 'Preston 001C'),
('E01025257', 'Preston 002A'),
('E01025315', 'Ribble Valley 001A'),
('E01025320', 'Ribble Valley 001B'),
('E01025331', 'Ribble Valley 001C'),
('E01025348', 'Ribble Valley 001D'),
('E01025355', 'Rossendale 001A'),
('E01025361', 'Rossendale 001B'),
('E01025362', 'Rossendale 001C'),
('E01025393', 'Rossendale 001D'),
('E01018236', 'South Cambridgeshire 002D'),
('E01019375', 'South Lakeland 001B'),
('E01019364', 'South Lakeland 004C'),
('E01025424', 'South Ribble 001A'),
('E01025425', 'South Ribble 001B'),
('E01025426', 'South Ribble 001C'),
('E01025466', 'South Ribble 001D'),
('E01025496', 'West Lancashire 001A'),
('E01025497', 'West Lancashire 001B'),
('E01025498', 'West Lancashire 001C'),
('E01025530', 'West Lancashire 001D'),
('E01006320', 'Wigan 003F'),
('E01006365', 'Wigan 018D'),
('E01025573', 'Wyre 001A'),
('E01025574', 'Wyre 001B'),
('E01025581', 'Wyre 001C'),
('E01025582', 'Wyre 001D');

INSERT INTO coordinates (location, longitude, latitude) VALUES
('Stone Hill Drive', -2.465978, 53.767257),
('Rowan Close', -2.464039, 53.766168),
('Kelsall Avenue', -2.462042, 53.762509),
('Fountains Avenue', -2.461766, 53.762222),
('Tintern Crescent', -2.46275, 53.763441),
('Sunny Bower Road', -2.46309, 53.768149),
('Philips Road', -2.458905, 53.762781),
('Challenge Way', -2.454236, 53.760282),
('Peridot Close', -2.474674, 53.770234),
('Gretna Road', -2.475607, 53.768253),
('Douglas Place', -2.473663, 53.768018),
('Brownhill Drive', -2.471547, 53.771433),
('Highbank', -2.471857, 53.769355),
('Beryl Avenue', -2.473358, 53.770572),
('Cornelian Street', -2.476635, 53.769282),
('Jasper Street', -2.476246, 53.768421),
('Lilac Road', -2.466822, 53.76409),
('Amber Avenue', -2.474098, 53.770335),
('Agate Street', -2.474237, 53.766514),
('Pearl Street', -2.476515, 53.769337),
('Whalley New Road North', -2.479301, 53.775527),
('Sports/Recreation Area', -2.486874, 53.769088),
('Whalley New Road South', -2.480452, 53.774058),
('Ruby Street', -2.478486, 53.770623),
('Emerald Street', -2.476979, 53.770171),
('Ramsgreave Drive', -2.486749, 53.771444),
('Pleckgate Road', -2.484754, 53.772063),
('Ramsgreave Avenue', -2.487489, 53.769778),
('Wilworth Crescent', -2.484873, 53.770588),
('Pemberton Street', -2.479576, 53.76768),
('Hill View', -2.481158, 53.765453),
('Outram Lane', -2.480381, 53.767829),
('North Bank Avenue', -2.483963, 53.76661),
('Rosewood Avenue', -2.476423, 53.765283),
('Buckden Close', -3.046372, 53.873648),
('Kelso Avenue West', -3.042794, 53.872889),
('Kelso Avenue East', -3.042435, 53.871912),
('Petrol Station', -3.043348, 53.871922),
('Alconbury Crescent', -3.04683, 53.874957),
('Maitland Avenue', -3.040654, 53.873105),
('Lyddesdale Avenue', -3.03942, 53.869952),
('Stoneway Road', -3.032112, 53.873952),
('Kew Grove', -3.036414, 53.871991),
('Keith Grove', -3.036264, 53.87148),
('Penswick Avenue', -3.029689, 53.871258),
('Vermont Grove', -3.030668, 53.867178),
('Springbrook Avenue', -3.027853, 53.867121),
('Brookdale Avenue', -3.03232, 53.867568),
('Neville Avenue', -3.032743, 53.869902),
('Anchorsholme Lane', -3.026883, 53.869727),
('Seabrook Drive', -3.028909, 53.867391),
('Redeswood Avenue', -3.035065, 53.868497),
('Glenarden Avenue', -3.027441, 53.867664),
('Gretna Crescent', -3.040081, 53.867178),
('Wilson Square', -3.041448, 53.86464),
('Parking Area', -3.04812, 53.857805),
('Micklegate', -3.044189, 53.863592);

INSERT INTO area (postcode, location, lsoa_code) VALUES
('BB0 1AA', 'Stone Hill Drive', 'E01012607'),
('BB0 1AB', 'Rowan Close', 'E01012607'),
('BB0 1AC', 'Kelsall Avenue', 'E01012607'),
('BB0 1AD', 'Fountains Avenue', 'E01012607'),
('BB0 1AE', 'Tintern Crescent', 'E01012607'),
('BB0 1AF', 'Sunny Bower Road', 'E01012607'),
('BB0 1AG', 'Philips Road', 'E01012607'),
('BB0 1AH', 'Challenge Way', 'E01012607'),
('BB0 1BA', 'Peridot Close', 'E01012608'),
('BB0 1BB', 'Gretna Road', 'E01012608'),
('BB0 1BC', 'Douglas Place', 'E01012608'),
('BB0 1BD', 'Brownhill Drive', 'E01012608'),
('BB0 1BE', 'Highbank', 'E01012608'),
('BB0 1BF', 'Beryl Avenue', 'E01012608'),
('BB0 1BG', 'Cornelian Street', 'E01012608'),
('BB0 1BH', 'Jasper Street', 'E01012608'),
('BB0 1BI', 'Lilac Road', 'E01012608'),
('BB0 1BJ', 'Amber Avenue', 'E01012608'),
('BB0 1BK', 'Agate Street', 'E01012608'),
('BB0 1BL', 'Pearl Street', 'E01012608'),
('BB0 1CA', 'Whalley New Road North', 'E01012633'),
('BB0 1CB', 'Sports/Recreation Area', 'E01012633'),
('BB0 1CC', 'Whalley New Road South', 'E01012633'),
('BB0 1CD', 'Ruby Street', 'E01012633'),
('BB0 1CE', 'Emerald Street', 'E01012633'),
('BB0 1CF', 'Ramsgreave Drive', 'E01012633'),
('BB0 1CG', 'Pleckgate Road', 'E01012633'),
('BB0 1CH', 'Ramsgreave Avenue', 'E01012633'),
('BB0 1CI', 'Wilworth Crescent', 'E01012633'),
('BB0 1DA', 'Pemberton Street', 'E01012634'),
('BB0 1DB', 'Hill View', 'E01012634'),
('BB0 1DC', 'Outram Lane', 'E01012634'),
('BB0 1DD', 'North Bank Avenue', 'E01012634'),
('BB0 1DE', 'Rosewood Avenue', 'E01012634'),
('FY0 1AA', 'Buckden Close', 'E01012663'),
('FY0 1AB', 'Kelso Avenue West', 'E01012663'),
('FY0 1AC', 'Kelso Avenue East', 'E01012663'),
('FY0 1AD', 'Petrol Station', 'E01012663'),
('FY0 1AE', 'Alconbury Crescent', 'E01012663'),
('FY0 1AF', 'Maitland Avenue', 'E01012663'),
('FY0 1AG', 'Lyddesdale Avenue', 'E01012663'),
('FY0 1BA', 'Stoneway Road', 'E01012664'),
('FY0 1BB', 'Kew Grove', 'E01012664'),
('FY0 1BC', 'Keith Grove', 'E01012664'),
('FY0 1CA', 'Penswick Avenue', 'E01012665'),
('FY0 1CB', 'Vermont Grove', 'E01012665'),
('FY0 1CC', 'Springbrook Avenue', 'E01012665'),
('FY0 1CD', 'Brookdale Avenue', 'E01012665'),
('FY0 1CE', 'Neville Avenue', 'E01012665'),
('FY0 1CF', 'Anchorsholme Lane', 'E01012665'),
('FY0 1CG', 'Seabrook Drive', 'E01012665'),
('FY0 1CH', 'Redeswood Avenue', 'E01012665'),
('FY0 1DA', 'Glenarden Avenue', 'E01012716'),
('FY0 1DB', 'Gretna Crescent', 'E01012716'),
('FY0 1DC', 'Wilson Square', 'E01012716'),
('FY0 1DD', 'Parking Area', 'E01012716'),
('FY0 1DE', 'Micklegate', 'E01012716');

INSERT INTO constabulary (constabulary_code, reported_by, falls_within) VALUES
('LNC', 'Lancashire Constabulary', 'Lancashire'),
('GMP', 'Greater Manchester Police', 'Greater Manchester'),
('CHC', 'Cheshire Constabulary', 'Cheshire'),
('MPS', 'Metropolitan Police Service', 'London Region'),
('PSC', 'Police Scotland', 'Scotland'),
('WMP', 'West Midlands Police', 'West Midlands'),
('PNI', 'Police Service of Northern Ireland', 'Northern Ireland'),
('WYP', 'West Yorkshire Police', 'West Yorkshire'),
('TVP', 'Thames Valley Police', 'Oxfordshire, Milton Keynes, Slough'),
('MSP', 'Merseyside Police', 'Merseyside'),
('KNP', 'Kent Police', 'Kent'), 
('ESP', 'Essex Police', 'Essex, Southend-On-Sea'),
('NBP', 'Northumbria Police', 'Tyne and Wear, Northumbria'),
('DCP', 'Devon and Cornwall Police', 'Devon and Cornwall, Plymouth, Torbay'),
('SWP', 'South Wales Police', 'Cardiff, Swansea, Talbot'),
('HIP', 'Hampshire and Isle of Wight Constabulary', 'Hampshire, Isle of Wight, Portsmouth, Southampton'),
('ASP', 'Avon and Somerset Police', 'Bath, Bristol, Somerset, Gloucestershire'),
('SSP', 'Sussex Police', 'Sussex, West Sussex, Brighton');

INSERT INTO individual (criminal_name, full_name, gender, age_range, selfdefined_ethnicity, officerdefined_ethnicity) VALUES
('SR0000', 'Sophie Reynolds', 'F', '25-34', 'White', 'White'),
('JH0000', 'Jamal Haines', 'M', 'Over 34', 'Black', 'Black'),
('AR0000', 'Alex Rodriguez', 'M', '18-24', 'Hispanic', 'Hispanic'),
('CW0000', 'Connor Williams', 'M', 'Under 18', 'White', 'White'),
('AP0000', 'Aisha Patel', 'F', '35-44', 'Asian', 'Asian'),
('LN0000', 'Leo Nguyen', 'M', '25-34', 'Asian', 'Asian'),
('MJ0000', 'Mia Johnson', 'F', '45-54', 'Black', 'Black'),
('OS0000', 'Olivia Smith', 'F', 'Over 54', 'White', 'White'),
/* These individuals below aren't linked to any crimes entries and are just testing/filler data */
('AM0000', 'Ava Martinez', 'F', 'Under 18', 'Hispanic', 'Hispanic'),
('EB0000', 'Elijah Brown', 'M', '35-44', 'Black', 'Carribean'),
('JT0000', 'Jordan Taylor', 'M', '25-34', 'White', 'White'),
('MG0000', 'Maya Gonzalez', 'F', '18-24', 'Hispanic', 'Hispanic'),
('LK0000', 'Liam Kim', 'M', '35-44', 'Asian', 'Asian'),
('ET0000', 'Emma Turner', 'F', 'Over 54', 'White', 'White'),
('CP0000', 'Caleb Patel', 'M', '45-54', 'Indian', 'Asian'),
('ZJ0000', 'Zoe Jackson', 'F', '25-34', 'Black', 'Black'),
('LC0000', 'Logan Chen', 'M', 'Under 18', 'Asian', 'Indian'),
('GD0000', 'Grace Davis', 'F', '35-44', 'White', 'White'),
('MR0000', 'Mason Rivera', 'M', 'Over 34', 'Hispanic', 'Hispanic'),
('AL0000', 'Aria Lee', 'F', '18-24', 'Asian', 'Asian'),
/* These individuals below aren't linked to any crimes entries OR stop search entries and are just testing/filler data */
('JS0000', 'John Smith', 'M', '25-34', 'Black', 'White and Black Carribean'),
('ED0000', 'Emily Davis', 'F', '35-44', 'Asian', 'Asian'),
('MJ0001', 'Michael Johnson', 'M', '18-24', 'Mixed', 'Asian'),
('JM0000', 'Jessica Miller', 'F', '45-54', 'White', 'White'),
('DS0000', 'Daniel Sutch', 'M', '55-64', 'Hispanic', 'Hispanic'),
('SL0000', 'Sophia Lee', 'F', '18-24', 'Asian', 'Chinese'),
('CB0000', 'Christopher Brown', 'M', '35-44', 'Black', 'Black'),
('OM0000', 'Olivia Martinez', 'F', '25-34', 'Mixed', 'White and Black Carribean'),
('MT0000', 'Matthew Taylor', 'M', '45-54', 'White', 'White'),
('YW0000', 'Yvonne Wilson', 'F', 'Under 18', 'Black', 'Black');

INSERT INTO stop_search (crime_id, criminal_name, legislation, object_of_search, outcome_linked_to_object_of_search, removal_of_more_than_just_outer_clothing) VALUES
('CR385012', 'SR0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Offensive weapons', TRUE, FALSE),
('CR384953', 'JH0000', 'Misuse of Drugs Act 1971 (section 23)', 'Controlled drugs', TRUE, TRUE),
('CR385065', 'AR0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Stolen goods', FALSE, FALSE),
('CR385199', 'CW0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Offensive weapons', TRUE, TRUE),
('CR385128', 'AP0000', 'Misuse of Drugs Act 1971 (section 23)', 'Controlled drugs', TRUE, FALSE),
('CR385317', 'LN0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Article for use in theft', TRUE, TRUE),
('CR385262', 'MJ0000', 'Misuse of Drugs Act 1971 (section 23)', 'Controlled drugs', FALSE, FALSE),
('CR385513', 'OS0000', 'Misuse of Drugs Act 1971 (section 23)', 'Controlled drugs', FALSE, FALSE),
/* Stop search cases below haven't been referenced in any crime entries and are just testing/filler data */
('CR385381', 'AM0000', NULL, NULL, FALSE, FALSE),
('CR385447', 'EB0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Article for use in theft', TRUE, FALSE),
('CR385578', 'JT0000', 'Misuse of Drugs Act 1971 (section 23)', 'Controlled drugs', TRUE, FALSE),
('CR385643', 'MG0000', 'Firearms Act 1968 (section 47)', 'Firearms', FALSE, FALSE),
('CR385712', 'LK0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Article for use in theft', TRUE, FALSE),
('CR385782', 'ET0000', 'Misuse of Drugs Act 1971 (section 23)', 'Controlled drugs', TRUE, FALSE),
('CR385853', 'CP0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Offensive weapons', FALSE, FALSE),
('CR385924', 'ZJ0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Offensive weapons', TRUE, TRUE),
('CR385995', 'LC0000', NULL, NULL, FALSE, FALSE),
('CR386067', 'GD0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Offensive weapons', TRUE, TRUE),
('CR386141', 'MR0000', 'Police and Criminal Evidence Act 1984 (section 1)', 'Stolen goods', FALSE, FALSE),
('CR386215', 'AL0000', 'Misuse of Drugs Act 1971 (section 23)', 'Controlled drugs', TRUE, TRUE);

INSERT INTO crime (case_no, crime_id, crime_type, date, constabulary_code, postcode, outcome, court_outcome) VALUES
(1, NULL, 'Violence and sexual offences', '2022-01-01 12:00:00', 'LNC', 'BB0 1AA', 'Under investigation', NULL),
(2, NULL, 'Vehicle crime', '2022-01-02 14:30:00', 'LNC', 'BB0 1AB', 'Awaiting court outcome', 'Suspect charged'),
(3, 'CR385012', 'Possession of weapons', '2022-01-03 16:45:00', 'LNC', 'BB0 1AC', 'Offender given penalty notice', NULL),
(4, NULL, 'Anti-social behaviour', '2022-01-04 18:20:00', 'LNC', 'FY0 1AA', NULL, NULL),
(5, 'CR384953', 'Drugs', '2022-01-05 20:10:00', 'LNC', 'FY0 1AB', 'Offender given a caution', NULL),
(6, NULL, 'Other crime', '2022-01-06 10:05:00', 'LNC', 'BB0 1AE', 'Under investigation', NULL),
(7, NULL, 'Criminal damage and arson', '2022-01-07 11:45:00', 'LNC', 'BB0 1AF', 'Local resolution', NULL),
(8, NULL, 'Burglary', '2022-01-08 13:30:00', 'LNC', 'BB0 1AG', 'Action to be taken by another organisation', NULL),
(9, NULL, 'Public order', '2022-01-09 15:20:00', 'LNC', 'BB0 1AH', 'Awaiting court outcome', NULL),
(10, NULL, 'Bicycle theft', '2022-01-10 17:10:00', 'LNC', 'BB0 1BA', 'Offender given a caution', NULL),
(11, 'CR385065', 'Shoplifting', '2022-01-11 19:00:00', 'LNC', 'FY0 1AA', 'Unable to prosecute suspect', NULL),
(12, NULL, 'Other theft', '2022-01-12 21:30:00', 'LNC', 'FY0 1AB', 'Awaiting court outcome', 'Defendant found not guilty'),
(13, NULL, 'Robbery', '2022-01-13 23:15:00', 'LNC', 'FY0 1AC', 'Offender given a caution', NULL),
(14, NULL, 'Violence and sexual offences', '2022-01-14 12:00:00', 'LNC', 'BB0 1AD', 'Local resolution', NULL),
(15, NULL, 'Vehicle crime', '2022-01-15 14:30:00', 'LNC', 'BB0 1AE', 'No suspect identified', NULL),
(16, 'CR385199', 'Possession of weapons', '2022-01-16 16:45:00', 'LNC', 'BB0 1AF', 'Awaiting court outcome', 'Defendant sent to Crown Court'),
(17, NULL, 'Anti-social behaviour', '2022-01-17 18:20:00', 'LNC', 'BB0 1AG', NULL, NULL),
(18, 'CR385128', 'Drugs', '2022-01-18 20:10:00', 'LNC', 'BB0 1AH', 'Under investigation', NULL),
(19, NULL, 'Other crime', '2022-01-19 10:05:00', 'LNC', 'BB0 1BA', 'Offender given penalty notice', NULL),
(20, NULL, 'Criminal damage and arson', '2022-01-20 11:45:00', 'LNC', 'BB0 1BB', 'Under investigation', NULL),
(21, NULL, 'Burglary', '2022-01-21 13:30:00', 'LNC', 'BB0 1BC', 'Action to be taken by another organisation', NULL),
(22, NULL, 'Public order', '2022-01-22 15:20:00', 'LNC', 'BB0 1BD', 'Offender given a caution', NULL),
(23, 'CR385317', 'Bicycle theft', '2022-01-23 17:10:00', 'LNC', 'BB0 1BE', 'Local resolution', NULL),
(24, NULL, 'Shoplifting', '2022-01-24 19:00:00', 'LNC', 'BB0 1BF', 'Offender given a caution', NULL),
(25, NULL, 'Other theft', '2022-01-25 21:30:00', 'LNC', 'BB0 1BG', 'Awaiting court outcome', NULL),
(26, NULL, 'Robbery', '2022-01-26 23:15:00', 'LNC', 'BB0 1BH', 'Offender given penalty notice', NULL),
(27, NULL, 'Violence and sexual offences', '2022-01-27 12:00:00', 'LNC', 'BB0 1BI', 'Under investigation', NULL),
(28, NULL, 'Vehicle crime', '2022-01-28 14:30:00', 'LNC', 'BB0 1BJ', 'Action to be taken by another organisation', NULL),
(29, NULL, 'Possession of weapons', '2022-01-29 16:45:00', 'LNC', 'BB0 1BK', 'No suspect identified', NULL),
(30, NULL, 'Anti-social behaviour', '2022-01-30 18:20:00', 'LNC', 'BB0 1BL', NULL, NULL),
(31, 'CR385262', 'Drugs', '2022-01-31 20:10:00', 'LNC', 'BB0 1CA', 'Nothing found - no further action', NULL),
(32, NULL, 'Other crime', '2022-02-01 10:05:00', 'LNC', 'BB0 1CB', 'Awaiting court outcome', 'Offender given conditional discharge'),
(33, NULL, 'Criminal damage and arson', '2022-02-02 11:45:00', 'LNC', 'BB0 1CC', 'No suspect identified', NULL),
(34, NULL, 'Burglary', '2022-02-03 13:30:00', 'LNC', 'BB0 1CD', 'Offender given penalty notice', NULL),
(35, NULL, 'Public order', '2022-02-04 15:20:00', 'LNC', 'BB0 1CE', 'Awaiting court outcome', 'Court case unable to proceed'),
(36, NULL, 'Bicycle theft', '2022-02-05 17:10:00', 'LNC', 'BB0 1CF', 'Action to be taken by another organisation', NULL),
(37, NULL, 'Shoplifting', '2022-02-06 19:00:00', 'LNC', 'BB0 1CG', 'No suspect identified', NULL),
(38, 'CR385513', 'Drugs', '2022-02-07 21:30:00', 'LNC', 'BB0 1CH', 'Offender given a caution', NULL),
(39, NULL, 'Robbery', '2022-02-08 23:15:00', 'LNC', 'BB0 1CI', 'Local resolution', NULL),
(40, NULL, 'Violence and sexual offences', '2022-02-09 12:00:00', 'LNC', 'BB0 1DA', 'Awaiting court outcome', 'Offender sent to prison');

/* QUERIES */

/* SELECT QUERIES */

	/* Retrieve the names of individuals involved in stop searches along with the associated crime type and location. */
	SELECT i.criminal_name, s.crime_id, s.legislation, s.object_of_search, c.crime_type, a.location
	FROM individual i
	JOIN stop_search s ON i.criminal_name = s.criminal_name
	JOIN crime c ON s.crime_id = c.crime_id
	JOIN area a ON c.postcode = a.postcode;
    
    /* Retrieve the distinct crime types recorded in the database */
    SELECT DISTINCT crime_type
	FROM crime;
    
    /* Retrieve the names of individuals involved in stop search crimes along with the corresponding constabulary names and stop search outcomes. */
    SELECT i.criminal_name, c.reported_by, s.outcome_linked_to_object_of_search
	FROM individual i
	JOIN stop_search s ON i.criminal_name = s.criminal_name
	JOIN crime cr ON s.crime_id = cr.crime_id
	JOIN constabulary c ON cr.constabulary_code = c.constabulary_code;
    
    /* Show the most latest crimes at the top */
    SELECT * FROM crime
    ORDER BY date DESC;
    
/* UPDATE QUERIES */

	/* Update the reported_by field in the constabulary table for a specific constabulary_code. */
	UPDATE constabulary
	SET reported_by = 'Updated Constabulary Name'
	WHERE constabulary_code = 'LNC';

	/* Update the outcome of stop searches where the object of search is a person to indicate if any contraband was found. */
	UPDATE stop_search
	SET outcome_linked_to_object_of_search = TRUE
	WHERE object_of_search = 'Firearms';

/* DELETE QUERIES */

	/* Delete stop search records where the outcome_linked_to_object_of_search is FALSE. */
	DELETE FROM crime
	WHERE crime_id IN (
		SELECT crime_id
		FROM stop_search
		WHERE outcome_linked_to_object_of_search = FALSE
	);

	DELETE FROM stop_search
	WHERE outcome_linked_to_object_of_search = FALSE;
    
    /* Re-add data from above that was deleted */
    INSERT INTO stop_search (crime_id, criminal_name, legislation, object_of_search, outcome_linked_to_object_of_search, removal_of_more_than_just_outer_clothing) VALUES
    ('CR385065', 'Alex Rodriguez', 'Stolen Property', 'Bag', FALSE, FALSE),
    ('CR385262', 'Mia Johnson', 'Drugs', 'Person', FALSE, FALSE),
	('CR385513', 'Ava Martinez', 'Stolen Property', 'Person', FALSE, FALSE),
    ('CR385381', 'Olivia Smith', 'Drugs', 'Car', FALSE, FALSE),
    ('CR385643', 'Maya Gonzalez', 'Weapons', 'Car', FALSE, FALSE),
    ('CR385853', 'Caleb Patel', 'Weapons', 'Person', FALSE, FALSE),
    ('CR385995', 'Logan Chen', 'Drugs', 'Person', FALSE, FALSE),
    ('CR386141', 'Mason Rivera', 'Stolen Property', 'Person', FALSE, FALSE);
    
    INSERT INTO crime (case_no, crime_id, crime_type, date, constabulary_code, postcode, outcome, court_outcome) VALUES
    (11, 'CR385065', 'Shoplifting', '2022-01-11 19:00:00', 'LNC', 'FY0 1AA', 'Unable to prosecute suspect', NULL),
	(31, 'CR385262', 'Drugs', '2022-01-31 20:10:00', 'LNC', 'BB0 1CA', 'Offender given a caution', NULL),
    (38, 'CR385513', 'Other theft', '2022-02-07 21:30:00', 'LNC', 'BB0 1CH', 'Offender given a caution', NULL);
    
    /* Delete all records of individuals who have not been involved in any stop searches. */
    DELETE FROM individual
	WHERE criminal_name NOT IN (
		SELECT DISTINCT criminal_name
		FROM stop_search
	);
    
    /* Re-add data from above that was deleted */
    INSERT INTO individual (criminal_name, gender, age_range, selfdefined_ethnicity, officerdefined_ethnicity) VALUES
	('John Smith', 'M', '25-34', 'Black', 'Black'),
	('Emily Davis', 'F', '35-44', 'Asian', 'Asian'),
	('Michael Johnson', 'M', '18-24', 'Mixed', 'Asian'),
	('Jessica Miller', 'F', '45-54', 'White', 'White'),
	('Daniel Sutch', 'M', '55-64', 'Hispanic', 'Hispanic'),
	('Sophia Lee', 'F', '18-24', 'Asian', 'Chinese'),
	('Christopher Brown', 'M', '35-44', 'Black', 'Black'),
	('Olivia Martinez', 'F', '25-34', 'Mixed', 'Mixed'),
	('Matthew Taylor', 'M', '45-54', 'White', 'White'),
	('Yvonne Wilson', 'F', 'Under 18', 'Black', 'Black');
    
/* GROUP BY QUERIES */

	/* Calculate the average age of individuals involved in crimes, grouped by crime type. */
    SELECT c.crime_type, 
		AVG(CASE
			WHEN i.age_range = 'under 18' THEN 16
		    WHEN i.age_range = '18-24' THEN 22.5
		    WHEN i.age_range = '25-34' THEN 29.5
            WHEN i.age_range = '35-44' THEN 39.5
            WHEN i.age_range = '45-54' THEN 49.5
			WHEN i.age_range = 'Over 54' THEN 65
			ELSE 0  -- Default value if age range is not recognized
		END) AS average_age
	FROM crime c
	JOIN stop_search s ON c.crime_id = s.crime_id
	JOIN individual i ON s.criminal_name = i.criminal_name
	GROUP BY c.crime_type;

/* SUBQUERIES */

	/* Find the crimes where the reported constabulary falls within the 'Greater Manchester Police' region. */
    SELECT c.case_no, c.crime_type, c.date, co.reported_by
	FROM crime c
	JOIN constabulary co ON c.constabulary_code = co.constabulary_code
	WHERE co.falls_within = 'Greater Manchester Police';

