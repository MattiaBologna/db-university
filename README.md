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


# QUERY CON GROUP BY 

1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

## QUERY 1

SELECT COUNT(*) AS `enrolled_per_year`, YEAR(`enrolment_date`)
FROM `students`
GROUP BY YEAR(`enrolment_date`);

## QUERY 2

SELECT COUNT(*), `office_address`
FROM `teachers`
GROUP BY `office_address`;

## QUERY 3

SELECT COUNT(*), `exam_id`, AVG(`vote`) AS `media_voto`
FROM `exam_student`
GROUP BY `exam_id`;


## QUERY 4

SELECT COUNT(*), `departments`.`id`, `departments`.`name`
FROM `courses` 
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`id` = `departments`.`id`
GROUP BY `departments`.`id`;


# QUERY CON JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.


## QUERY 1

SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` 
FROM `degrees`
INNER JOIN `students`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

## QUERY 2

SELECT * 
FROM `degrees`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = 'magistrale' AND `departments`.`name` = 'Dipartimento di Neuroscienze';

## QUERY 3

SELECT * 
FROM `courses` 
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = '44';

## QUERY 4

SELECT `students`.`name`, `students`.`surname`, `degrees`.`name`, `degrees`.`level`,`degrees`.`address`, `degrees`.`email`, `degrees`.`website`, `departments`.`name` 
FROM `students`
INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
INNER JOIN `departments` 
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`name` ASC, `students`.`surname` ASC;

## QUERY 5 

SELECT `degrees`.`department_id`, `degrees`.`name`, `degrees`.`level`, `courses`.`name` AS `course_name`, `teachers`.`name`,  `teachers`.`surname` 
FROM `degrees`
INNER JOIN `courses` 
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`;

## QUERY 6 

SELECT `teachers`.`name`, `teachers`.`surname`, `departments`.`name`
FROM `departments`
INNER JOIN `courses`
ON `departments`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';





