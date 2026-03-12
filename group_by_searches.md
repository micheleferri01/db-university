1. Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT 
    COUNT(students.id) AS enrolled_students, 
    YEAR(enrolment_date) AS enrolment_year
FROM db_university.students
GROUP BY enrolment_year;

```
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT 
    COUNT(teachers.id) AS num_of_teachers, 
    teachers.office_address
FROM db_university.teachers
GROUP BY teachers.office_address;
```
3. Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT 
	ROUND(AVG(exam_student.vote)) AS avg_vote, 
	exam_student.exam_id 
FROM db_university.exam_student
GROUP BY exam_student.exam_id;
```
4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT 
    COUNT(degrees.id) AS num_of_degrees, 
    degrees.department_id
FROM db_university.degrees
GROUP BY department_id;
```