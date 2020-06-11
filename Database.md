# _Database_

---

# _Models, Schemas, Entities_

## Schema

- A database schema is close to the implementation details and tells the database (and developer) how an entity (e.g. user entity) looks like in a database table whereas every instance of an entity is represented by a table row
- For instance, the schema defines fields (e.g. username) and relationships (e.g. a user has messages) of an entity
- Each field is represented as a column in the database
- Basically a schema is the blueprint for an entity

## Model

- A database model is a more abstract perspective on the schema
- It offers the developer a conceptual framework on what models are available and how to use models as interfaces to connect an application to a database to interact with the entities
- Often models are implemented with ORMs

## Entity

- A database entity is actual instance of a stored item in the database that is created with a database schema
- Each database entity uses a row in the database table whereas each field of the entity is defined by a column
- A relationship to another entity is often described with an identifier of the other entity and ends up as field in the database as well

---

# _Non-Relational_

- Mostly unstructured
- Like a giant JavaScript Object
- Allows irregular data types to be stored more easily
  - Allows for a more nested data structure as you can store lists and objects in any field
- Do not have structured mechanisms for linking data between tables
  - No SQL means we have to do manual linking of our data records which can get ugly pretty fast, but it also means it’s safe from SQL injection attacks
- Avoid nesting data
  - When you fetch data at a location in your database, you also retrieve all of its child nodes
  - It allows has to traverse through all parents node to get to the requested data
  - In addition, when you grant someone read or write access at a node in your database, you also grant them access to all data under that node
  - Therefore, in practice, it's best to keep your data structure as flat as possible
- Denormalization
  - Data is instead split into separate paths

```
*// Notice: footnotes are stored as an array directly within*
*// the research paper object, and they do not need a key*
*// to reference the publication
*
*// Research Papers:
*
[{
 'id': 1,
 'title': 'Lorem Ipsum Dolor',
 'publicationDate': 1493673656502,
 'footnotes': [{
    'id': 1
    'pageNumber': 26,
    'note': 'Dolor set amet consequetar'
  },
  {
    'id': 2
    'pageNumber': 362,
    'note': 'Consequetar adipscing'
  },
  {
    'id': 3
    'pageNumber': 75,
    'note': 'Lorem set amet'
  }]
}];
```

---

# _Relational_

- Helps avoids nesting and duplication of data (nomalization)
- Connect (reference) data with something that doesn't change
  - Reference a username with a userID
- Stores data in tables with rows and columns
  - Similar to an excel spreadsheet
- Requires a strict, pre-defined schema
  - You must know the exact fields and their data types for each column of every table, and each record must conform to the defined structure
- Uses SQL to access and manipulate data points
  - Allows you to link information from different tables through unique keys (foreign and primary)
- Every table should have a unique identifier ID for a row or piece of data (primary key(PK))
  - Database table determines with PK should be
    - Auto-incrementing primary key (AIPK)

* Schema
  - The definition of your data structure
  - It provides a blueprint for the tables in your database and the relationships between them
  - Within each table, you also need to define the types of data that can be stored in each column
* Primary Key
  - A key in a relational database that is unique for each record
  - It is a unique identifier
  - You must have one and only one primary key
* Foreign Key
  - A field in one table that uniquely identifies a row of another table
  - A foreign key is defined in a second table, but it refers to the primary key in the first table

```
// Requires two separate tables: one for research papers
// and another for footnotes
// Each footnote must contain a 'publicationId' field (foreign key)
// to link it to a specific paper

// Scheme:

researchPapers: id, title, publicationDate;
footNotes: id, page, note, publicationId;
```

### researchPapers:

| id  | title            | publicationDate |
| --- | ---------------- | --------------- |
| 1   | Lorem Ispum      | 2345635682547   |
| --- | ---              | ---             |
| 2   | Dolor Set Amet   | 3568356245622   |
| 3   | Consequetar Adip | 5795673456278   |

### footNotes:

| id  | page | publicationId | note                         |
| --- | ---- | ------------- | ---------------------------- |
| 1   | 26   | 1             | ‘Dolor set amet consequetar’ |
| --- | ---  | ---           | ---                          |
| 2   | 362  | 1             | ‘Consequetar adipscing’      |
| 3   | 75   | 2             | ‘Lorem set amet’             |

---

# _SQL_

- Structured Querying Language
- http://sql-by-repetition.herokuapp.com/

* `CREATE DATABASE <databasename>;`
  - create a new database
* `DROP DATABASE <databasename>;`
  - deletes a database
* `CREATE TABLE <tablename> (colum names);`
  - creates a table in a database
* `SELECT * FROM <tablename>;`
  - accesses rows
  - `*` selects all rows
* `SELECT * FROM students WHERE program='data'`
  - filters rows
* `INSERT INTO <tablename> (columns) VALUES ('data');`
  -
* `DELETE FROM students WHERE id='1';`
  -
* `CREATE ROLE`
  - A role is an entity that can function as a user and/or as a group
* `CREATE USER`
  - an alias for `CREATE ROLE`
* Commands don't have to be all caps

## Databas Management Systems (DBMS)

- Uses SQL to communicate with a relational database

---

# _PostgreSQL_

- https://www.robinwieruch.de/postgres-sql-windows-setup/

## Setup

- Install Postgres
  - Installing PostgreSQL on Windows with the PostgreSQL "One-click" installer packaged by EnterpriseDB, `psql` is not added to the `PATH` automatically
    - Add `psql` to the user `PATH` environment variable with:
      - `;C:\Program Files\PostgreSQL\11\bin;C:\Program Files\PostgreSQL\11\lib`
      - Update version number if needed
- The `postgres` user will be the only user on your system that can open the PostgreSQL prompt without defining a database, which means `postgres` is the only user who can administer PostgreSQL
- For a fresh install, the default user is `postgres` and the password should be blank
  - If using EDB installer, you specified one during installation so skip this step
  - Set a password
    - `psql -U postgres`
    - `ALTER USER postgres`WITH PASSWORD`'somepass';`
- By default, `psql` tries to connect to the PostgreSQL server using the same user name as your system user
- In order to make connecting easier, create a user with the same name as your system user
  - `CREATE USER someuser;`
  - `ALTER USER someuser`WITH PASSWORD`'someuserpass';`
  - `ALTER USER someuser SUPERUSER CREATEDB;`
  - `CREATE DATABASE someuser;`
- If you see:
  - WARNING: Console code page (437) differs from Windows code page (1252) 8-bit characters might not work correctly. See psql reference page "Notes for Windows users" for details.
  - Run in the terminal:
    - `cmd.exe /c chcp 1252`

## Commands

- `psql`
  - enters the PostgreSQL console
- `\l`
  - list all databases
- `\c <databasename>`
  - connect to a particular database
- `\dt`
  - after you’re connected to a database, show the tables it contains
- `\d <tablename>`
  - list all columns in a table
  - must connect to a database first
- `\q`
  - quit
- `\du`
  - show users

## Misc

### Unsigned Integers

- All integer types can have an optional (nonstandard) attribute UNSIGNED
- Unsigned type can be used to permit only nonnegative numbers in a column or when you need a larger upper numeric range for the column
- For example, if an INT column is UNSIGNED, the size of the column's range is the same but its endpoints shift from -2147483648 and 2147483647 up to 0 and 4294967295.

---

### SQLite

### MySQL

---

# _Knex_

- Translates SQL into JavaScript
- Promise based

* `npm install -g knex`
  - must be installed globally as well as locally
* `npm install knex --save`
* `npm install pg --save`
  - interface between knex and postgess

- `knex init`
  - creates `knexfile.js`
    - has configs for different environments
      - development

```
development: {
    client: 'pg',
    connection: 'postgres://localhost/publications',
    migrations: {
      directory: './db/migrations'
    },
    useNullAsDefault: true
  }
```

            * staging
            * production

