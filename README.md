# Mongo DB

<!-- ``` bash
mongoimport --type csv -d test -c titanic --headerline --drop titanic.csv
db.titanic.find()
db.titanic.find({"Survived": 1})
db.titanic.find({"Parents/Children Aboard": {$ne: 0}})
db.titanic.find({"Pclass": {$lte: 2}}).sort({"Fare": 1})
db.titanic.createIndex({"Name": 1}, {unique: true}, { name: 'names' })
db.titanic.dropIndex("Name")
``` -->

Для начала надо завести mongodb. для этого напишем небольшой docker-compose файл:
``` docker
version: "3.8"
services:
  mongodb:
    image: mongo
    container_name: mongodb
    
    environment:
      - PUID=1000
      - PGID=1000
    
    volumes:
      - ./database:/data/db
    
    ports:
      - 27017:27017
```

И запустим его: `docker compose up`  

Теперь воспользуемся утилитой `mongoimport`, с помощью которой загрузим данные в нашу базу test, в коллекцию titanic:
``` bash
mongoimport --type csv -d test -c titanic --headerline --drop titanic.csv
```

Проверим, что наши данные успешно загрузилились:
```
db.titanic.find()
```

Вывод:
``` 
{ "_id" : ObjectId("6227da34a4b86f206a17f5b1"), "Survived" : 0, "Pclass" : 3, "Name" : "Mr. Owen Harris Braund", "Sex" : "male", "Age" : 22, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 7.25 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b2"), "Survived" : 1, "Pclass" : 1, "Name" : "Mrs. John Bradley (Florence Briggs Thayer) Cumings", "Sex" : "female", "Age" : 38, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 71.2833 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b3"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Laina Heikkinen", "Sex" : "female", "Age" : 26, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.925 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b4"), "Survived" : 1, "Pclass" : 1, "Name" : "Mrs. Jacques Heath (Lily May Peel) Futrelle", "Sex" : "female", "Age" : 35, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 53.1 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b5"), "Survived" : 0, "Pclass" : 3, "Name" : "Mr. William Henry Allen", "Sex" : "male", "Age" : 35, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 8.05 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b6"), "Survived" : 0, "Pclass" : 3, "Name" : "Mr. James Moran", "Sex" : "male", "Age" : 27, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 8.4583 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b7"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Timothy J McCarthy", "Sex" : "male", "Age" : 54, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 51.8625 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b8"), "Survived" : 0, "Pclass" : 3, "Name" : "Master. Gosta Leonard Palsson", "Sex" : "male", "Age" : 2, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 1, "Fare" : 21.075 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b9"), "Survived" : 1, "Pclass" : 3, "Name" : "Mrs. Oscar W (Elisabeth Vilhelmina Berg) Johnson", "Sex" : "female", "Age" : 27, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 2, "Fare" : 11.1333 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ba"), "Survived" : 1, "Pclass" : 2, "Name" : "Mrs. Nicholas (Adele Achem) Nasser", "Sex" : "female", "Age" : 14, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 30.0708 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5bb"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Marguerite Rut Sandstrom", "Sex" : "female", "Age" : 4, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 1, "Fare" : 16.7 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5bc"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Elizabeth Bonnell", "Sex" : "female", "Age" : 58, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 26.55 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5bd"), "Survived" : 0, "Pclass" : 3, "Name" : "Mr. William Henry Saundercock", "Sex" : "male", "Age" : 20, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 8.05 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5be"), "Survived" : 0, "Pclass" : 3, "Name" : "Mr. Anders Johan Andersson", "Sex" : "male", "Age" : 39, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 5, "Fare" : 31.275 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5bf"), "Survived" : 0, "Pclass" : 3, "Name" : "Miss. Hulda Amanda Adolfina Vestrom", "Sex" : "female", "Age" : 14, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.8542 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c0"), "Survived" : 1, "Pclass" : 2, "Name" : "Mrs. (Mary D Kingcome) Hewlett", "Sex" : "female", "Age" : 55, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 16 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c1"), "Survived" : 0, "Pclass" : 3, "Name" : "Master. Eugene Rice", "Sex" : "male", "Age" : 2, "Siblings/Spouses Aboard" : 4, "Parents/Children Aboard" : 1, "Fare" : 29.125 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c2"), "Survived" : 1, "Pclass" : 2, "Name" : "Mr. Charles Eugene Williams", "Sex" : "male", "Age" : 23, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 13 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c3"), "Survived" : 0, "Pclass" : 3, "Name" : "Mrs. Julius (Emelia Maria Vandemoortele) Vander Planke", "Sex" : "female", "Age" : 31, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 18 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c4"), "Survived" : 1, "Pclass" : 3, "Name" : "Mrs. Fatima Masselmani", "Sex" : "female", "Age" : 22, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.225 }
Type "it" for more
```

