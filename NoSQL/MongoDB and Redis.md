
# [NoSQL数据库-MongoDB和Redis](http://www.uml.org.cn/sjjm/201212205.asp)


##Keys:
>MongoDB,Javascript,Mongo Shell,Redis,Redis-cli,

## Term compare:
>Mongo Shell
  
    $ mongoimport -d mydb -c things --type csv --file      
    locations.csv --headerline
    connected to: 127.0.0.1
    imported 3 objects
    $ mongo
    MongoDB shell version: 1.7.3
    connecting to: test
    > use mydb
    switched to db mydb
    > db.things.find()
    { "_id" : ObjectId("4d32a36ed63d057130c08fca"),  "Name" : "Jane Doe", "Address" : "123 Main St", "City"  : "Whereverville", "State" : "CA", "ZIP" : 90210 }
    { "_id" : ObjectId("4d32a36ed63d057130c08fcb"), "Name" : "John Doe", "Address" : "555 Broadway Ave", "City" : "New York", "State" : "NY", "ZIP" : 10010 }
> redis shell
   
    $ redis-cli
    >select 1
    ok
    >keys *
    all keys shown in db1
    >get <key shon above>
    return value for the key