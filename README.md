# OSD
Exercise DS.6.0
Todays exercise will consist of completing a partly done REST API application.

The skeleton application is to be forked from

https://codeberg.org/arosano/restapi.git

The Database sampleAPI.db
sqlite> .tables
city             country          user           
continent        countrylanguage

sqlite> .schema user
CREATE TABLE user (
        email varchar(64) unique not null,
        password blob not null,
        profile int not null default 99,
        bio text not null
);

sqlite> .schema continent
CREATE TABLE continent(
    name varchar(16) unique not null
);

sqlite> .schema country
CREATE TABLE country(
    code char(3) unique not null,
    name varchar(52) default null,
    continent varchar(16) not null,
    region varchar(26) default null,
    surfacearea float(10,2) not null default 0.0,
    indepyear int default null,
    population int not null default 0,
    lifeexpectancy float(3,1) default null,
    gnp float(10,2) default null,
    gnpold float(10,2) default null,
    localname varchar(45) default null,
    governmentform varchar(32) not null default '',
    headofstate varchar(32) default null,
    capital int default null,
    code2 char(2) unique not null,
    foreign key(continent) references continent(name)
);

sqlite> .schema city
CREATE TABLE city (
    name varchar(35) not null,
    countrycode char(3) not null,
    district varchar(20) default null,
    population int not null default 0,
    foreign key(countrycode) references country(code)
);

sqlite> .schema countrylanguage
CREATE TABLE countrylanguage (
    countrycode char(3) not null,
    language varchar(30) not null,
    isofficial boolean default 'false' not null,
    percentage float(4,1) not null default 0.0,
    primary key(countrycode, language),
    foreign key(countrycode) references country(code)
);

sqlite> select count(*) from user;
0
sqlite> select count(*) from continent;
7
sqlite> select count(*) from country;
239
sqlite> select count(*) from city;
4082
sqlite> select count(*) from countrylanguage;
991
Completion means:

In routes/users.js create whatever may be missing routes for
registering
logging in
Create controller function in controllersworld.js for adding a city to the database. Usage must require authentication, and admin privileges.
All reading and displaying of data must require authentication as at least a regular user.
Only an admin may change the entries in the user table ie change profiles. Controller functions must be in controllers.js
Logging in should mean receiving a token from the API server. You must rpobably save in in local storage, so that it can be used repeatedly until it’s expiration.

The architecture is MVC, Model-View-Controller. You must not change that.

Please keep the separation of functionality between the two routers.

This should probably be done in groups of two or three. Some research is expected. Take a couple of weeks to do it. And don’t forget that questions are welcome.