Давайте найдем всех пассажиров, которые выжили, для этого воспользуемся командой `find`
```
db.titanic.find({"Survived": 1})
```
Вывод:
``` 
{ "_id" : ObjectId("6227da34a4b86f206a17f5b2"), "Survived" : 1, "Pclass" : 1, "Name" : "Mrs. John Bradley (Florence Briggs Thayer) Cumings", "Sex" : "female", "Age" : 38, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 71.2833 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b3"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Laina Heikkinen", "Sex" : "female", "Age" : 26, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.925 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b4"), "Survived" : 1, "Pclass" : 1, "Name" : "Mrs. Jacques Heath (Lily May Peel) Futrelle", "Sex" : "female", "Age" : 35, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 53.1 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b9"), "Survived" : 1, "Pclass" : 3, "Name" : "Mrs. Oscar W (Elisabeth Vilhelmina Berg) Johnson", "Sex" : "female", "Age" : 27, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 2, "Fare" : 11.1333 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ba"), "Survived" : 1, "Pclass" : 2, "Name" : "Mrs. Nicholas (Adele Achem) Nasser", "Sex" : "female", "Age" : 14, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 30.0708 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5bb"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Marguerite Rut Sandstrom", "Sex" : "female", "Age" : 4, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 1, "Fare" : 16.7 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5bc"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Elizabeth Bonnell", "Sex" : "female", "Age" : 58, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 26.55 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c0"), "Survived" : 1, "Pclass" : 2, "Name" : "Mrs. (Mary D Kingcome) Hewlett", "Sex" : "female", "Age" : 55, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 16 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c2"), "Survived" : 1, "Pclass" : 2, "Name" : "Mr. Charles Eugene Williams", "Sex" : "male", "Age" : 23, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 13 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c4"), "Survived" : 1, "Pclass" : 3, "Name" : "Mrs. Fatima Masselmani", "Sex" : "female", "Age" : 22, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.225 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c6"), "Survived" : 1, "Pclass" : 2, "Name" : "Mr. Lawrence Beesley", "Sex" : "male", "Age" : 34, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 13 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c7"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Anna McGowan", "Sex" : "female", "Age" : 15, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 8.0292 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c8"), "Survived" : 1, "Pclass" : 1, "Name" : "Mr. William Thompson Sloper", "Sex" : "male", "Age" : 28, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 35.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ca"), "Survived" : 1, "Pclass" : 3, "Name" : "Mrs. Carl Oscar (Selma Augusta Emilia Johansson) Asplund", "Sex" : "female", "Age" : 38, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 5, "Fare" : 31.3875 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5cc"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Ellen O'Dwyer", "Sex" : "female", "Age" : 24, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.8792 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5d0"), "Survived" : 1, "Pclass" : 3, "Name" : "Mr. Hanna Mamee", "Sex" : "male", "Age" : 18, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.2292 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5d1"), "Survived" : 1, "Pclass" : 1, "Name" : "Mrs. William Augustus (Marie Eugenie) Spencer", "Sex" : "female", "Age" : 48, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 146.5208 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5d4"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Jamila Nicola-Yarred", "Sex" : "female", "Age" : 14, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 11.2417 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5d7"), "Survived" : 1, "Pclass" : 2, "Name" : "Miss. Simonne Marie Anne Andree Laroche", "Sex" : "female", "Age" : 3, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 2, "Fare" : 41.5792 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5da"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Mary Agatha Glynn", "Sex" : "female", "Age" : 18, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 7.75 }
Type "it" for more
```