## Creating a schema

- Use migrations
  - sort of like commits
- Create a migration
  - run `knex migrate:make initial`
    - `initial` is a descriptor of what the migration is doing

* `up` defines what should happen when we run the migration
  - (i.e. What changes do we want to make to our database?)
* `down` is the reverse
  - always does the reverse of exports.up
  - If we want to roll back to a previous version, then `down` undoes whatever `up` did
* For every `up` there must be an equal and opposite `down` that will allow us to rollback those changes

## Up

- `table.increments('id').primary();`
  - Creates a primary key

* `table.integer('paper_id').unsigned()`

  - Creates an ID

* `table.foreign('paper_id').references('papers.id');`

  - Creates a foreign key

* `table.timestamps(true, true);`
  - Creates columns
    - `created_at`
    - `updated_at`

## Down

- Order of dropping tables matters
  - Knex won't delete a table with dependencies (foreign keys) that are not found

```
exports.down = function(knex, Promise) {
  return Promise.all([
    knex.schema.dropTable('footnotes'),
    knex.schema.dropTable('papers')
  ]);
};
```

## Running Your Migrations

- You must run your migrations for them to take effect
- You can run all of your migrations to the latest point with the following command:
  - run `knex migrate:latest --env development`

## Updating Your Schema

- Add a new column after table is created
- `knex migrate:make add-publisher`

```
exports.up = function(knex, Promise) {
  return Promise.all([
    knex.schema.table('papers', function(table) {
      table.string('publisher');
    })
  ]);
};

exports.down = function(knex, Promise) {
  return Promise.all([
    knex.schema.table('papers', function(table) {
      table.dropColumn('publisher');
    })
  ]);
};
```

- run `knex migrate:latest --env development`

## Seed file

- Some default data
- Programmatically inserts data into database tables
- Use to populate your database with some fake data

* add to `knexfile.js`:

```
`seeds: {directory: './db/seeds/dev'},`
```

- run `knex seed:make papers --env development`

- if you have multiple seeds, run them in alphabetical order
- will delete all existing data
  - only use to initiate or test a database
- insert
  - `.insert(data, [returning])`
  - `returning` is important to return the primary ID of the entry to use as a foreign key

```
knex('papers').insert({
  title: 'Fooo', author: 'Bob', publisher: 'Minnesota'
}, 'id')
.then(paper => {
  return knex('footnotes').insert([
    { note: 'Lorem', paper_id: paper[0] },
    { note: 'Dolor', paper_id: paper[0] }
  ])
})
```

- run `knex seed:run` --env development`` to add the seed data

* add some configuration to work with the knex database:

```
// server.js

// use environment from confing, or development by default
const environment = process.env.NODE_ENV || 'development';
// get config
const configuration = require('./knexfile')[environment];
// use config
const database = require('knex')(configuration);
```

---

# _Misc_

- One-to-many relationship
  - One item can have many sub-items
- Many-to-many relationship
  - One-to-Many relationship both ways

## Mapping endpoints to Schema

- tables
  - papers
    - columns
      - ID, title, author, publisher
  - footnotes
    - columns
      - ID, note, paper_id

---

# _Server-side testing_

- Use:
  - `npm install -D mocha chai chai-http`
  - Mocha
    - add test run command to package.json

```
"scripts": {
 "test": "NODE_ENV=test mocha --exit"
 },
```

        * run `npm test`
    * Chai
    * Chai-HTTP

```
const chai = require('chai');
const should = chai.should();
const chaiHttp = require('chai-http');
const server = require('../server');

chai.use(chaiHttp);

describe('CLIENT routes', () => {});

describe('API routes', () => {});
```

- Step 1
  - Set up the database
    - structure (migrations)
      - use `before()`
    - records (seeds)
      - `knex seed:make <seedName> --env test`
      - use `beforeEach()`
        - clear the records
- Step 2
  - Make request to server route
- Step 3
  - Get response from server
