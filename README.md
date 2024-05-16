1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

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

## QUERY 4

SELECT COUNT(*)
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = '1';

SELECT `name`, `period`, `year`
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = '1';

## QUERY 5

SELECT COUNT(*)
FROM `exams`
WHERE `date` = '2020-06-20'
AND `hour` > '14:00:00';

SELECT `course_id`, `date`, `hour`, `address`, `location`
FROM `exams`
WHERE `date` = '2020-06-20'
AND `hour` > '14:00:00';

## QUERY 6

SELECT COUNT(*)
FROM `degrees`
WHERE `level` = 'magistrale';

SELECT `name`, `level`
FROM `degrees`
WHERE `level` = 'magistrale';

## QUERY 7

SELECT COUNT(*)
FROM `departments`;

SELECT `name`, `address`, `head_of_department`
FROM `departments`;

## QUERY 8

SELECT COUNT(*)
FROM `teachers`
WHERE `phone` IS NULL;

SELECT `name`, `surname`, `email`, `office_address`, `office_number`, `phone`
FROM `teachers`
WHERE `phone` IS NULL;


### QUERY CON GROUP BY 

1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

## QUERY 1

SELECT COUNT(*) AS `enrolled_per_year`, YEAR(`enrolment_date`)
FROM `students`
GROUP BY YEAR(`enrolment_date`);