Далее сделаем поиск с условием и выведем пассажиров, у которых не было родственников на борту:
```
db.titanic.find({"Parents/Children Aboard": {$ne: 0}})
```
Вывод:
``` 
{ "_id" : ObjectId("6227da34a4b86f206a17f5b8"), "Survived" : 0, "Pclass" : 3, "Name" : "Master. Gosta Leonard Palsson", "Sex" : "male", "Age" : 2, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 1, "Fare" : 21.075 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5b9"), "Survived" : 1, "Pclass" : 3, "Name" : "Mrs. Oscar W (Elisabeth Vilhelmina Berg) Johnson", "Sex" : "female", "Age" : 27, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 2, "Fare" : 11.1333 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5bb"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Marguerite Rut Sandstrom", "Sex" : "female", "Age" : 4, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 1, "Fare" : 16.7 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5be"), "Survived" : 0, "Pclass" : 3, "Name" : "Mr. Anders Johan Andersson", "Sex" : "male", "Age" : 39, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 5, "Fare" : 31.275 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c1"), "Survived" : 0, "Pclass" : 3, "Name" : "Master. Eugene Rice", "Sex" : "male", "Age" : 2, "Siblings/Spouses Aboard" : 4, "Parents/Children Aboard" : 1, "Fare" : 29.125 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5c9"), "Survived" : 0, "Pclass" : 3, "Name" : "Miss. Torborg Danira Palsson", "Sex" : "female", "Age" : 8, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 1, "Fare" : 21.075 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ca"), "Survived" : 1, "Pclass" : 3, "Name" : "Mrs. Carl Oscar (Selma Augusta Emilia Johansson) Asplund", "Sex" : "female", "Age" : 38, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 5, "Fare" : 31.3875 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ce"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Charles Alexander Fortune", "Sex" : "male", "Age" : 19, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 2, "Fare" : 263 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5d7"), "Survived" : 1, "Pclass" : 2, "Name" : "Miss. Simonne Marie Anne Andree Laroche", "Sex" : "female", "Age" : 3, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 2, "Fare" : 41.5792 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5dd"), "Survived" : 0, "Pclass" : 3, "Name" : "Master. Juha Niilo Panula", "Sex" : "male", "Age" : 7, "Siblings/Spouses Aboard" : 4, "Parents/Children Aboard" : 1, "Fare" : 39.6875 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5e2"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Engelhart Cornelius Ostby", "Sex" : "male", "Age" : 65, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 1, "Fare" : 61.9792 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5e6"), "Survived" : 1, "Pclass" : 2, "Name" : "Miss. Constance Mirium West", "Sex" : "female", "Age" : 5, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 2, "Fare" : 27.75 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5e8"), "Survived" : 0, "Pclass" : 3, "Name" : "Master. William Frederick Goodwin", "Sex" : "male", "Age" : 11, "Siblings/Spouses Aboard" : 5, "Parents/Children Aboard" : 2, "Fare" : 46.9 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ed"), "Survived" : 1, "Pclass" : 3, "Name" : "Master. Gerios Moubarek", "Sex" : "male", "Age" : 7, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 1, "Fare" : 15.2458 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ef"), "Survived" : 1, "Pclass" : 3, "Name" : "Miss. Erna Alexandra Andersson", "Sex" : "female", "Age" : 17, "Siblings/Spouses Aboard" : 4, "Parents/Children Aboard" : 2, "Fare" : 7.925 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5f2"), "Survived" : 0, "Pclass" : 3, "Name" : "Miss. Lillian Amy Goodwin", "Sex" : "female", "Age" : 16, "Siblings/Spouses Aboard" : 5, "Parents/Children Aboard" : 2, "Fare" : 46.9 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5f5"), "Survived" : 0, "Pclass" : 3, "Name" : "Master. Harald Skoog", "Sex" : "male", "Age" : 4, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 2, "Fare" : 27.9 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5f9"), "Survived" : 1, "Pclass" : 2, "Name" : "Master. Alden Gates Caldwell", "Sex" : "male", "Age" : 0.83, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 2, "Fare" : 29 }
{ "_id" : ObjectId("6227da34a4b86f206a17f603"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Mabel Helen Fortune", "Sex" : "female", "Age" : 23, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 2, "Fare" : 263 }
{ "_id" : ObjectId("6227da34a4b86f206a17f60b"), "Survived" : 0, "Pclass" : 3, "Name" : "Mr. Bertram Frank Dean", "Sex" : "male", "Age" : 26, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 2, "Fare" : 20.575 }
Type "it" for more
```

