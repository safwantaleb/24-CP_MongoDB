Microsoft Windows [Version 10.0.19042.928]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Safwan Taleb>mongo
MongoDB shell version v4.4.5
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("33a14d00-63ac-4f91-8b1f-77ce3b332cb4") }
MongoDB server version: 4.4.5
---
The server generated these startup warnings when booting:
        2021-04-20T10:22:48.750+01:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
---
---
        Enable MongoDB's free cloud-based monitoring service, which will then receive and display
        metrics about your deployment (disk utilization, CPU, operation statistics, etc).

        The monitoring data will be available on a MongoDB website with a unique URL accessible to you
        and anyone you share the URL with. MongoDB may use this information to make product
        improvements and to suggest MongoDB products and deployment options to you.

        To enable free monitoring, run the following command: db.enableFreeMonitoring()
        To permanently disable this reminder, run the following command: db.disableFreeMonitoring()
---
> show dbs
admin       0.000GB
config      0.000GB
crsMongoDB  0.000GB
local       0.000GB
> use contact
switched to db contact
> db.createCollection('contactlist')
{ "ok" : 1 }
> show dbs
admin       0.000GB
config      0.000GB
contact     0.000GB
crsMongoDB  0.000GB
local       0.000GB
> use contact
switched to db contact
> show collections
contactlist
> db.contactlist.insertMany([{Last_name: 'Ben Lahmer', First_name: 'Fares', Email: 'fares@gmail.com', age:26},{Last_name: 'Kefi', First_name: 'Seif', Email: 'kefi@gmail.com', age:15},{Last_name: 'Fatnassi', First_name: 'Sarra', Email: 'sarra.f@gmail.com', age:40},{Last_name: 'Ben Yahia', First_name: 'Rym', age:4},{Last_name: 'Cherif', First_name: 'Sami', age:3}])
{
        "acknowledged" : true,
        "insertedIds" : [
                ObjectId("607f67442a05f058067b8abc"),
                ObjectId("607f67442a05f058067b8abd"),
                ObjectId("607f67442a05f058067b8abe"),
                ObjectId("607f67442a05f058067b8abf"),
                ObjectId("607f67442a05f058067b8ac0")
        ]
}
> db.contactlist.find().pretty()
{
        "_id" : ObjectId("607f67442a05f058067b8abc"),
        "Last_name" : "Ben Lahmer",
        "First_name" : "Fares",
        "Email" : "fares@gmail.com",
        "age" : 26
}
{
        "_id" : ObjectId("607f67442a05f058067b8abd"),
        "Last_name" : "Kefi",
        "First_name" : "Seif",
        "Email" : "kefi@gmail.com",
        "age" : 15
}
{
        "_id" : ObjectId("607f67442a05f058067b8abe"),
        "Last_name" : "Fatnassi",
        "First_name" : "Sarra",
        "Email" : "sarra.f@gmail.com",
        "age" : 40
}
{
        "_id" : ObjectId("607f67442a05f058067b8abf"),
        "Last_name" : "Ben Yahia",
        "First_name" : "Rym",
        "age" : 4
}
{
        "_id" : ObjectId("607f67442a05f058067b8ac0"),
        "Last_name" : "Cherif",
        "First_name" : "Sami",
        "age" : 3
}
> db.contactlist.find({_id: ObjectId("607f67442a05f058067b8abe")}).pretty()
{
        "_id" : ObjectId("607f67442a05f058067b8abe"),
        "Last_name" : "Fatnassi",
        "First_name" : "Sarra",
        "Email" : "sarra.f@gmail.com",
        "age" : 40
}
> db.contactlist.find({age: {$gt: 18}}).pretty()
{
        "_id" : ObjectId("607f67442a05f058067b8abc"),
        "Last_name" : "Ben Lahmer",
        "First_name" : "Fares",
        "Email" : "fares@gmail.com",
        "age" : 26
}
{
        "_id" : ObjectId("607f67442a05f058067b8abe"),
        "Last_name" : "Fatnassi",
        "First_name" : "Sarra",
        "Email" : "sarra.f@gmail.com",
        "age" : 40
}
> db.contactlist.find({$and: [{age: {$gt: 18}},{Last_name: /ah/}]}).pretty()
{
        "_id" : ObjectId("607f67442a05f058067b8abc"),
        "Last_name" : "Ben Lahmer",
        "First_name" : "Fares",
        "Email" : "fares@gmail.com",
        "age" : 26
}
> db.contactlist.update({Last_name: 'Kefi'},{$set:{First_name: 'Anis'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.contactlist.find().pretty()
{
        "_id" : ObjectId("607f67442a05f058067b8abc"),
        "Last_name" : "Ben Lahmer",
        "First_name" : "Fares",
        "Email" : "fares@gmail.com",
        "age" : 26
}
{
        "_id" : ObjectId("607f67442a05f058067b8abd"),
        "Last_name" : "Kefi",
        "First_name" : "Anis",
        "Email" : "kefi@gmail.com",
        "age" : 15
}
{
        "_id" : ObjectId("607f67442a05f058067b8abe"),
        "Last_name" : "Fatnassi",
        "First_name" : "Sarra",
        "Email" : "sarra.f@gmail.com",
        "age" : 40
}
{
        "_id" : ObjectId("607f67442a05f058067b8abf"),
        "Last_name" : "Ben Yahia",
        "First_name" : "Rym",
        "age" : 4
}
{
        "_id" : ObjectId("607f67442a05f058067b8ac0"),
        "Last_name" : "Cherif",
        "First_name" : "Sami",
        "age" : 3
}
> db.contactlist.remove({age:{$lt: 5}})
WriteResult({ "nRemoved" : 2 })
> db.contactlist.find().pretty()
{
        "_id" : ObjectId("607f67442a05f058067b8abc"),
        "Last_name" : "Ben Lahmer",
        "First_name" : "Fares",
        "Email" : "fares@gmail.com",
        "age" : 26
}
{
        "_id" : ObjectId("607f67442a05f058067b8abd"),
        "Last_name" : "Kefi",
        "First_name" : "Anis",
        "Email" : "kefi@gmail.com",
        "age" : 15
}
{
        "_id" : ObjectId("607f67442a05f058067b8abe"),
        "Last_name" : "Fatnassi",
        "First_name" : "Sarra",
        "Email" : "sarra.f@gmail.com",
        "age" : 40
}
>
