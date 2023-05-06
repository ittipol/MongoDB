# MongoDB

## Using CLI
``` bash
mongosh - u root -p
```

### Database
``` bash
# list of databases,
show dbs

# check current Database
db

# create database or swiich to existing database
use Database_Name

# drop database
db.dropDatabase()
```

### Collection (collection are like table)
``` bash
# list of collections
show collections
```

### Insert document
``` bash
# insert document (users = collection)
db.users.insertOne({name: "Test name"})
# result
# {
#   acknowledged: true,
#   insertedId: ObjectId("6455d6c4a3f26ada5daa707f")
# }

# insert many documents
db.users.insertMany([{name: "Name 1", age: 22}, {name: "Name 2", age: 18}])
```

### Query Document
``` bash
# query all
db.users.find()

db.users.find().limit(2)

db.users.find().skip(1).limit(2)

# Search equal to given data
db.users.find({ name: "Test name"})

db.users.find({ age: 18})
```

### Sorting document
``` bash
# order by desc
db.users.find().sort({ name: 1})

# order by asc
db.users.find().sort({ name: -1})

# order multiple fields
db.users.find().sort({ age: -1, name: 1})
```