Если мы хотим пассажиров круче 3 класса и в порядке возрастания стоимости их билетов, то нам понадобиться `sort()`:
```
db.titanic.find({"Pclass": {$lte: 2}}).sort({"Fare": 1})
```
Вывод:
``` 
{ "_id" : ObjectId("6227da34a4b86f206a17f6b1"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. William Harrison", "Sex" : "male", "Age" : 40, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f6bf"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Francis Parkes", "Sex" : "male", "Age" : 21, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f754"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Alfred Fleming Cunningham", "Sex" : "male", "Age" : 22, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f78a"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. William Campbell", "Sex" : "male", "Age" : 21, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f78b"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Anthony Wood Frost", "Sex" : "male", "Age" : 37, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f822"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. William Henry Marsh Parr", "Sex" : "male", "Age" : 30, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f861"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Ennis Hastings Watson", "Sex" : "male", "Age" : 19, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f888"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Robert J Knight", "Sex" : "male", "Age" : 41, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f8d2"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Thomas Jr Andrews", "Sex" : "male", "Age" : 39, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f8db"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Richard Fry", "Sex" : "male", "Age" : 39, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f8e2"), "Survived" : 0, "Pclass" : 1, "Name" : "Jonkheer. John George Reuchlin", "Sex" : "male", "Age" : 38, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 0 }
{ "_id" : ObjectId("6227da34a4b86f206a17f923"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Frans Olof Carlsson", "Sex" : "male", "Age" : 33, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5e1"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Edward H Wheadon", "Sex" : "male", "Age" : 66, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5e4"), "Survived" : 1, "Pclass" : 2, "Name" : "Miss. Emily Rugg", "Sex" : "female", "Age" : 21, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5f1"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Stephen Curnow Jenkin", "Sex" : "male", "Age" : 32, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5fe"), "Survived" : 1, "Pclass" : 2, "Name" : "Mrs. (Elizabeth Ramell) Nye", "Sex" : "female", "Age" : 29, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f609"), "Survived" : 1, "Pclass" : 2, "Name" : "Miss. Bertha Ilett", "Sex" : "female", "Age" : 17, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f687"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Walter Harris", "Sex" : "male", "Age" : 30, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f692"), "Survived" : 1, "Pclass" : 2, "Name" : "Mr. William John Mellors", "Sex" : "male", "Age" : 19, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f69a"), "Survived" : 0, "Pclass" : 2, "Name" : "Mr. Robert William Norman Leyson", "Sex" : "male", "Age" : 24, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 10.5 }
Type "it" for more
```

Обновим данные для пассажира Mr. Charles Eugene Williams  
До апдейта:
``` 
{ "_id" : ObjectId("6227da34a4b86f206a17f5c2"), "Survived" : 1, "Pclass" : 2, "Name" : "Mr. Charles Eugene Williams", "Sex" : "male", "Age" : 23, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 13 }
```
Апдейт:
```
db.titanic.updateOne({"Name": "Mr. Charles Eugene Williams"}, {$set: {"Fare": 130}})
```
После апдейта сделаем:
```
db.titanic.find({"Name": "Mr. Charles Eugene Williams"})
```
Вывод:
``` 
{ "_id" : ObjectId("6227da34a4b86f206a17f5c2"), "Survived" : 1, "Pclass" : 2, "Name" : "Mr. Charles Eugene Williams", "Sex" : "male", "Age" : 23, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 130 }
```

