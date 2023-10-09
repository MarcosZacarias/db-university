# Data Base University - Exercise 2

## Query con _GROUP BY_

### Query 1

```sql
-- Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(*) "number_students", YEAR(`enrolment_date`) "enrolment_year"
FROM `students`
GROUP BY YEAR(`enrolment_date`);
```

### Query 2

```sql
-- Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(*) "number_teachers", `office_address` "office"
FROM `teachers`
GROUP BY `office_address`;
```

### Query 3

```sql
-- Calcolare la media dei voti di ogni appello d'esame
SELECT  `exam_id` "exam appeal", AVG(`vote`) "average vote"
FROM `exam_student`
GROUP BY `exam_id`;
```

### Query 4

```sql
-- Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT `department_id` "departments", COUNT(*) "numbers_degrees"
FROM `degrees`
GROUP BY `department_id`;
```

## Query con _JOIN_

### Query 1

```sql
-- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT
`stu`.`id` "id",
`stu`.`name` "name",
`stu`.`surname` "surname",
`deg`.`name` "degree"
FROM `students` `stu`

INNER JOIN `degrees` `deg`
ON `deg`.`id` = `stu`.`degree_id`

WHERE `deg`.`name`= "Corso di Laurea in Economia";
```

### Query 2

```sql
-- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT
`dep`.`name` "department",
`deg`.`name` "name",
`deg`.`level` "level"
FROM `departments` `dep`

INNER JOIN `degrees` `deg`
ON `dep`.`id` = `deg`.`department_id`

WHERE `dep`.`name` = "Dipartimento di Neuroscienze"
AND `deg`.`level` = "magistrale";
```

### Query 3

```sql
-- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT *
FROM `courses` `cou`

INNER JOIN `course_teacher` `cou_tea`
ON `cou`.`id` = `cou_tea`.`course_id`

INNER JOIN `teachers` `tea`
ON `tea`.`id` = `cou_tea`.`teacher_id`

WHERE `tea`.`id` = 44;
```

### Query 4

```sql
-- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT `stu`.`surname` "surname_student",
`stu`.`name` "name_student",
`deg`.*,
`dep`.`name` "department_name"
FROM `students` `stu`

INNER JOIN `degrees` `deg`
ON `stu`.`degree_id` = `deg`.`id`

INNER JOIN `departments` `dep`
ON `dep`.`id` = `deg`.`department_id`

ORDER BY `stu`.`surname`, `stu`.`name`;
```

### Query 5

```sql
-- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT `deg`.*,
`cou`.`name` "course_name",
`tea`.`surname` "teacher_surname",
`tea`.`name` "teacher_name"
FROM `degrees` `deg`

INNER JOIN `courses` `cou`
ON `cou`.`degree_id`= `deg`.`id`

INNER JOIN `course_teacher` `cou_tea`
ON `cou`.`id` = `cou_tea`.`course_id`

INNER JOIN `teachers` `tea`
ON `tea`.`id` = `cou_tea`.`teacher_id`;
```

### Query 6

```sql
-- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT `dep`.`name` "department",
`tea`.*
FROM `departments` `dep`

INNER JOIN `degrees` `deg`
ON `deg`.`department_id` = `dep`.`id`

INNER JOIN `courses` `cou`
ON `cou`.`degree_id`= `deg`.`id`

INNER JOIN `course_teacher` `cou_tea`
ON `cou`.`id` = `cou_tea`.`course_id`

INNER JOIN `teachers` `tea`
ON `tea`.`id` = `cou_tea`.`teacher_id`

WHERE `dep`.`name` = "Dipartimento di Matematica"

GROUP BY `tea`.`id`;
```

### Query 7 **BONUS**

```sql
-- BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.


```
