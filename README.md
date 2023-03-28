## Info

Simple grafana testenvironment with docker. 

## start the container
> docker-compose up -d

## get container ip

> docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' grafana-database-1

## login to grafan server

> http://localhost:3000/

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Credentials: admin / admin

## Example Database source

- click on the gear
- Data sources 
- Host Container IP from "get container ip"
- Credentials / Ports form docker-compose.yml

## Demo Table in mysql
Create a Table
> CREATE TABLE Persons (<br>
&nbsp;&nbsp;&nbsp;    PersonID int,<br>
&nbsp;&nbsp;&nbsp;    Name varchar(255),<br>
&nbsp;&nbsp;&nbsp;    Age INT<br>
);

Create some Data
> INSERT INTO Persons(PersonID,Name,Age)<br>
VALUES (2,"Frodo",50)

...

# Create a Dashboard
- Menu (with the 4 squares)
- Dashboards 
- New 
- Add a new panel
- Type: Table
- Cell Options 
  * Type: Gauge
  * Gauge Display Mode: Gradient
  * Value Mappings:
  * define a range e.g.   10 - 45 -> green & 46 - 99999 -> red
  * define a regex: ^[^0-9]*   -> set to transparent
- Query 
  * Order: On (Order by Age)
  * Dataset: db
  * Table: Persons
  * Column: Name
  * Column: Age