Добавим нового человека на борт (который заплатил очень много):
``` 
db.titanic.insert({"Survived": 1, "Name": "Aleksej Volkov", "Fare": 1000000000})
```
Выведем всех, отсортировав по плате за билеты:
```
db.titanic.find().sort({"Fare": -1})
```
Вывод:
``` 
{ "_id" : ObjectId("6229303aa540a37171a8b9dd"), "Survived" : 1, "Name" : "Aleksej Volkov", "Fare" : 1000000000 }
{ "_id" : ObjectId("6227da34a4b86f206a17f6b6"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Anna Ward", "Sex" : "female", "Age" : 35, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 512.3292 }
{ "_id" : ObjectId("6227da34a4b86f206a17f85b"), "Survived" : 1, "Pclass" : 1, "Name" : "Mr. Thomas Drake Martinez Cardeza", "Sex" : "male", "Age" : 36, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 1, "Fare" : 512.3292 }
{ "_id" : ObjectId("6227da34a4b86f206a17f88c"), "Survived" : 1, "Pclass" : 1, "Name" : "Mr. Gustave J Lesurer", "Sex" : "male", "Age" : 35, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 512.3292 }
{ "_id" : ObjectId("6227da34a4b86f206a17f5ce"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Charles Alexander Fortune", "Sex" : "male", "Age" : 19, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 2, "Fare" : 263 }
{ "_id" : ObjectId("6227da34a4b86f206a17f603"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Mabel Helen Fortune", "Sex" : "female", "Age" : 23, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 2, "Fare" : 263 }
{ "_id" : ObjectId("6227da34a4b86f206a17f716"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Alice Elizabeth Fortune", "Sex" : "female", "Age" : 24, "Siblings/Spouses Aboard" : 3, "Parents/Children Aboard" : 2, "Fare" : 263 }
{ "_id" : ObjectId("6227da34a4b86f206a17f766"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Mark Fortune", "Sex" : "male", "Age" : 64, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 4, "Fare" : 263 }
{ "_id" : ObjectId("6227da34a4b86f206a17f6e8"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Emily Borie Ryerson", "Sex" : "female", "Age" : 18, "Siblings/Spouses Aboard" : 2, "Parents/Children Aboard" : 2, "Fare" : 262.375 }
{ "_id" : ObjectId("6227da34a4b86f206a17f892"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Susan Parker Ryerson", "Sex" : "female", "Age" : 21, "Siblings/Spouses Aboard" : 2, "Parents/Children Aboard" : 2, "Fare" : 262.375 }
{ "_id" : ObjectId("6227da34a4b86f206a17f622"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Quigg Edmond Baxter", "Sex" : "male", "Age" : 24, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 1, "Fare" : 247.5208 }
{ "_id" : ObjectId("6227da34a4b86f206a17f6d5"), "Survived" : 1, "Pclass" : 1, "Name" : "Mrs. James (Helene DeLaudeniere Chaput) Baxter", "Sex" : "female", "Age" : 50, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 1, "Fare" : 247.5208 }
{ "_id" : ObjectId("6227da34a4b86f206a17f72b"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Rosalie Bidois", "Sex" : "female", "Age" : 42, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 227.525 }
{ "_id" : ObjectId("6227da34a4b86f206a17f7db"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Victor Robbins", "Sex" : "male", "Age" : 45, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 227.525 }
{ "_id" : ObjectId("6227da34a4b86f206a17f86a"), "Survived" : 1, "Pclass" : 1, "Name" : "Mrs. John Jacob (Madeleine Talmadge Force) Astor", "Sex" : "female", "Age" : 18, "Siblings/Spouses Aboard" : 1, "Parents/Children Aboard" : 0, "Fare" : 227.525 }
{ "_id" : ObjectId("6227da34a4b86f206a17f875"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Caroline Louise Endres", "Sex" : "female", "Age" : 38, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 227.525 }
{ "_id" : ObjectId("6227da34a4b86f206a17f7b8"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. John Farthing", "Sex" : "male", "Age" : 49, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 221.7792 }
{ "_id" : ObjectId("6227da34a4b86f206a17f728"), "Survived" : 0, "Pclass" : 1, "Name" : "Mr. Harry Elkins Widener", "Sex" : "male", "Age" : 27, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 2, "Fare" : 211.5 }
{ "_id" : ObjectId("6227da34a4b86f206a17f85a"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Georgette Alexandra Madill", "Sex" : "female", "Age" : 15, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 1, "Fare" : 211.3375 }
{ "_id" : ObjectId("6227da34a4b86f206a17f886"), "Survived" : 1, "Pclass" : 1, "Name" : "Miss. Elisabeth Walton Allen", "Sex" : "female", "Age" : 29, "Siblings/Spouses Aboard" : 0, "Parents/Children Aboard" : 0, "Fare" : 211.3375 }
Type "it" for more
```

