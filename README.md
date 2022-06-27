# Xenon-ReadMe
Setting-up steps (for local runs):

1. add all the needed configurations (e.g. connecting DB creds, Auth creds etc.) in the _.env_ root file
2. _npm install_
3. _npx directus bootstrap_
4. _npx directus schema apply ./xenon_db.yaml_
5. _npx directus start_
6. open *http://0.0.0.0:8055/*
7. enjoy yourself =)

Notes:

- requirements: Node 12.20+, PostgreSQL 10+ (since only this kind of DB is currently using by us)
- (if wanna run PostgreSQL server like a docker container) _docker pull postgres_ (pull the image from Docker Hub) & _docker run --name postgres-directus -p 5432:5432 -e POSTGRES_PASSWORD=root -e POSTGRES_USER=root -e POSTGRES_DB=xenon -d postgres_ (to run it with the creds that are currently in the ./.example.env configs by default)

##############################################################################################

Adding new test table(-s):

- analyse which tables (relations) are you planning to add for a newly creating/updating question (according to a set of tables which are using by this current question, e.g. that enlisted in the _proper_query_ field's query string) and add their names ("clear" ones, with out of "_<question_id>" postfix) to the corresponding question's \_served_tables_ field's enums set (from its relation's schema: Project settings -> Data model -> Questions -> edit _served_tables_ field -> Interface tab -> Choices -> Create New);

### Step 1: Add New Served Tables Enum Option
Go to https://staging-api.datalemur.com/admin/settings/data-model/Questions/served_tables then click on Interface Tab the click 'Create New' to add a new served table option.  

![](https://i.ibb.co/JKRPdS5/Step-1-Served-Tables-New-Enum-Choice.png)

Add the name of the table(s) **WITHOUT THE QUESTION ID** for both the text and value.

![](https://i.ibb.co/dtbFm8j/Step-1-Trades-Enum.png)


### Step 2: For A Specific Question, Pick The Table(s) To Serve
Go to the specific question (for example, for question #8 we go to https://staging-api.datalemur.com/admin/content/Questions/8) and then go to the 'Served Tables' field and pick the names of the served tables! 

![](https://i.ibb.co/GP28xrB/Step-2-Questions-Served-Tables.png)

### Step 3: Create The Table
Go to https://staging-api.datalemur.com/admin/settings/data-model/+ to create a new table - name the table **WITH THE QUESTION ID** in the name.
For example, because the trades table is associated with question #8, we name the table: trades_8

![](https://i.ibb.co/hfmS1V2/Screen-Shot-2022-06-20-at-9-08-07-PM.png)

### Step 3: Create The Table's Columns

See below brief explanation of the possible fields.

- Input - regular string/integer/etc. values
- Markdown -  formatted text with a special syntax
- Datetime - all using dates by its formats (e.g. timestamp)
- Toggle - boolean flag-values
- Dropdown - enum-settled field that allows to select a SINGLE option from the opening list (storing like a plain string/integer/etc. value)
- Dropdown (Multiple) - enum-settled field that allows to select a MULTIPLE options from the opening list (storing like an ARRAY of values)
- Many to One (Many to Many, One to Many) - field adding like a foreign key for making a corresponding relationship between two DB relations (e.g. Comment.question_id -> Question.id)

### Step 4: Add sample data/rows to the newly created tables.

For example, go to https://staging-api.datalemur.com/admin/content/users_8 to add rows to users_8 table. 




