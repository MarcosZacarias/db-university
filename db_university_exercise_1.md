# Data Base University - Exercise 1

## Query 1

```sql
-- Selezionare tutti gli studenti nati nel 1990 (160)
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990
```

## Query 2

```sql
-- Selezionare tutti i corsi che valgono più di 10 crediti (479)
SELECT *
FROM `courses`
WHERE `cfu`>10
```

## Query 3

```sql
-- Selezionare tutti gli studenti che hanno più di 30 anni
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`)<1993

-- OR
SELECT *
FROM `students`
WHERE YEAR(CURRENT_DATE) - YEAR(`date_of_birth`)>30
```

## Query 4

```sql
-- Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
SELECT *
FROM `courses`
WHERE `year` = 1
AND `period`= "I semestre"
```

## Query 5

```sql
-- Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
SELECT *
FROM `exams`
WHERE `date` = "2020/06/20"
AND `hour`>"14:00"
```

## Query 6

```sql
-- Selezionare tutti i corsi di laurea magistrale (38)
SELECT *
FROM `degrees`
WHERE `level`="magistrale"
```

## Query 7

```sql
-- Da quanti dipartimenti è composta l'università? (12)
SELECT COUNT(*) AS "N° Departments"
FROM `departments`
```

## Query 8

```sql
-- Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
SELECT COUNT(*) AS "Teachers without cell number"
FROM `teachers`
WHERE `phone` IS NULL
```
