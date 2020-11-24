## RDF METADATA EXTRACTOR FROM PROJECT GUTTENBERG

#### THE CHALLENGE

The challenge is to build a metadata extractor from project Gutenberg <br/>
titles which are available here: <br/>
​https://www.gutenberg.org/wiki/Gutenberg:Feeds <br/>
(​https://www.gutenberg.org/cache/epub/feeds/rdf-files.tar.zip​)

Each book has an RDF file which will need to be processed to extract the:
```
* id (will be a number with 0-5 digits)
* title
* author/s
* publisher (value will always be Gutenberg)
* publication date
* language
* subject/s
* license rights
```
**Note:** For some books all of the data won't be available.

**YouTube link:** https://www.youtube.com/watch?v=moq1hvXSMw0


#### BEFORE USAGE

Install deps:
```bash
npm install
```

Configure proper database connection string in `.env` file:
```
DATABASE_CONNECTION_STRING=mysql://root:password@127.0.0.1:3306/rdf
```

Login to database interface and create database (for MySQL):
```
mysql -u root -p

> CREATE DATABASE rdf;
> exit;
```
or use favourite database GUI (IDE) to create the database: 
* MySQL Workbench,
* Toad MySQL
* JetBrains DataGrip 
* Sequel Pro

Run database migrations:
```bash
npm run db:migrate
```

----

#### USAGE

Download and import all RDFs:
```bash
npm run import
```

Import RDF file(s):
```bash
npm run parse path/to/file.rdf path/to/another.rdf ...
```
example (single): 
```bash
npm run parse test/samples/pg1.rdf

File: test/samples/pg1.rdf
id: "1"
title: "The Declaration of Independence of the United States of America"
authors: [{"id":"1638","name":"Jefferson, Thomas","aliases":["United States President (1801-1809)"]}]
publisher: "Project Gutenberg"
published: "1971-12-01"
language: "en"
rights: "Public domain in the USA."

----
```
example (multiple):
```bash
npm run parse test/samples/pg1.rdf test/samples/pg2.rdf 

File: test/samples/pg1.rdf
id: "1"
title: "The Declaration of Independence of the United States of America"
authors: [{"id":"1638","name":"Jefferson, Thomas","aliases":["United States President (1801-1809)"]}]
publisher: "Project Gutenberg"
published: "1971-12-01"
language: "en"
rights: "Public domain in the USA."

----

File: test/samples/pg2.rdf
id: "2"
title: "The United States Bill of Rights\r\nThe Ten Original Amendments to the Constitution of the United States"
authors: [{"id":"1","name":"United States","aliases":["U.S.A."]}]
publisher: "Project Gutenberg"
published: "1972-12-01"
language: "en"
rights: "Public domain in the USA."

----
```

----

Tests:
```bash
npm test
```

Coverage:
```bash
npm run coverage
```
