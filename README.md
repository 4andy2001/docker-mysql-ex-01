# docker-mysql-01

Basic example showing how to dockerize mysql and run a sample session with the mysql client.

From tutorial at:

https://vijayasimhabr.medium.com/running-mysql-database-server-with-docker-ad10533473c7

## Setup git for the project
Create repository in github 4andy2001 called docker-mysql-ex-01
Get the URL of the repository, i.e., git@github.com:4andy2001/docker-mysql-ex-01.git

Create a .gitignore file

In the directory containing the project files, i.e., docker-mysql-ex-01 execute the following to initialize the git project do the initial commit and push: 
```
git init
git add .
git commit   
git remote add origin git@github.com:4andy2001/docker-mysql-ex-01.git
git branch -M main
git push -u origin main
```



##  Get and run mysql in a Docker container

Create docker-compose.yaml using a mysql image from Docker Hub.

Start mysql
```
docker compose up -d
```

## Use mysql client to play with database

Either execute mysql client from within the container or execute the client from the command line.

### Execute mysql client from within the container
```
docker exec -it mysql-container mysql -u root -p
```

### Execute mysql from command line
```
mysql -h 127.0.0.1 -P 3306 -u root -p
```

### Example mysql session
```
SHOW DATABASES;
USE my_database;


CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    hire_date DATE NOT NULL
);

INSERT INTO employees (first_name, last_name, email, hire_date) VALUES
('Amit', 'Sharma', 'amit.sharma@example.com', '2023-01-15'),
('Priya', 'Singh', 'priya.singh@example.com', '2023-02-20'),
('Rahul', 'Verma', 'rahul.verma@example.com', '2023-03-25'),
('Anjali', 'Patel', 'anjali.patel@example.com', '2023-04-10'),
('Vikram', 'Gupta', 'vikram.gupta@example.com', '2023-05-05');

SELECT * FROM employees;

SELECT first_name, last_name, email FROM employees;

SELECT * FROM employees WHERE hire_date > '2023-01-01';

SELECT * FROM employees ORDER BY last_name ASC;

SELECT * FROM employees LIMIT 5;

INSERT INTO employees (first_name, last_name, email, hire_date) VALUES
('Ravi', 'Kumar', 'ravi.kumar@example.com', '2023-06-15');

UPDATE employees
SET email = 'ravi.kumar123@example.com'
WHERE first_name = 'Ravi' AND last_name = 'Kumar';

DELETE FROM employees
WHERE first_name = 'Ravi' AND last_name = 'Kumar';
```