Посмотрим сколько записей нужно отсмотреть что бы найти Mrs. James (Helene DeLaudeniere Chaput) Baxter:
```
db.titanic.find({"Name": "Mrs. James (Helene DeLaudeniere Chaput) Baxter"}).explain("executionStats")
``` 
Вывод:
``` json
{
	"explainVersion" : "1",
	"queryPlanner" : {
		"namespace" : "test.titanic",
		"indexFilterSet" : false,
		"parsedQuery" : {
			"Name" : {
				"$eq" : "Mrs. James (Helene DeLaudeniere Chaput) Baxter"
			}
		},
		"maxIndexedOrSolutionsReached" : false,
		"maxIndexedAndSolutionsReached" : false,
		"maxScansToExplodeReached" : false,
		"winningPlan" : {
			"stage" : "COLLSCAN",
			"filter" : {
				"Name" : {
					"$eq" : "Mrs. James (Helene DeLaudeniere Chaput) Baxter"
				}
			},
			"direction" : "forward"
		},
		"rejectedPlans" : [ ]
	},
	"executionStats" : {
		"executionSuccess" : true,
		"nReturned" : 1,
		"executionTimeMillis" : 0,
		"totalKeysExamined" : 0,
		"totalDocsExamined" : 888,
		"executionStages" : {
			"stage" : "COLLSCAN",
			"filter" : {
				"Name" : {
					"$eq" : "Mrs. James (Helene DeLaudeniere Chaput) Baxter"
				}
			},
			"nReturned" : 1,
			"executionTimeMillisEstimate" : 0,
			"works" : 890,
			"advanced" : 1,
			"needTime" : 888,
			"needYield" : 0,
			"saveState" : 0,
			"restoreState" : 0,
			"isEOF" : 1,
			"direction" : "forward",
			"docsExamined" : 888
		}
	},
	"command" : {
		"find" : "titanic",
		"filter" : {
			"Name" : "Mrs. James (Helene DeLaudeniere Chaput) Baxter"
		},
		"$db" : "test"
	},
	"serverInfo" : {
		"host" : "1d66400e5374",
		"port" : 27017,
		"version" : "5.0.6",
		"gitVersion" : "212a8dbb47f07427dae194a9c75baec1d81d9259"
	},
	"serverParameters" : {
		"internalQueryFacetBufferSizeBytes" : 104857600,
		"internalQueryFacetMaxOutputDocSizeBytes" : 104857600,
		"internalLookupStageIntermediateDocumentMaxSizeBytes" : 104857600,
		"internalDocumentSourceGroupMaxMemoryBytes" : 104857600,
		"internalQueryMaxBlockingSortMemoryUsageBytes" : 104857600,
		"internalQueryProhibitBlockingMergeOnMongoS" : 0,
		"internalQueryMaxAddToSetBytes" : 104857600,
		"internalDocumentSourceSetWindowFieldsMaxMemoryBytes" : 104857600
	},
	"ok" : 1
}
```

Получаем `"totalDocsExamined" : 888`. то есть 888 записей. Теперь добавим индекс:
```
db.titanic.createIndex({"Name": 1})
```

