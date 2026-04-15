# SQL-Island — Writeups

Welcome — this page contains my writeups for the SQL Island challenge. Each question includes the SQL query used to solve it and a screenshot of the result.

## Table of contents
- [Questions 1–8](#questions-1-8)
- [Questions 9–16](#questions-9-16)
- [Questions 17–24](#questions-17-24)

---

## Questions 1–8

### QUESTION 01
It seems there are a few people living in these villages. How can I see a list of all inhabitants?
![ffb0ae32b580efd9e489c30632346b3a.png](:/8ed9e498425c4f36bdaf904cb6312bfc)

Solution:
```sql
SELECT * FROM INHABITANT;
```
![Solution_01.png](:/3782a31cd8674f7ab7e335cfbe55ec59)

---

### QUESTION 02
Who is friendly on this island?
![Question_02.png](:/d37b4629d077469bb4070ed618f85d2c)

Solution:
```sql
SELECT * FROM INHABITANT WHERE state = 'friendly';
```
![Solution_02.png](:/b26274d442924613bd707d357ecd1c25)

---

### QUESTION 03
Find a friendly weaponsmith.

Solution:
```sql
SELECT * FROM INHABITANT WHERE job = 'weaponsmith' AND state = 'friendly';
```
![Solution_03.png](:/b71dcf18fcce44c58577df5e719d173f)

---

### QUESTION 04
Find smiths (jobs ending with "smith") who are friendly.

Solution:
```sql
SELECT * FROM INHABITANT WHERE job LIKE '%smith' AND state = 'friendly';
```

---

### QUESTION 05
What is the `personid` for the inhabitant named 'Stranger'?

Solution:
```sql
SELECT personid FROM INHABITANT WHERE name = 'Stranger';
```
![Solution_05.png](:/8ce884659a1049cbbc72015ac86fe60c)

---

### QUESTION 06
How much gold does 'Stranger' have?

Solution:
```sql
SELECT gold FROM INHABITANT WHERE name = 'Stranger';
```
![Solution_06.png](:/eb66050cbdf946339f3df7ecbab96e3f)

---

### QUESTION 07
List all items that don't belong to anyone.

Solution:
```sql
SELECT * FROM ITEM WHERE owner ISNULL;
```
![Solution_07.png](:/277f22c546034c20ab6223b378d4ac5a)

---

### QUESTION 08
Collect ownerless items by assigning them to personid 20.

Solution:
```sql
UPDATE ITEM SET owner = '20' WHERE owner ISNULL;
```
![Solution_08.png](:/081a3fd0be54498d933e73fa8fe45527)

---

## Questions 9–16

### QUESTION 09
List all items owned by personid 20.

Solution:
```sql
SELECT * FROM ITEM WHERE owner = '20';
```
![Solution_09.png](:/2a8d4bca66fe4b4eafee1f5f01493754)

---

### QUESTION 10
Find a friendly dealer or merchant.

Solution:
```sql
SELECT * FROM INHABITANT WHERE (job = 'dealer' OR job = 'merchant') AND state = 'friendly';
```
![Solution_10.png](:/e158ae34be434d2a8cf9a2acdd358ed9)

---

### QUESTION 11
Transfer the `ring` and `teapot` to personid 15.

Solution:
```sql
UPDATE ITEM SET owner = 15 WHERE item IN ('ring','teapot');
```
![Solution_11.png](:/3640571fed0f4766ae313337f8c44785)

---

### QUESTION 12
Change name from 'Stranger' to 'Ahmed' for personid 20.

Solution:
```sql
UPDATE INHABITANT SET name = 'Ahmed' WHERE personid = 20;
```
![Solution_12.png](:/273c99abd6b1453abe9b6701eb7609be)

---

### QUESTION 13
Find bakers and sort by gold (richest first).

Solution:
```sql
-- Use ORDER BY gold DESC to get richest first
SELECT * FROM INHABITANT WHERE job = 'baker' ORDER BY gold DESC;
```
![Solution_13.png](:/e0d79d063d2042ce95eb8c9476368e4c)

---

### QUESTION 14
Is there a pilot on the island?

Solution:
```sql
SELECT * FROM INHABITANT WHERE job = 'pilot';
```
![Solution_14.png](:/fe2a0d6fbb144949b154ac35bff490ad)

---

### QUESTION 15
Find the chief's name of Onionville using a join.

Solution:
```sql
SELECT INHABITANT.name FROM VILLAGE, INHABITANT
ON VILLAGE.villageid = INHABITANT.villageid
WHERE VILLAGE.name = 'Onionville' AND INHABITANT.personid = VILLAGE.chief;
```
![Solution_15.png](:/c3f6fb661c3746d4bf501b2df4acc3f9)

---

### QUESTION 16
How many women (gender = 'f') are in Onionville?

Solution:
```sql
SELECT COUNT(*) FROM VILLAGE, INHABITANT
ON VILLAGE.villageid = INHABITANT.villageid
WHERE VILLAGE.name = 'Onionville' AND INHABITANT.gender = 'f';
```
![Solution_16.png](:/b6a5b0d648d1434080cc67608e08ed78)

---

## Questions 17–24

### QUESTION 17
Who is the woman in Onionville?

Solution:
```sql
SELECT INHABITANT.name FROM VILLAGE, INHABITANT
ON VILLAGE.villageid = INHABITANT.villageid
WHERE VILLAGE.name = 'Onionville' AND INHABITANT.gender = 'f';
```
![Solution_17.png](:/407dc5ae93d542a69cca1f1b2769d88b)

---

### QUESTION 18
Total gold in Cucumbertown (sum of inhabitants' gold).

Solution:
```sql
SELECT SUM(inhabitant.gold) FROM inhabitant, village
WHERE village.villageid = inhabitant.villageid AND village.name = 'Cucumbertown';
```
![Solution_18.png](:/69e23301ac884fe88758659b1ec26e53)

---

### QUESTION 19
Total gold owned by bakers, dealers, and merchants.

Solution:
```sql
SELECT SUM(gold) FROM INHABITANT
WHERE job = 'baker' OR job = 'dealer' OR job = 'merchant';
```
![Solution_19.png](:/3b7bc5a8a5824a97b19d088f788d77fa)

---

### QUESTION 20
Average gold per `state`.

Solution:
```sql
SELECT state, AVG(gold) FROM INHABITANT GROUP BY state;
```
![Solution_20.png](:/46db1f04ce10419f99a1004fed5f78b9)

---

### QUESTION 21
Delete 'Dirty Dieter' from inhabitants.

Solution:
```sql
DELETE FROM INHABITANT WHERE name = 'Dirty Dieter';
```
![Solution_21.png](:/215756506ed74324ba9dc34b66817ed9)

---

### QUESTION 22
Delete 'Dirty Diane' as well.

Solution:
```sql
DELETE FROM INHABITANT WHERE name = 'Dirty Diane';
```
![Solution_22.png](:/cf3ca9f0ed45433d9c2f042075b2cf1f)

---

### QUESTION 23
Release the pilot (set state to 'friendly').

Solution:
```sql
UPDATE INHABITANT SET state = 'friendly' WHERE job = 'pilot';
```
![Solution_23.png](:/ce61d586857c4e62b302129561db0240)

---

### QUESTION 24
Update the certificate name (change inhabitant name for personid 20).

Solution:
```sql
UPDATE INHABITANT SET name = 'Your Name' WHERE personid = 20;
```
![Solution_24.png](:/1ba40a136db341edbaeebd860a53fb3b)

---

If you'd like, I can also add a link to the `sql_exercises.md` writeups file, add badges, or add a license. Tell me which you'd prefer.
