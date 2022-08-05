# Portfolio-Project
**Basic To Advance SQL Query**

**Note:- Use SQL Server for the result **

--DDL= Data deffination Language----
-------*******************--------------

create database test

use test

drop table employee

--no rollback in truncate command it permantly delete all the entry in the table 
truncate table employee2

create table employee
( Employee_ID int,
First_Name Varchar (100) Not Null,
Last_Name varchar (100) not null,
Age int );
constraint emppk primary key (Employee_ID)
);

alter table employee add marital_status varchar (100); --(add column)
alter table employee drop column marital_status -- (drop column field in the table)
alter table employee alter column Employee_ID char (100) -- (change caracter of the column)
alter table employee add salary numeric (10,2)

-- externally add primary key in table
alter table employee add constraint emppkk primary key (First_Name)

-----foreign key-----------------------------
create table Product
(
product_ID int primary key,
product_Name varchar(255),
category varchar (255)
);

create table Orders
(
orders_ID int primary key,
product_ID int not null,
quantity int

);

--if we want to delete the table then error will find or *on delete cascade* will prevent it 
alter table Orders add 
constraint abc foreign key (product_ID) references Product (product_ID) 
on delete cascade


-------------**************************------------------
--DML = Data manipulation Language

--Insert command
insert into employee values (1,'lsd', 'rsfd', 91)
insert into employee values (2,'ksd', 'gsfd', 31)
insert into employee values (3,'tsd', 'wsfd', 81)
insert into employee values (4,'hsd', 'asfd', 61)
insert into employee values (5,'dsd', 'nsfd', 51)
insert into employee values (6,'kg', 'nsfd', 51)
insert into employee values (7,'are', 'fjg', 51)

-- if we want to ***add data from another table*** 
insert into employee2 (Employee_ID, First_Name, Last_Name, Age)
(select * from employee)

-- if we want to **add some specfic data**
insert into employee2 (Employee_ID, First_Name, Last_Name, Age)
(select * from employee where Age > 40)

--Update Command
--- for **updating** the data in table---(where is mandatory)
update employee set Last_Name = 'paua' where Age = 91

--- Delete Statement we can retreave data to give rollback in command before delete command excuate
--if we want to deleting the record 
delete from employee2 where Age =31

--------------------------Select Statement-------------------------------------------------
select * from employee
select top 3 * from employee

--select only spacific 
select top 2 Last_Name from employee

--change field name
select Age as agee from employee

-- stop showing distinct values(duplicate)
select distinct Age from employee2

--order by condition
select distinct Age from employee2 order by Age desc

--------Logical Operators (and, or, not)--------
--and
select * from employee2 where Age = 51 and First_Name = 'dsd'
--or
select * from employee2 where Age = 51 or First_Name = 'dsd'
--not
select * from employee2 where Age not in (51)

---------- comparison operators--------
--between
select * from employee2 where Age between 40 and 70

--like start with d
select * from employee2 where First_Name like 'd%'

---case expression
select case (Age)
when 59 then 50
when 31 then 30
else 00
end
from employee2

------------------------Joint command---------
create table emp
(
Employee_ID int primary key,
Firstname varchar (255),
lastname varchar (255),
address varchar(255)
);

create table Orders1
(
orders_ID int primary key,
Employee_ID int,
quantity int

);

insert into emp values(101, 'Prabhanshu', 'Neekhara', 'Mumbai')
insert into emp values(102, 'Ram', null, 'Bangalore') 
insert into emp values(103, 'Shyam', 'sharma', 'Indore') 
insert into emp values(104, 'Radha', 'jain', 'Bihar') 
insert into emp values(105, 'Rajesh', 'suman', 'Bhopal') 
insert into emp values(106, 'Priyanshi', 'Neekhara', 'Mumbai') 
insert into emp values(107, 'Prabhu', 'Neekhara', 'Bangalore') 

alter table Orders1 drop column quantity
alter table Orders1 add Orderdate date

insert into Orders1 values(1, 101, '2020/02/06') 
insert into Orders1 values(2, 102, '2020-03-10') 
insert into Orders1 values(3, 103, '2020-03-19') 
insert into Orders1 values(4, 106, '2020-03-22') 
insert into Orders1 values(5, 105, '2020-03-29') 
insert into Orders1 values(6, null , '2020-04-05') 

select * from Orders1
select * from emp

--inner join--
select emp.Employee_ID, Orders1.orders_ID, Orders1.Orderdate
from emp
inner join Orders1
on emp.Employee_ID = Orders1.Employee_ID
order by emp.Employee_ID desc

----Left outer join---------
select emp.Employee_ID, Orders1.orders_ID, Orders1.Orderdate
from emp
left join Orders1
on emp.Employee_ID = Orders1.Employee_ID

--Right outer join -----
select emp.Employee_ID, Orders1.orders_ID, Orders1.Orderdate
from emp
Right join Orders1
on emp.Employee_ID = Orders1.Employee_ID

--full outer joins----
select emp.Employee_ID, Orders1.orders_ID, Orders1.Orderdate
from emp
full outer join Orders1
on emp.Employee_ID = Orders1.Employee_ID

--------cross joins-------
select emp.Employee_ID, Orders1.orders_ID, Orders1.Orderdate
from emp
cross join Orders1

