```sql
**QUESTION 01:**  It seems there are a few people living in these villages. How can I see a list of all inhabitants?
![ffb0ae32b580efd9e489c30632346b3a.png](:/8ed9e498425c4f36bdaf904cb6312bfc)

**Solution 01:** SELECT * FROM INHABITANT;
![Solution_01.png](:/3782a31cd8674f7ab7e335cfbe55ec59)

**QUESTION 02:** Thank you, Edward! Okay, let's see who is friendly on this island...
![Question_02.png](:/d37b4629d077469bb4070ed618f85d2c)
**Solution 02:** SELECT * FROM INHABITANT WHERE state = 'friendly';
![Solution_02.png](:/b26274d442924613bd707d357ecd1c25)
**QUESTION 03:** There is no way around getting a sword for myself. I will now try to find a friendly weaponsmith to forge me one. (Hint: You can combine predicates in the WHERE clause with AND)
**Solution 03:** SELECT * FROM INHABITANT WHERE job = 'weaponsmith' AND state = 'friendly';
![Solution_03.png](:/b71dcf18fcce44c58577df5e719d173f)

**QUESTION 04:** Oh, that does not look good. Maybe other friendly smiths can help you out, e.g. a blacksmith. Try out: job LIKE '%smith' to find all inhabitants whose job ends with 'smith'.

**Solution 04:** SELECT * FROM INHABITANT WHERE job LIKE '%smith' AND state = 'friendly';

**QUESTION 05:**  No need to call me stranger! What's my personid? (Hint: Use a SELECT query without an asterisk. In former queries, the * stands for: all columns. Instead of the star, you can also address one or more columns (seperated by a comma) and you will only get the columns you need.)
**Solution 05:** SELECT personid FROM INHABITANT WHERE name = 'Stranger';
![Solution_05.png](:/8ce884659a1049cbbc72015ac86fe60c)

**QUESTION 06:** I can offer to make you a sword for 150 gold. That's the cheapest you will find! How much gold do you have?
**Solution 06:** SELECT gold FROM INHABITANT WHERE name = 'Stranger';
![Solution_06.png](:/eb66050cbdf946339f3df7ecbab96e3f)

**QUESTION 07:** Damn! No mon, no fun. There has to be another option to earn gold other than going to work. Maybe I could collect ownerless items and sell them! Can I make a list of all items that don't belong to anyone?
**Solution 07:** SELECT * FROM ITEM WHERE owner ISNULL;
![Solution_07.png](:/277f22c546034c20ab6223b378d4ac5a)

**QUESTION 08:** Do you know a trick how to collect all the ownerless items?
**Solution 08:** UPDATE ITEM SET owner = '20' WHERE owner ISNULL;

![Solution_08.png](:/081a3fd0be54498d933e73fa8fe45527)

**QUESTION 09:** Now list all of the items I have!
**Solution 09:** SELECT * FROM ITEM WHERE owner = '20';
![Solution_09.png](:/2a8d4bca66fe4b4eafee1f5f01493754)

**QUESTION 10:** Find a friendly inhabitant who is either a dealer or a merchant. Maybe they want to buy some of my items. (Hint: When you use both AND and OR, don't forget to put brackets correctly!)
**Solution 10:** SELECT * FROM INHABITANT WHERE (job = 'dealer' OR job = 'merchant') AND state = 'friendly';
![Solution_10.png](:/e158ae34be434d2a8cf9a2acdd358ed9)

**QUESTION 11:** I'd like to get the ring and the teapot. The rest is nothing but scrap. Please give me the two items. My personid is 15.
**Solution 11:** UPDATE ITEM SET owner = 15 WHERE item IN ('ring','teapot');
![Solution_11.png](:/3640571fed0f4766ae313337f8c44785)
**QUESTION 12:** Unfortunately, that's not enough gold to buy a sword. Seems like I do have to work after all. Maybe it's not a bad idea to change my name from Stranger to my real name before I will apply for a job.
**Solution 12:** UPDATE INHABITANT SET name = 'Ahmed' WHERE personid = 20;
![Solution_12.png](:/273c99abd6b1453abe9b6701eb7609be)

**QUESTION 13:** Since baking is one of my hobbies, why not find a baker who I can work for? (Hint: List all bakers and use 'ORDER BY gold' to sort the results. 'ORDER BY gold DESC' is even better because then the richest baker is on top.)
**Solution 13:** ![Solution_13.png](:/e0d79d063d2042ce95eb8c9476368e4c)
**QUESTION 14:** Is there a pilot on this island by any chance? He could fly me home.
**Solution 14:** SELECT * FROM INHABITANT WHERE job = 'pilot';
![Solution_14.png](:/fe2a0d6fbb144949b154ac35bff490ad)
**QUESTION 15:** Horrible, the pilot is held captive by Dirty Dieter! I will show you a trick how to find out the name of the village where Dirty Dieter lives. Thanks for the hint! I can use the join to find out the chief's name of the village Onionville. (Hint: In the column 'chief' in the village table, the personid of the chief is stored)
**Solution 15:** SELECT INHABITANT.name FROM VILLAGE,INHABITANT
ON VILLAGE.villageid = INHABITANT.villageid
WHERE VILLAGE.name = 'Onionville' 
AND INHABITANT.personid = VILLAGE.chief;
![Solution_15.png](:/c3f6fb661c3746d4bf501b2df4acc3f9)
**QUESTION 16:**  Hello Ahmed, the pilot is held captive by Dirty Dieter in his sister's house. Shall I tell you how many women there are in Onionville? Nah, you can figure it out by yourself! (Hint: Women show up as gender = 'f')
**Solution 16:** SELECT COUNT(*) FROM VILLAGE, INHABITANT
 ON VILLAGE.villageid = INHABITANT.villageid
 WHERE VILLAGE.name = 'Onionville' AND INHABITANT.gender = 'f';
![Solution_16.png](:/b6a5b0d648d1434080cc67608e08ed78)
 
**QUESTION 17:** Oh, only one woman. What's her name?
**Solution 17:** SELECT INHABITANT.name FROM VILLAGE, INHABITANT
 ON VILLAGE.villageid = INHABITANT.villageid
 WHERE VILLAGE.name = 'Onionville' AND INHABITANT.gender = 'f';
 ![Solution_17.png](:/407dc5ae93d542a69cca1f1b2769d88b)
**QUESTION 18:** Ahmed, if you hand me over the entire property of our nearby village Cucumbertown, I will release the pilot. I will show you now what this property consists of.
**Solution 18:** SELECT SUM(inhabitant.gold) FROM inhabitant, village WHERE village.villageid = inhabitant.villageid AND village.name = 'Cucumbertown';
![Solution_18.png](:/69e23301ac884fe88758659b1ec26e53)
**QUESTION 19:** Oh no, baking bread alone can't solve my problems. If I continue working and selling items though, I could earn more gold than the worth of gold inventories of all bakers, dealers and merchants together. How much gold is that?
**Solution 19:** SELECT SUM(gold) FROM INHABITANT WHERE job = 'baker' OR job = 'dealer' OR job = 'merchant';
![Solution_19.png](:/3b7bc5a8a5824a97b19d088f788d77fa)
**QUESTION 20:** For some reason, butchers own the most gold. How much gold do different inhabitants have on average, depending on their state (friendly, ...)?
**Solution 20:** SELECT state, AVG(gold) FROM INHABITANT GROUP BY state; 
![Solution_20.png](:/46db1f04ce10419f99a1004fed5f78b9)

**QUESTION 21:** Or I might as well go ahead and just kill Dirty Dieter with my sword! 
**Solution 21:** DELETE FROM inhabitant WHERE name = 'Dirty Dieter';
![Solution_21.png](:/215756506ed74324ba9dc34b66817ed9)

**QUESTION 22:** Heeeey! Now I'm very angry! What will you do next, Ahmed?
**Solution 22:** DELETE FROM INHABITANT WHERE name = 'Dirty Diane';
![Solution_22.png](:/cf3ca9f0ed45433d9c2f042075b2cf1f)
**QUESTION 23:** Yeah! Now I release the pilot!
**Solution 23:**  UPDATE INHABITANT SET state = 'friendly' WHERE job = 'pilot';
![Solution_23.png](:/ce61d586857c4e62b302129561db0240)

**QUESTION 24:** The game is over. Get your certificate of completion now! If you want to change the name on the certificate, use an UPDATE command on the inhabitants table.
**Solution 24:** UPDATE INHABITANT SET name = 'Your Name' WHERE personid = 20;
![Solution_24.png](:/1ba40a136db341edbaeebd860a53fb3b)
```
