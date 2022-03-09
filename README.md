# Mongo DB

``` bash
mongoimport --type csv -d test -c titanic --headerline --drop titanic.csv
db.titanic.find()
db.titanic.find({"Survived": 1})
db.titanic.find({"Parents/Children Aboard": {$ne: 0}})
db.titanic.createIndex({"Name": 1}, {unique: true}, { name: 'names' })
db.titanic.dropIndex("Name");
```