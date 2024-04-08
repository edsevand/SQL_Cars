## Data Analyst
This work consists of a dataset that collects information about cars, the brand they belong to, model, year of manufacture, transmission type, and fuel type, as well as information about the customers who purchased any of the cars. 

An analysis of the dataset using MySQL is shown, which allows to know key information, such as the total number of cars sold in a particular year or of a particular brand, as well as the total number of cars purchased by gender, among other relationships that hold the data.

## Dataset

The dataset contains different tables that are correlated with each other by means of different keys, so that it is possible to join different tables to obtain a better understanding. 

The following image shows the different tables of the dataset

<p align="center">
    <img src = "https://raw.githubusercontent.com/edsevand/SQL_Cars/main/images/2.jpeg">
</p>

The way to join tables in SQL is through the word "Join" that allows to match the keywords of two (or more) tables and thus correlate the data

### Case 1

```
use carsonline;

select CT.car_make, CT.car_model, C.price, CT.car_year, T.transmission_name, F.fuel_type_name

from cars C 
join transmission_types T on C.transmission_type_id = T.transmission_type_id
join car_types CT on C.car_type_id = CT.car_type_id
join fuel_types F on C.fuel_type_id = F.fuel_type_id

where F.fuel_type_name = 'Hybrid';
```
In this particular case, we show the code that yields a table made up of 3 and with the particularity of filtering only hybrid cars

<p align="center">
    <img src = "https://raw.githubusercontent.com/edsevand/SQL_Cars/main/images/3.jpeg">
</p>

### Case 2

In this case, it is necessary to know the specific number of manual gearbox cars, by year and brand, sorting the output in ascending order

```
use carsonline;

select CT.car_make, CT.car_year, count(distinct CT.car_model) as 'Num_cars_manual-gearbox'

from cars C

join car_types CT on C.car_type_id = CT.car_type_id

join transmission_types T on T.transmission_type_id = C.transmission_type_id

where T.transmission_name = 'manual'

group by CT.car_make, CT.car_year

order by CT.car_year;

```
The number of cars sold by brand from 1999 to 2020 can be broken down by year

<p align="center">
    <img src = "https://raw.githubusercontent.com/edsevand/SQL_Cars/main/images/4.jpeg">
</p>