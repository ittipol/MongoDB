# MongoDB

## Using CLI
``` bash
mongosh -u root -p
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

### Basic query command
``` bash
# query all
db.users.find()

db.users.find().limit(2)

db.users.find().skip(1).limit(2)

# Search equal to given data
db.users.find({ name: "Test name" })

db.users.find({ age: 18 })

db.users.find({ 'address.city': 'New York City' })

# findOne()
db.users.findOne({ age: {$gt: 20} })

# Search and return only name, address fields
db.users.find({ name: 'New Name' }, { name: 1, address: 1 })

# no id return
db.users.find({ name: 'New Name' }, { name: 1, address: 1, _id: 0 })

# return all fields except "age" field
db.users.find({ name: 'New Name' }, { age: 0 })
```

### Complex query command
``` bash
# $eq = equal
db.users.find({ name: { $eq: 'New Name' } })

# $ne = not equal
db.users.find({ name: { $ne: 'New Name' } })

# $gt = greater than
db.users.find({ age: { $gt: 20 } })

# $gte
db.users.find({ age: { $gte: 20 } })

# $lt = less than
db.users.find({ age: { $lt: 22 } })

# $lte
db.users.find({ age: { $lte: 22 } })

# $in = in
db.users.find({ name: { $in: ['Test Name', 'New Name'] } })

# $nin = not in
db.users.find({ name: { $nin: ['Test Name', 'New Name'] } })

# $exists = true (return only the object that have an address)
db.users.find({ address: { $exists: true } })

# $exists = false
db.users.find({ address: { $exists: false } })

# $not
db.users.find({ age: { $not: { $lt: 20 } }  })
```

### Combine query
``` bash
# combine query
db.users.find({ age: { $gte: 18, $lte: 40 }  })

db.users.find({ name: 'New Name', age: { $gte: 18, $lte: 40 } })

# $and
db.users.find({ $and: [{ name: 'New Name' }, { age: 20 }] })

# $or
db.users.find({ $or: [{ name: 'New Name' }, { age: { $gte: 20, $lte: 40} }] })
```

### Expression
``` bash
# db.users.insertOne({name: 'ABCD', age: 22, balance: 20000, debt: 30000})
# db.users.insertOne({name: 'XYZ', age: 35, balance: 400000, debt: 80000})

# $expr
db.users.find({ $expr: { $gt: ['$balance', '$debt'] } })
```

### Count document
``` bash
db.users.countDocuments({ age: { $gt: 18 } })
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

### Insert command
``` bash
# insert document (users = collection)
db.users.insertOne({name: "Test name"})
# result
# {
#   acknowledged: true,
#   insertedId: ObjectId("6455d6c4a3f26ada5daa707f")
# }

db.users.insertOne({ name: 'New Name', age: 20, hobbies: ['Running', 'playing video game'], address: { street: '123', city: 'New York City' } })

# insert many documents
db.users.insertMany([{name: "Name 1", age: 22}, {name: "Name 2", age: 18}])
```

### Update command
``` bash
# updateOne()
db.users.updateOne({ age: { $gt: 22 } }, { $set: { age: 30 } })
# result
# {
#   acknowledged: true,
#   insertedId: null,
#   matchedCount: 1,
#   modifiedCount: 1,
#   upsertedCount: 0
# }

# updateMany()
db.users.updateMany({ age: { $gt: 22 } }, { $set: { age: 55 } })
# result
# {
#   acknowledged: true,
#   insertedId: null,
#   matchedCount: 2,
#   modifiedCount: 2,
#   upsertedCount: 0
# }

# update by id
db.users.updateOne({_id: ObjectId("6455f6621c0ddaa079c9be2e")}, {$set: { age: 60 }})
```

### Increment value
``` bash
# $inc
db.users.updateOne({ _id: ObjectId("6455f6621c0ddaa079c9be2e") }, { $inc: { age: 1 }  })
```

### Rename property
``` bash
db.users.updateOne({ _id: ObjectId("6455f6621c0ddaa079c9be2e") }, { $rename: { name: 'firstName' }  })
```

### Unset property
``` bash
db.users.updateOne({ _id: ObjectId("6455f6621c0ddaa079c9be2e") }, { $unset: { address: '' }  })

db.users.updateMany({ hobbies: { $exists: true } }, { $unset: { hobbies: '' } })
```

### Add, Remove item from array
``` bash
$push
db.users.updateOne({ _id: ObjectId("6455f6621c0ddaa079c9be2e") }, { $push: { hobbies: 'gardening' }  })

$pull
db.users.updateOne({ _id: ObjectId("6455f6621c0ddaa079c9be2e") }, { $pull: { hobbies: 'gardening' }  })
```

### Replace command
``` bash
# replace entire object with giver value

# replaceOne()
db.users.replaceOne({ name: 'ABCD' }, { name: 'Summer'})

# Before replace
# {
#     _id: ObjectId("645602771c0ddaa079c9be2f"),
#     name: 'ABCD',
#     age: 22,
#     balance: 50000,
#     debt: 20000
# }

# After replace
# { _id: ObjectId("645602771c0ddaa079c9be2f"), name: 'Summer' }
```

### Delete command
``` bash
# deleteOne()
db.users.deleteOne({ name: 'Summer' })
# result
# { acknowledged: true, deletedCount: 1 }

# deleteMany()
db.users.deleteMany({ age: { $gt: 30 }})
# result
# { acknowledged: true, deletedCount: 3 }

```