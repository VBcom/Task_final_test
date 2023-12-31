# Задания
## 1
![Задание 1](https://raw.githubusercontent.com/VBcom/Examination_Final/main/src/1.png)
## 2
![Задание 2](https://raw.githubusercontent.com/VBcom/Examination_Final/main/src/2.png)
## 3
![Задание 3](https://raw.githubusercontent.com/VBcom/Examination_Final/main/src/3_1.png)
![Задание 3](https://raw.githubusercontent.com/VBcom/Examination_Final/main/src/3_2.png)
## 4
![Задание 4](https://raw.githubusercontent.com/VBcom/Examination_Final/main/src/4.png)
## 5
### 1
```
cat > animals_home    
cat > animals_pack
cat animals_home animals_pack > animals
cat animals
mv animals_friends_of_man
ls -ali
```
### 2
```
mkidir VB_folder
cd ~/VB
mv friends_of_man ~/VB_folder
ls -ali
```
### 3
```
sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.29-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.29-1_all.deb
sudo apt-get update
```
### 4
```
sudo wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/containerd.io_1.5.10-1_amd64.deb
sudo dpkg -i containerd.io_1.5.10-1_amd64.deb
sudo dpkg -r containerd.io
```
## 6
![Задание 6](https://raw.githubusercontent.com/VBcom/Examination_Final/main/src/6.png)

## 7
```mysql
CREATE DATABASE friends_of_human;
```
## 8
```mysql
USE friends_of_human;
CREATE TABLE animal_classes
(
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Class_name VARCHAR(20)
);

INSERT INTO animal_classes (Class_name)
VALUES ('домашние'), ('вьючные');

CREATE TABLE animals_home
(
    Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR (20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO home_animals (Genus_name, Class_id)
VALUES ('Собаки', 1), ('Кошки', 1), ('Хомяки', 1);

CREATE TABLE animals_pack
(
    Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR (20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO animals_pack (Genus_name, Class_id)
VALUES ('Лошади', 2), ('Верблюды', 2), ('Ослы', 2);
```
## 9
```mysql

CREATE TABLE dogs 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(30), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES animals_home (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO dogs (Name, Birthday, Commands, Genus_id)
VALUES ('Собака 1', '2023-01-01', 'Команда 1', 1),
('Собака 2', '2023-01-01', "Команда 2", 1),
('Собака 3', '2023-01-01', "Команда 3", 1);

CREATE TABLE cats 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES animals_home (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO cats (Name, Birthday, Commands, Genus_id)
VALUES ('Кошка 1', '2023-01-01', 'Команда 1', 2),
('Кошка 2', '2023-01-01', "Команда 2", 2),
('Кошка 3', '2023-01-01', "Команда 3", 2);

CREATE TABLE hamsters 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES animals_home (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO hamsters (Name, Birthday, Commands, Genus_id)
VALUES ('Хомяк 1', '2023-01-01', 'Команда 1', 3),
('Хомяк 2', '2023-01-01', "Команда 2", 3),
('Хомяк 3', '2023-01-01', "Команда 3", 3);

CREATE TABLE horses
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES animals_pack (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO horses (Name, Birthday, Commands, Genus_id)
VALUES ('Лошадь 1', '2023-01-01', 'Команда 1', 1),
('Лошадь 2', '2023-01-01', "Команда 2", 1),
('Лошадь 3', '2023-01-01', "Команда 3", 1);

CREATE TABLE camels 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES animals_pack (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO camels (Name, Birthday, Commands, Genus_id)
VALUES ('Верблюд 1', '2023-01-01', 'Команда 1', 3),
('Верблюд 2', '2023-01-01', "Команда 2", 3),
('Верблюд 3', '2023-01-01', "Команда 3", 3);

CREATE TABLE donkeys 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES animals_pack (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO donkeys (Name, Birthday, Commands, Genus_id)
VALUES ('Осел 1', '2023-01-01', 'Команда 1', 2),
('Осел 2', '2023-01-01', 'Команда 2', 2),
('Осел 3', '2023-01-01', 'Команда 3', 2);
```
## 10
```mysql
SET SQL_SAFE_UPDATES = 0;
DELETE FROM camels;

SELECT Name, Birthday, Commands FROM horses
UNION SELECT  Name, Birthday, Commands FROM donkeys;
```
## 11
```mysql
CREATE TEMPORARY TABLE animals AS 
SELECT *, 'Лошади' as genus FROM horses
UNION SELECT *, 'Ослы' AS genus FROM donkeys
UNION SELECT *, 'Собаки' AS genus FROM dogs
UNION SELECT *, 'Кошки' AS genus FROM cats
UNION SELECT *, 'Хомяки' AS genus FROM hamsters;

CREATE TABLE animals_young AS
SELECT Name, Birthday, Commands, genus, TIMESTAMPDIFF(MONTH, Birthday, CURDATE()) AS Age_in_month
FROM animals WHERE Birthday BETWEEN ADDDATE(curdate(), INTERVAL -3 YEAR) AND ADDDATE(CURDATE(), INTERVAL -1 YEAR);
 
SELECT * FROM animals_young;
```
## 12
```mysql
SELECT h.Name, h.Birthday, h.Commands, pa.Genus_name, ya.Age_in_month 
FROM horses h
LEFT JOIN animals_young ya ON ya.Name = h.Name
LEFT JOIN animals_pack pa ON pa.Id = h.Genus_id
UNION 
SELECT d.Name, d.Birthday, d.Commands, pa.Genus_name, ya.Age_in_month 
FROM donkeys d 
LEFT JOIN animals_young ya ON ya.Name = d.Name
LEFT JOIN animals_pack pa ON pa.Id = d.Genus_id
UNION
SELECT c.Name, c.Birthday, c.Commands, ha.Genus_name, ya.Age_in_month 
FROM cats c
LEFT JOIN animals_young ya ON ya.Name = c.Name
LEFT JOIN animals_home ha ON ha.Id = c.Genus_id
UNION
SELECT d.Name, d.Birthday, d.Commands, ha.Genus_name, ya.Age_in_month 
FROM dogs d
LEFT JOIN animals_young ya ON ya.Name = d.Name
LEFT JOIN animals_home ha ON ha.Id = d.Genus_id
UNION
SELECT hm.Name, hm.Birthday, hm.Commands, ha.Genus_name, ya.Age_in_month 
FROM hamsters hm
LEFT JOIN animals_young ya ON ya.Name = hm.Name
LEFT JOIN animals_home ha ON ha.Id = hm.Genus_id;
```
