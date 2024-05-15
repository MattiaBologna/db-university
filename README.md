##  QUERY 1

SELECT COUNT(*)
FROM `students`
WHERE `date_of_birth` LIKE '1990%' 

SELECT `name`, `surname`, `date_of_birth`
FROM `students`
WHERE `date_of_birth` LIKE '1990%'  
ORDER BY `date_of_birth` ASC;

## QUERY 2

SELECT COUNT(*)
FROM `courses`
WHERE `cfu` > '10';

SELECT `name`, `description`, `cfu`
FROM `courses`
WHERE `cfu` > '10';

## QUERY 3

SELECT `name`, `surname`, `date_of_birth`
FROM `students`
WHERE `date_of_birth` <= '1994-01-01'  
ORDER BY `students`.`date_of_birth` DESC



