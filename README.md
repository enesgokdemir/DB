# Meals DB

Hello, today we will do a database design together with you.

Design a Meals_DB database for cookery book according to the following:
- create the following tables:
**Ingredients, Dishes, Categories, Meals**
- Database should contain the following relationships:
**Prepared_by, Meal_Contains**
- Dishes are prepared with specified ingredients in specified amounts and each dish has calories details.

Sample Data (from more than one table):

**Lentil Soup:** (1 onion, 2 carrots, 2 cloves garlic, one cup of lentil), 139 calories

**Mushroom Soup:** (2 onion, 4 cloves garlic, 750-gram mushroom, one cup cream), 96 calories

**Green Salad:** (1 tomato, one cucumber, 1 lettuce, 0.5 onion, 0.5 cup olive oil, half limon), 9 calories

**Roka Salad:** (2 onion, 2 cups of roka, 1 tomato, 0.5 cup parmesan cheese, 0.5 cup olive oil, half limon, 0.25 cup balsamic vinegar), 120 calories

**Chicken Rice:** (1 cup rice, 600-gram chicken, 0.5 cup chickpeas), 607 calories

**Spaghetti bolognese:** (400 gram spaghetti, 500 gram beef mince, 100 gram tomato paste, 2 onion, 2 cloves garlic, 0.5 cup parmesan cheese), 667 calories


Dishes have got well-defined categories (e.g. soups, main dish, etc.)

Meals have a certain degree of difficulty, preparation time.

**Meal 1:** (Lentil soup, Green salad, Chicken Rice), Difficult, 60 minutes 

**Meal 2:** (Mushroom soup, Roka salad, Spaghetti Bolognese), Easy, 45 minutes

**Meal 3:** (Lentil soup, Roka salad, Chicken Rice), Difficult, 75 minutes

**Meal 4:** (Lentil soup, Green salad, Spaghetti bolognese), Medium, 60 minutes


**SQL command to create the database:**

create database Meals_DB;

**SQL command to create one of the tables:**

create table Ingredients (Ingredients_id int,Ingredients_name varchar(15),Ingredients_calories int);

create table dishes(dishes_id int,dishes_name varchar(15),ingredients1 int,ingredients2 int,ingredients3 int,ingredients4 int,ingredients5 int,ingredients6 int,calories int);

create table categories(category_id int,category_name varchar(15));

create table meals(meals_id int,soups int,salad int,difficulty varchar(15),times int);

create table meal_contains(m_id int,meal_id int,dish_id int);

create table prepared_by(prep_id int,dish_id int,ing_id int,amount varchar(30));

**Screenshot of the relationships diagram**

![image](https://user-images.githubusercontent.com/108132038/200850456-f923d195-e4b4-4149-9d3e-6b1042f3cb4b.png)

**SQL commands to insert data into one of the tables:**

INSERT INTO categories(category_name)values('Soup');

**Insert the sample data (mentioned in the first section) in the appropriate tables.**

Screenshot:

![image](https://user-images.githubusercontent.com/108132038/200850826-3118414c-f05f-44f7-ab2d-db8e38cde4ca.png)

![image](https://user-images.githubusercontent.com/108132038/200850878-86d65b89-712b-49fc-9515-1716cded143f.png)

![image](https://user-images.githubusercontent.com/108132038/200850894-48f4a83c-fb2e-416e-b0bb-3640a27a4712.png)

![image](https://user-images.githubusercontent.com/108132038/200850909-c79cb27a-8a1c-4f53-9d15-b26a56d6f549.png)

![image](https://user-images.githubusercontent.com/108132038/200850928-1b97c7b1-150a-4e9d-810e-4e5101d43140.png)

**SQL command to list all salads in descending order according to calories.**

select  dishes.dishes_name,dishes.calories,categories.category_id From dishes inner join categories on dishes.category_id=categories.category_id  order by category_id DESC

![image](https://user-images.githubusercontent.com/108132038/200851306-9f011ecb-9be5-4853-97ab-c4c644e1fe84.png)

**SQL command to list all the ingredients that contains the letter “g”**

select * from Ingredients where Ingredients_name LIKE '%g%';

![image](https://user-images.githubusercontent.com/108132038/200851451-df491ad2-5441-4ac0-8032-31e3a4147d0a.png)

**SQL command to find the number of ingredients for each Dish.**

select dishes.dishes_name,count(prepared_by.dish_id) from prepared_by inner join dishes on dishes.dishes_id = prepared_by.dish_id GROUP BY dishes.dishes_name,dishes_id;

![image](https://user-images.githubusercontent.com/108132038/200851608-96883754-69ea-4dc3-a4c6-537b721d88a1.png)

**SQL command to find the difficulty of the meal that has the maximum preparation time.**

select max(times) from meals 

![image](https://user-images.githubusercontent.com/108132038/200851741-2f942fea-72c8-4c86-bf4b-6e2d8c7bbe07.png)

**SQL command to find the dishes which calories is less than 100 or is a main dish.**

select * from dishes where calories<100 or category_id=4 

![image](https://user-images.githubusercontent.com/108132038/200851843-460a5aa6-4df5-4440-851d-1ad810ccbe7e.png)

**SQL command to find the meals that take 60 minutes to pe prepared and are easy or medium.**

select * from meals where difficulty='Medium' or difficulty='Easy' or times=60

![image](https://user-images.githubusercontent.com/108132038/200851979-4d69f439-d185-4023-96ef-bddb07cb9bdf.png)

**SQL command that modify the Dishes table by adding the “Origin” attribute.**

alter table dishes add  Origin varchar(15)

**SQL command that modify the Origin of Spaghetti bolognese to ‘Italy’**

update dishes set origin='Italy' where dishes_name='Spaghetti Bolognese'

![image](https://user-images.githubusercontent.com/108132038/200852238-9d2415a5-6a2b-48e9-b920-34b7a78d84fa.png)

**SQL command that display the dishes and details of the third meal.**

select dishes.dishes_name,meals.difficulty,dishes.calories,categories.category_name from meal_contains 
inner join meals on meals.meals_id=meal_contains.meal_id
inner join dishes on dishes.dishes_id=meal_contains.dish_id
inner join categories on categories.category_id = dishes.category_id where
meal_contains.meal_id=3

![image](https://user-images.githubusercontent.com/108132038/200852443-4255b99a-5155-4f79-b6e3-f82a677e3f83.png)

**SQL command that display the preparation details of Green Salad.**

select dishes.dishes_name,Ingredients.Ingredients_name,prepared_by.amount from prepared_by
inner join dishes on dishes.dishes_id=prepared_by.dish_id
inner join Ingredients on Ingredients.Ingredients_id=prepared_by.ing_id

![image](https://user-images.githubusercontent.com/108132038/200852581-7018d1f0-69c6-4108-9203-f11d78fc1fdc.png)

**SQL command that modifies the tomato amount of the Green salad to be two**

update prepared_by set amount='two' where dish_id=3 and ing_id=7

![image](https://user-images.githubusercontent.com/108132038/200852680-168f953f-1485-4c74-895a-045b32c528d3.png)

**SQL command that displays the Category names of dishes that contain parmesan cheese**

select  categories.category_name from prepared_by inner join
dishes on dishes.dishes_id=prepared_by.dish_id 
inner join categories on categories.category_İd=dishes.category_id
where prepared_by.ing_id=13

![image](https://user-images.githubusercontent.com/108132038/200852816-49dbdb7f-1047-4608-8f31-0d76f7e61593.png)

