- Step 4
  - Test response
    - Check:
      - status code
      - content type
      - content of body
      - data structure
        - i.e. object, array
- Step 5
  - Clean up database
    - rollback

---

# _Environments_

- An environment is the setup of where the code is running

- Developement
  - setup for developing
  - local to you
- Testing
  - uses mock data
- Staging
  - intermediate step between development and production
  - close to production as possible
  - uses production environment
  - accessible by team
- Continuous Integration (CI)
  - runs tests and reports results
  - if passes, automatically deploys
- Production
  - live app

## _Environment Variable_

- They define your environment

---

# _Firebase_

- `npm install -S firebase`
- F~~i~~rebase stores data as a giant object with key-value pairs
  - Unlike JSON or JavaScript objects, there are no arrays in Firebase

* Setup
  - https://css-tricks.com/intro-firebase-react/

```
// src/private/firebase.js

export const config = {
  apiKey: "AIzaSyDblTESEB1SbAVkpy2q39DI2OHphL2-Jxw",
  authDomain: "fun-food-friends-eeec7.firebaseapp.com",
  databaseURL: "https://fun-food-friends-eeec7.firebaseio.com",
  projectId: "fun-food-friends-eeec7",
  storageBucket: "fun-food-friends-eeec7.appspot.com",
  messagingSenderId: "144750278413"
};

// src/firebase.js

import firebase from 'firebase'
import { config } from '../private/firebase';

firebase.initializeApp(config);

// for auth
export const provider = new firebase.auth.GithubAuthProvider();
export const auth = firebase.auth();

export default firebase;
```

---

# _indexedDB_

## Dexie

- http://dexie.org/docs/
- The basic pattern that IndexedDB encourages is the following:
  - Open a database.
  - Create an object store in the database.
  - Start a transaction and make a request to do some database operation, like adding or retrieving data.
  - Wait for the operation to complete by listening to the right kind of DOM event.
  - Do something with the results (which can be found on the request object).
- With these big concepts under our belts, we can get to more concrete stuff.
- you declare what tables and schemas you have in current and previously released versions and you let Dexie / indexedDB handle the situation where a database wasn’t created yet, needs upgrade or is already on latest version).

* .add = post
* .put = put
* `put()` and `add()`. `add()` can only be used for inserting objects, `put()` is either an insert or an update operation depending if the object with that primary key already exists

```
const db = new Dexie('keys');

   // out-of-line primary key

   db.version(1).stores({
       simple: ''
   });

   db.simple.add('one', 1); // insert
   //db.simple.add('another one', 1); //throws an error
   db.simple.add('two', 2); // insert
   db.simple.put('three', 3); // insert
   db.simple.put('Three', 3); // update

   // get something
   const value = await db.simple.get(3);
   // Three


   // out-of-line auto generated

   const db = new Dexie('keys');
   db.version(1).stores({
       simple: '++'
   });

   db.simple.add('one'); // insert
   db.simple.add('two'); // insert
   db.simple.put('three'); // insert
   db.simple.put('Three', 3); // update

   const value = await db.simple.get(3);
   // Three
```

- get
  - To access the record with the `get()` method you need to provide an array and specify the values in the same order as defined in the index definition

* To add or delete an index you create a new version and provide the new schema definition. If you want to delete an index you omit it from the definition

```
db.version(2).stores({
   contacts: 'id,name,city'
});
```

```
const db = new Dexie('AppDatabase');
db.version(1).stores({
   contacts: 'id,name,&email,*hobbies,[postCode+city]'
});
db.contacts.add({
   id: 1,
   name: 'John',
   email: 'john@test.com',
   hobbies: ['Reading', 'Traveling', 'Cycling'],
   postCode: 11111,
   city: 'BigCity'
});
```

---

# _pgAdmin_

- Setup
  - Click 'Add new server'
  - Name: localhost
  - Connection → Host name: localhost

* View data
  - Schemas → Public → Tables → right-click table → View/Edit Data → All Rows

---