И сделаем тот же запрос, вывод:
``` json
{
	"explainVersion" : "1",
	"queryPlanner" : {
		"namespace" : "test.titanic",
		"indexFilterSet" : false,
		"parsedQuery" : {
			"Name" : {
				"$eq" : "Mrs. James (Helene DeLaudeniere Chaput) Baxter"
			}
		},
		"maxIndexedOrSolutionsReached" : false,
		"maxIndexedAndSolutionsReached" : false,
		"maxScansToExplodeReached" : false,
		"winningPlan" : {
			"stage" : "FETCH",
			"inputStage" : {
				"stage" : "IXSCAN",
				"keyPattern" : {
					"Name" : 1
				},
				"indexName" : "Name_1",
				"isMultiKey" : false,
				"multiKeyPaths" : {
					"Name" : [ ]
				},
				"isUnique" : false,
				"isSparse" : false,
				"isPartial" : false,
				"indexVersion" : 2,
				"direction" : "forward",
				"indexBounds" : {
					"Name" : [
						"[\"Mrs. James (Helene DeLaudeniere Chaput) Baxter\", \"Mrs. James (Helene DeLaudeniere Chaput) Baxter\"]"
					]
				}
			}
		},
		"rejectedPlans" : [ ]
	},
	"executionStats" : {
		"executionSuccess" : true,
		"nReturned" : 1,
		"executionTimeMillis" : 0,
		"totalKeysExamined" : 1,
		"totalDocsExamined" : 1,
		"executionStages" : {
			"stage" : "FETCH",
			"nReturned" : 1,
			"executionTimeMillisEstimate" : 0,
			"works" : 2,
			"advanced" : 1,
			"needTime" : 0,
			"needYield" : 0,
			"saveState" : 0,
			"restoreState" : 0,
			"isEOF" : 1,
			"docsExamined" : 1,
			"alreadyHasObj" : 0,
			"inputStage" : {
				"stage" : "IXSCAN",
				"nReturned" : 1,
				"executionTimeMillisEstimate" : 0,
				"works" : 2,
				"advanced" : 1,
				"needTime" : 0,
				"needYield" : 0,
				"saveState" : 0,
				"restoreState" : 0,
				"isEOF" : 1,
				"keyPattern" : {
					"Name" : 1
				},
				"indexName" : "Name_1",
				"isMultiKey" : false,
				"multiKeyPaths" : {
					"Name" : [ ]
				},
				"isUnique" : false,
				"isSparse" : false,
				"isPartial" : false,
				"indexVersion" : 2,
				"direction" : "forward",
				"indexBounds" : {
					"Name" : [
						"[\"Mrs. James (Helene DeLaudeniere Chaput) Baxter\", \"Mrs. James (Helene DeLaudeniere Chaput) Baxter\"]"
					]
				},
				"keysExamined" : 1,
				"seeks" : 1,
				"dupsTested" : 0,
				"dupsDropped" : 0
			}
		}
	},
	"command" : {
		"find" : "titanic",
		"filter" : {
			"Name" : "Mrs. James (Helene DeLaudeniere Chaput) Baxter"
		},
		"$db" : "test"
	},
	"serverInfo" : {
		"host" : "1d66400e5374",
		"port" : 27017,
		"version" : "5.0.6",
		"gitVersion" : "212a8dbb47f07427dae194a9c75baec1d81d9259"
	},
	"serverParameters" : {
		"internalQueryFacetBufferSizeBytes" : 104857600,
		"internalQueryFacetMaxOutputDocSizeBytes" : 104857600,
		"internalLookupStageIntermediateDocumentMaxSizeBytes" : 104857600,
		"internalDocumentSourceGroupMaxMemoryBytes" : 104857600,
		"internalQueryMaxBlockingSortMemoryUsageBytes" : 104857600,
		"internalQueryProhibitBlockingMergeOnMongoS" : 0,
		"internalQueryMaxAddToSetBytes" : 104857600,
		"internalDocumentSourceSetWindowFieldsMaxMemoryBytes" : 104857600
	},
	"ok" : 1
}
```
Получили `"totalDocsExamined": 1`, что очевидно намного меньше и быстрее
