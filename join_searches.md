1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
SELECT 

-- #table students
	students.id,  
    students.name, 
    students.surname, 
    students.date_of_birth, 
    students.fiscal_code, 
    students.enrolment_date, 
    students.registration_number, 
    students.email, 
    
-- # table degrees
    degrees.id AS degree_id, 
    degrees.department_id, 
    degrees.name AS degree_name

FROM db_university.students
INNER JOIN db_university.degrees
ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di Laurea in Economia';
```
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
```sql
SELECT 
-- #table degrees
	degrees.id, 
    degrees.name, 
    degrees.level, 
    degrees.address, 
    degrees.email, 
    degrees.website, 
    
-- #table departments
    departments.id AS department_id, 
    departments.name AS department_name, 
    departments.address AS department_address, 
    departments.phone AS department_phone, 
    departments.email AS department_email, 
    departments.website AS department_website, 
    departments.head_of_department
    
FROM db_university.degrees
INNER JOIN db_university.departments
ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Neuroscienze'
AND degrees.level = 'magistrale';
```
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT 
-- #table courses
	courses.id AS course_id, 
    courses.degree_id, 
    courses.name AS course_name, 
    courses.description, 
    courses.period, 
    courses.year, 
    courses.cfu, 
    courses.website, 
    
-- #table teachers
    teachers.id AS teacher_id, 
    teachers.name, 
    teachers.surname, 
    teachers.phone, 
    teachers.email, 
    teachers.office_address, 
    teachers.office_number
FROM db_university.courses

INNER JOIN db_university.course_teacher
ON courses.id = course_teacher.course_id

INNER JOIN db_university.teachers
ON course_teacher.teacher_id = teachers.id

WHERE teachers.id = 44;
```
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
```sql
SELECT 

-- #table students
	students.id, 
    students.name, 
    students.surname, 
    
-- #table degrees
    degrees.id AS degree_id, 
	degrees.name AS degree_name, 
    degrees.level, 
    degrees.address, 
    degrees.email, 
    degrees.website, 
    
-- #table departments
    departments.id AS department_id, 
    departments.name AS department_name
    
FROM db_university.students

INNER JOIN db_university.degrees
ON students.degree_id = degrees.id

INNER JOIN db_university.departments
ON degrees.department_id = departments.id

ORDER BY students.surname ,students.name ASC;
```
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
SELECT 
	
-- #table degrees
	degrees.id AS degree_id, 
    degrees.department_id, 
    degrees.name AS degree_name, 
    degrees.level, 
    degrees.address AS degree_address, 
    degrees.email AS degree_email, 
    degrees.website AS degree_website,
    
-- #table courses
    courses.id AS course_id, 
    courses.name AS course_name, 
    courses.description, 
    courses.period, 
    courses.year, 
    courses.cfu, 
    courses.website AS course_website,
    
-- #table teachers
	teachers.id AS teacher_id, 
    teachers.name, 
    teachers.surname, 
    teachers.phone, 
    teachers.email AS teacher_email, 
    teachers.office_address, 
    teachers.office_number
    
    
    
FROM db_university.teachers

INNER JOIN db_university.course_teacher
ON teachers.id = course_teacher.teacher_id

INNER JOIN db_university.courses
ON course_teacher.course_id = courses.id

INNER JOIN db_university.degrees
ON courses.degree_id = degrees.id;
```
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
```sql
SELECT 

-- #table teachers
	DISTINCT teachers.id AS teacher_id, 
    teachers.name, 
    teachers.surname, 
    teachers.phone AS teacher_phone, 
    teachers.email AS teacher_email, 
    teachers.office_address, 
    teachers.office_number, 
    
-- #table departments
    departments.id AS department_id, 
    departments.name AS department_name,
    departments.address AS department_address, 
    departments.phone AS department_phone, 
    departments.email AS department_email, 
    departments.website, 
    departments.head_of_department

FROM db_university.teachers

INNER JOIN db_university.course_teacher
ON teachers.id = course_teacher.teacher_id

INNER JOIN db_university.courses
ON course_teacher.course_id = courses.id

INNER JOIN db_university.degrees
ON courses.degree_id = degrees.id
INNER JOIN db_university.departments
ON degrees.department_id = departments.id

WHERE departments.name = 'Dipartimento di Matematica';
```
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18