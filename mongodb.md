### Create a new or switch databases


```other
use dbName
```


### Delete Database


```javascript
db.dropDatabase()
```


Copy

## 2. Collection Commands


### Show Collections


```javascript
show collections
```


Copy

### Create a collection named 'comments'


```javascript
db.createCollection('comments')
```


Copy

### Drop a collection named 'comments'


```javascript
db.comments.drop()
```


Copy

## 3. Row(Document) Commands


### Show all Rows in a Collection


```javascript
db.comments.find()
```


Copy

### Show all Rows in a Collection (Prettified)


```javascript
db.comments.find().pretty()
```


Copy

### Find the first row matching the object


```javascript
db.comments.findOne({name: 'Harry'})
```


```other
db.comments.find({lang: 'python',name:'chakshu'})
```


### Insert One Row


```javascript
db.comments.insert({
    'name': 'Harry',
    'lang': 'JavaScript',
    'member_since': 5
 })
```


Copy

### Insert many Rows


```javascript
db.comments.insertMany([{
    'name': 'Harry',
    'lang': 'JavaScript',
    'member_since': 5
    }, 
    {'name': 'Rohan',
    'lang': 'Python',
    'member_since': 3
    },
    {'name': 'Lovish',
    'lang': 'Java',
    'member_since': 4
}])
```


Copy

Search in a MongoDb Database

```javascript
db.comments.find({lang:'Python'})
```


Copy

### Limit the number of rows in output


```javascript
db.comments.find().limit(2)
```


Copy

### Count the number of rows in the output


```javascript
db.comments.find().count()
```


### Update a row


```javascript
db.comments.updateOne({name: 'Shubham'},
{$set: {'name': 'Harry',
    'lang': 'JavaScript',
    'member_since': 51
}}, {upsert: true})
```


Copy

### Mongodb Increment Operator


```javascript
db.comments.update({name: 'Rohan'},
{$inc:{
    member_since: 2
}})
```


Copy

### Mongodb Rename Operator


```javascript
db.comments.update({name: 'Rohan'},
{$rename:{
    member_since: 'member'
}})
```


Copy

### Delete Row


```javascript
db.comments.remove({name: 'Harry'})
```


Copy

### Less than/Greater than/ Less than or Eq/Greater than or Eq


```javascript
db.comments.find({member_since: {$lt: 90}})
```


Copy

```javascript
db.comments.find({member_since: {$lte: 90}})
```


Copy

```javascript
db.comments.find({member_since: {$gt: 90}})
```


Copy

```javascript
db.comments.find({member_since: {$gte: 90}})
```


