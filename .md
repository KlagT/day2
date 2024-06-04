# DAY3
### TASK0
---
```
WITH m AS (SELECT * FROM menu WHERE price BETWEEN 800 AND 1000)
SELECT m.pizza_name, m.price, pz.name as pizzeria_name, pv.visit_date, p.name FROM person_visits pv
JOIN pizzeria pz
	ON pz.id = pv.pizzeria_id
JOIN person_order po
	ON po.person_id = pv.person_id
JOIN person p
	ON p.id = po.person_id
JOIN m 
	ON m.pizzeria_id = pv.pizzeria_id
WHERE p.name = 'Kate'
ORDER BY 1, 2, 3
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/039509a7-cab3-4945-a32c-c0d125a479e1)
---

### TASK1
---
```
SELECT id as menu_id FROM menu
WHERE id NOT IN (SELECT menu_id FROM person_order)
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/b0f31ab5-f1f3-41b9-b15b-eb99f0ed99b4)

---

### TASK2
---
```
SELECT menu.pizza_name, menu.price, pizzeria.name as pizzeria_name FROM menu
JOIN pizzeria
	ON pizzeria.id = menu.pizzeria_id
WHERE menu.id NOT IN (SELECT menu_id FROM person_order)
ORDER BY 1, 2
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/d6cd4760-4b8f-4c39-ad4b-f1febb06499d)

---


### TASK4
---
```
SELECT pz.name as pizzeria_name FROM person_order po
JOIN person p ON p.id = po.person_id
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pz ON pz.id = m.pizzeria_id
WHERE p.gender = 'female'
EXCEPT
SELECT pz.name as pizzeria_name FROM person_order po
JOIN person p ON p.id = po.person_id
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pz ON pz.id = m.pizzeria_id
WHERE p.gender = 'male'
ORDER BY pizzeria_name;
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/7d02bf67-1992-48d7-ac88-c76daec7cedc)

---

### TASK5
---
```
SELECT pz.name as pizzeria_name FROM person_visits pv
JOIN person p ON p.id = pv.person_id
JOIN pizzeria pz ON pz.id = pv.pizzeria_id
WHERE p.name = 'Andrey'
EXCEPT
SELECT pz.name as pizzeria_name FROM person_order po
JOIN person p ON p.id = po.person_id
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pz ON pz.id = m.pizzeria_id
WHERE p.name = 'Andrey'
ORDER BY pizzeria_name;
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/25a6b90e-4d0d-4db2-bd82-e8590416086f)

---

### TASK6
---
```
SELECT m1.pizza_name, pz1.name as pizzeria_name_1, pz2.name as pizzeria_name_2, m1.price FROM menu m1
JOIN menu m2 ON m1.pizza_name = m2.pizza_name and m1.price = m2.price
JOIN pizzeria pz1 ON pz1.id = m1.pizzeria_id
JOIN pizzeria pz2 ON pz2.id = m2.pizzeria_id
WHERE pz1.name < pz2.name
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/0b666603-0ef5-4d69-9d1e-63981cf0152f)

---

### TASK7
---
```
INSERT INTO menu
VALUES (19, 2, 'greek pizza', 800);
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/f0c38f0f-3484-4df2-856b-9d7b81c99c89)

---

### TASK8
---
```
INSERT INTO menu
VALUES ((SELECT max(id) + 1 FROM menu), 2, 'sicilian pizza', 900);
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/463362c0-6bf6-4b4e-adff-51366ec892ca)

---

### TASK9
---
```
INSERT INTO person_visits
VALUES (
	(SELECT max(id) + 1 FROM person_visits),
	(SELECT id FROM person WHERE person.name = 'Denis'),
	(SELECT id FROM pizzeria WHERE pizzeria.name = 'Dominos'),
	'2022-02-24'
);
INSERT INTO person_visits
VALUES (
	(SELECT max(id) + 1 FROM person_visits),
	(SELECT id FROM person WHERE person.name = 'Irina'),
	(SELECT id FROM pizzeria WHERE pizzeria.name = 'Dominos'),
	'2022-02-24'
);
SELECT * FROM person_visits
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/9979b11a-eca3-4a5d-942e-00d01a25f667)

---

### TASK10
---
```
INSERT INTO person_order VALUES (
	(SELECT MAX(id) + 1 FROM person_order),
	(SELECT id FROM person WHERE name = 'Denis'),
	(SELECT id FROM menu WHERE pizza_name = 'sicilian pizza'),
	'2022-02-24'
);
INSERT INTO person_order VALUES (
	(SELECT MAX(id) + 1 FROM person_order),
	(SELECT id FROM person WHERE name = 'Irina'),
	(SELECT id FROM menu WHERE pizza_name = 'sicilian pizza'),
	'2022-02-24'
)
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/b21c39bf-3410-4d41-8b56-b49e35f246b7)

---

### TASK11
---
```
UPDATE menu
SET price = price - price * 0.1
WHERE menu.pizza_name = 'greek pizza';
SELECT * FROM menu
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/7700debf-6704-4922-a5db-fa9ead3b168e)

---


### TASK13
---
```
DELETE FROM person_order WHERE order_date='2022-02-25';
SELECT * FROM person_order WHERE order_date = '2022-02-25';
```
```
DELETE FROM menu WHERE pizza_name='greek pizza';
SELECT * FROM menu WHERE pizza_name ='greek pizza';
```
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/a256c895-6665-439e-8f86-e54ab7113e15)
![image](https://github.com/Banechka1/SQL_Practice/assets/108561676/6b1b40dc-27d7-4fd5-83f6-719489278ede)

---
