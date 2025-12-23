# mongodb-playbook

22/12/2025
 SQL - NO-SQL  - Not Object Structured Query Language
------------
-> RDMBS -> Oracle , MySQL , SQL Server , DB2 

	Application(Object) -> store -> Database (Types) -> ORM

-> NO-SQL -> Mongo DB , Firebase , CouchDB -> Object DB 

Oracle              Mongo DB
--------------------------------
Database            Database
Tables              Collections -> Array of object 
Rows                Documents -> Object 
Columns             Fields -> prop of an object
===========================================================================================

Installation of Mongo DB (Local / Cloud)
------------------------
Issues
------
1. 'mongo' is not recognized as an internal or external command
	
	Resolution : Need to set the Path in system Env variables

2. Connection Failed to Connect MongoDB (If MongoDB Server is Down)
   
   Resolution : Start MongoDB server with "Windows Services"
                Ctrl + R => "services.msc"
============================================================================================

4 kind of operations with DB -> CRUD
CREATE , READ , UPDATE , DELETE

2 ways with DB Operations
-------------------------
1. using CMD -> Windows Commands for TEST / Static data
2. using Application -> Real Data / Dynamic Data -> mongoose
=======================================================================================
Command Line (Shell) CRUD Operations with MongoDB
-------------------------------------------------
Database : hcl_db
Table : employee
Fields : name , age , designation , location

show dbs
use <db_name>
db.createCollection('employee');
show collections

INSERT / CREATE Operations
------------------------------
db.employee.insertOne({
	name : 'Rajan',
	age : 25,
	designation : 'Software Engineer',
	location : 'Bangalore'
});

db.employee.insertOne({
	name : 'Mahesh',
	age : 28,
	designation : 'Sr.Software Engineer',
	location : 'Bangalore'
});

db.employee.insertMany([
	{
		name : 'John',
		age : 40,
		designation : 'Project Manager',
		location : 'Hyderabad'
	},
	{
		name : 'Wilson',
		age : 45,
		designation : 'Sr.Project Manager',
		location : 'Hyderabad'
	}
]);

READ Operations
------------------------------
db.employee.find() // SELECT * FROM EMPLOYEE;
db.employee.find().pretty()
db.employee.find({name : 'Rajan'}); // SELECT * FROM EMPLOYEE WHERE NAME = 'Rajan'
db.employee.find({_id : ObjectId("602683dc2398238d2bcdccc8")}); // SELECT * FROM EMPLOYEE WHERE ID = '4654'

UPDATE Operations
------------------
db.employee.updateOne({name : 'Mahesh'},
	{
		$set : {
			age : 30,
			designation : 'TechLead'
		}
	}
);

DELETE Operations
-----------------
db.employee.deleteOne({name : 'Wilson'});

Sort Rows
----------
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()

Count Rows
------------
db.posts.find().count()
db.posts.find({ category: 'news' }).count()

Limit Rows
-----------
db.posts.find().limit(2).pretty()

Chaining
---------
db.posts.find().limit(2).sort({ title: 1 }).pretty()

Foreach
---------
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})

Find One Row
---------------
db.posts.findOne({ category: 'News' })

Find Specific Fields
-----------------------
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})

Update Row
------------
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})

Update Specific Field
------------------------
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})

Increment Field (\$inc)
---------------------------
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})

Rename Field
---------------
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})

Sub-Documents
-----------------
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})

Find By Element in Array (\$elemMatch)
-------------------------------------------
db.posts.find({
  comments: {
     $elemMatch: {
       author: 'Mary Williams'
       }
    }
  }
)

Add Index
-------------
db.posts.createIndex({ title: 'text' })

Text Search
------------------
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})

Greater & Less Than
----------------------
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
=====================================================================================================