-------****conversion Function**----------
--cast ---------- convert-----
select CAST('10' as int) * 20 as cast_ver
, convert(int, '10') * 20 as covert_ver

--is the error shown so we can use try function--------
select TRY_CAST('A' as int) as cast_ver

---------logical functions--------
--choose---
select choose (3, 'test','zet','bat','cat','dad','pad') --in SQL Values is starting with 1 not 0

-- iif function --
select iif(1>10, 'True', 'Fales') as abc 

------------Math functions-------
--abs values
select abs(-10)
--Random values
select rand()
--exponential values
select exp(4)
--floor
select floor(5.8)
--ceiling--
select ceiling (4.78)
--sqrt--
select sqrt(6.87)
--square--
select square(4)
--power 
select power(4,6)
--round
select round(4.8678,2)

----------aggregate functions
--avg--
select avg(distinct Employee_ID) from emp

--count
select count(distinct Employee_ID) from emp

--min
select min(distinct Employee_ID) from emp

--max
select max(distinct Employee_ID) from emp


---------String Functions-------------
---reverse
select reverse('abcd')

--Ltrim
select ltrim('			asasd')

---rtrim
select rtrim ('qdqs			')

--trim
select trim(		'gsduyhag'		)

--replace 
select replace('fssuaygdhg','ss', 'xx')

--substring--
select SUBSTRING('abcdef',3,5)

--Left
select left('abcdef',2)

--rignt
select right('abcdef',3)

--upper
select upper('sgfiuhas')

--Lower
select lower('ADSAHDFDS')

--length
select len('dscdwfcwdvcd')

-------------------------------Date function---------------
--sysdatetime
select SYSDATETIME()

--current_timestamp
select current_timestamp

--datepart
select datepart(year, '12-oct-2009')
select datepart(mm, '12-oct-2009')

--datediff
select datediff(mm, '12-oct-2009','21-nov-2020')

-----------------group by ---------------------
select * from employee2
--Group by
select Employee_ID, count (*) as count from employee2 
group by Employee_ID	


--Having
select Age, count(*) from employee2
group by Age
having min(Age)>30


------------------Transaction Control Language-------------
/*commit
Rollback
savepoint*/

--commit command = it is use to save the changes made in the table permanently
begin transaction
delete from employee2 where	Age = '91' 
commit 

--Rollback command = it is used to get back in permanent status (Note: table can be rollback only if its temprary. if you commit no rollback applied) 
begin transaction
delete from employee2 where	Age = '31' 
rollback
select * from employee2

update employee2 set Age = Age+2

--(set implicit transaction on) for implicit commint
--(Begin transaction) for explicit commit
-- savepoint command = (bookmark) use along with the Rollback command it is used to mark the transaction in a table a transaction can be named usind this command	






----------------------------------------=====================================================----------------------------------------------
/*-- Query \\ the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

select distinct city from station where lower(left(city,1)) in ('a', 'e', 'i', 'o', 'u');


-- Query\\ the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
select city , length(city) as length from station order by length asc, city asc limit 1;
select city , length(city) as length from station order by length desc, city asc limit 1;

--Query \\ the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.
select city from station where left(lower(city),1) in ('a', 'e', 'i', 'o', 'u') and right(lower(city),1) in ('a', 'e', 'i', 'o', 'u'); 
SELECT DISTINCT City FROM Station WHERE (City NOT LIKE '%A' AND City NOT LIKE '%E' AND City NOT LIKE '%I' AND City NOT LIKE '%O' AND City NOT LIKE '%U') OR (City NOT LIKE 'A%' AND City NOT LIKE 'E%' AND City NOT LIKE 'I%' AND City NOT LIKE 'O%' AND City NOT LIKE 'U%') ORDER BY City

--the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.
select name from students where marks > 75 order by right(name,3) asc, id;

--a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. Sort your result by ascending employee_id.
select name from Employee where salary > 2000 and months <10 order by employee_id asc;

-- Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:
Equilateral: It's a triangle with 3 sides of equal length.
Isosceles: It's a triangle with 2 sides of equal length.
Scalene: It's a triangle with 3 sides of differing lengths.
Not A Triangle: The given values of A, B, and C don't form a triangle.

select case 
when a+b<=c or a+c<=b or b+c<=a then 'Not A Triangle'
when a=b and b=c and c=a then 'Equilateral'
when a=b or b=c or c=a then 'Isosceles'
when a!=b and b!=c and c!=a then 'Scalene'
end
from TRIANGLES;

-- select count(*) from city where population > 100000;

-- if we wat 3 days or 7 days moving average
select date.., closing.. 
avg(closing..) over(order by date rows between 2 predecting and current row) 
from ...stock


--select round(LAT_N,4) from STATION where LAT_N< 137.2345 order by LAT_N desc limit 1;

--select round(max(LAT_N)+MIN(LAT_N)-MAX(LONG_W)-MIN(LONG_W),4)*-1 from station ;


--Query // Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

select sum(a.population) from city a inner join country b on a.countrycode = b.code where b.continent = 'Asia'


-- A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 4 decimal places.
select round(LAT_N,4) from 
(select row_number() over(order by LAT_N asc) as abc, LAT_N from station) a
where abc = (select round(count(*)/2) from station)

--a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.
select distinct(city) from station where id%2 = 0


--Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.
Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

select city.name from city inner join country on CITY.CountryCode = COUNTRY.Code where CONTINENT = 'Africa'
