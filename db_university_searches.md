1. Selezionare tutti gli studenti nati nel 1990 (160)
```sql
SELECT * 
FROM db_university.students
WHERE students.date_of_birth LIKE '1990%';
```
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
```sql
SELECT * 
FROM db_university.courses
WHERE courses.cfu > 10;
```
3. Selezionare tutti gli studenti che hanno più di 30 anni
```sql
SELECT *
FROM db_university.students
WHERE students.date_of_birth < CURRENT_DATE() - INTERVAL 30 YEAR;
```
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
```sql
SELECT * 
FROM db_university.courses
WHERE courses.period = 'I semestre' 
AND courses.year = 1;
```
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
```sql
SELECT * 
FROM db_university.exams
WHERE exams.date = '2020-06-20'
AND exams.hour > '14:00:00';
```
6. Selezionare tutti i corsi di laurea magistrale (38)
```sql
SELECT * 
FROM db_university.degrees
WHERE degrees.level = 'magistrale';
```
7. Da quanti dipartimenti è composta l'università? (12)
```sql
SELECT COUNT(*)
FROM db_university.departments;
```
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
```sql
-- PER IL NUMERO ESATTO
SELECT COUNT(*) 
FROM db_university.teachers
WHERE teachers.phone IS NULL;

-- PER LA LISTA
SELECT * 
FROM db_university.teachers
WHERE teachers.phone IS NULL;
```