![image](https://res.craft.do/user/full/df03ed4f-4af1-7826-400f-71f003504554/doc/CF55CFCE-79FB-4F7E-8530-4CE2FC53FDB5/60AD854B-D518-4D42-8F4E-A40D76F7DCA0_2/LidgMsgQNjaxIFsWfwO9N04Zdo40EUuHurE0fRAMHZUz/Image.png)
# MongoDB Shell Commands Cheat Sheet.

This is a Cheat Sheet for interacting with the Mongo Shell ( mongo on your command line). This is for MongoDB Community Edition.

## Preface:


[Mongo Manual](https://docs.mongodb.com/manual/mongo/) can help you with getting started using the Shell.

[FAQ for MongoDB Fundamentals](https://docs.mongodb.com/manual/faq/fundamentals/) and other FAQs can be found in the side-bar after visiting that link.

The Mongo Shell reference can be found [here](https://docs.mongodb.com/manual/reference/method/).

Anything that looks like `db.<something>()` will be found in [Database Methods](https://docs.mongodb.com/manual/reference/method/js-database/).

Anything that looks like `db.collection.<something>` will be found in [Collection Methods](https://docs.mongodb.com/manual/reference/method/js-collection/).

Use `db.help()` to get a list of all database commands. ( Note that it's pretty long.)

Anything in `< >` should be replaced with your unique values. IE: You want to have a database called `Cars` so you would use the command `use <db>` but you would type it as `use Cars`.

## Databases:

This table will list the commands most commonly used when working with the database as a whole. 

Type| Command| Description
:--- |:--- | :---
Create/Connect | `use <db>` | Connects to a specific database. If none exists then one will automatically be created with that name. [Doc](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell)
List All | `show dbs` | Lists all Databases. DBs with no data are not shown. [Doc](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell)
List Current| `db.getName()` | Lists the name of the currently selected databasse. [Doc](https://docs.mongodb.com/manual/reference/method/db.getName/#db.getName)
Return | `db` | Returns the currently seleceted Database. Allows you to use methods and chain commands. IE `db.createCollection('test')`. [Doc](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell)
Drop | `db.dropDatabase()` | Drops the currently selected Database. [Doc](https://docs.mongodb.com/manual/reference/method/db.dropDatabase/#db.dropDatabase)
Stats | `db.stats()` | Lists the stats about the current Database. [Doc](https://docs.mongodb.com/manual/reference/method/db.stats/#db.stats)

## Collections:

This Table lists the commands most commonly used when working with collections as a whole.

Type | Command | Description 
:--- | :--- | :---
Create | `db.createCollection('<collection>)` | Creates a new empty collection in the database. [Doc](https://docs.mongodb.com/manual/reference/method/db.createCollection/#db.createCollection)
List | `db.getCollectionNames()` | Lists all collections for a current Database. [Doc](https://docs.mongodb.com/manual/reference/method/db.getCollectionNames/#db.getCollectionNames)
Return | `db.getCollection('<collection>')` | Returns a collection. Can chain methods onto it. IE `db.getCollection.('authors').find({})`. [Doc](https://docs.mongodb.com/manual/reference/method/db.getCollection/)
Return/Create | `db.<collection>` | Similar to `db.getCollection()`, but if the collection doesn't exist, then the collection will be return, but not added unless data is also added to that collection at the same time. IE: `db.items` does not add a collection to the database, but `db.items.insertOne({name: 'Mike'})` would, because data is also being added to the collection. Use `db.createCollection()` to add an empty collection. [Doc](https://docs.mongodb.com/manual/reference/method/js-collection/)
Drop | `db.<collection>.drop()` | Drops the collection from the database. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.drop/#db.collection.drop)
Rename | `db.<cllectn>.renameCollection('collection')` | Renames a collection. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.renameCollection/#db.collection.renameCollection)

## Data

This section is broken down into 5 sub-sections. The first 4 match the CRUD Verbs of Create, Read, Update, Delete, and the last one is a list of Combos like `findAndUpdate`. Check here for the [Mongo Docs on Crud](https://docs.mongodb.com/manual/crud/)

Couple notes here:

1. All of these commands start with `db.<collection>` where `<collection>` is the name of the collection you want to call these methods on. Any exceptions will be noted in the description.**
2. `{query}` Is referring to queries like `{<field>: '<value>', <field>:'<value>', etc)`. IE: `{ book: 'Golden River Doth Flows', author: 'I.P. Freely', etc}`. They are field-value pairs that are used to make documents, and also used during searches, aka queries.

### Create

Type | Command | Description
:--- | :--- | :---
Create One | `.insertOne({<doc>})` | Inserts a document into the collection. IE: `db.cars.insertOne({make:"ford"})`. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/#db.collection.insertOne)
Create One/Many | `.insert([{<doc>},{<doc>},{<doc>}] )` | Inserts One or more documents into the collection. If an array is passed in it will make a record of each document in the array. Otherwise it will accept a single document. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.insert/#db.collection.insert)


### Read

Most of these commands allow methods to be chained onto them.

Type | Command | Description 
:--- | :--- | :---
Count | `.count()` | Returns the number of items in the collection. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.count/#db.collection.count)
Return All | `.find({})` | Returns an array of all items in a collection. `.find()` Must be passed `{}` in order to return all documents. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.find/#db.collection.find)
Return All Filtered| `.find({query})` | Returns an array of items in a collection that match the query passed into `.find()`. See [Query and Project Operators](https://docs.mongodb.com/manual/reference/operator/query/) for extra info on querys. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.find/#db.collection.find)
Return One Filtered | `.findOne({query})` | Returns a document (not an array) of the first item found, filtering based off what was passed into `.findOne()`. Useful when searching by unique fields like `_id`, IE `db.cars.findOne({_id: 1})`. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.findOne/#db.collection.findOne)

### Update

Type | Command | Description 
:--- | :--- | :---
Update/Replace | `.update({query}, { $set: {query} }, options)` | The first argument is used as the query to find the document. The second argument specifies which field which to update. Exclude `$set:` and the entire document will be Replaced. Common options: `upsert: <boolean>` to keep it unique, and `multi: <boolean>` will update multiple documents if set to true. [Docs](https://docs.mongodb.com/manual/reference/method/db.collection.update/#db.collection.update) and [Field Operator Docs](https://docs.mongodb.com/manual/reference/operator/update-field/)
Update One/Many | `.updateOne()` and `.updateMany()`| Basically the same as the above function, except the `multi: <boolean>` option is basically defaulted to `false` and `true`, and isnt' an allowed option that can be passed in. [One Doc](https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/#db.collection.updateOne), [Many Doc](https://docs.mongodb.com/manual/reference/method/db.collection.updateMany/#db.collection.updateMany)

### Delete

Type | Command | Description 
:--- | :--- | :---
Delete One | `.deleteOne({query})` | Deletes the first document that matches the query. Recommend to search by `_id` or another unique field. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.deleteOne/#db.collection.deleteOne)
Delete Many/All | `.deleteMany({query})` | Deletes all records that match the query. Leave the query blank to delete all documents. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.deleteMany/#db.collection.deleteMany)


### Combos

These are some combo commands that really just do the same thing as their base commands, but have a couple extra options.

All of these can leave their `{query}` blank and it will find the first document and execute it's verb on that item.

Command | Desctiption
:--- | :---
`.findOneAndDelete({query})` | Finds the first document that matches the query and deletes it. [Doc] https://docs.mongodb.com/manual/reference/method/db.collection.findOneAndDelete/#db.collection.findOneAndDelete
`.findOneAndUpdate({query}, {<update>}, {<options>})` | Finds the first document that matches the query in the first argument, and updates it using the second arguments. Has optional options as well. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.findOneAndUpdate/#db.collection.findOneAndUpdate)
`.findOneAndReplace({query}, {<replacement>}, {<options>})` | Finds and replaces the document that matches the query. `<replacement>` cannot use update operators. [Doc](https://docs.mongodb.com/manual/reference/method/db.collection.findOneAndReplace/#db.collection.findOneAndReplace)

