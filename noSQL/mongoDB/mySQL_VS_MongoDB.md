# 문법의 차이를 이해하기 위해 간단하게 작성함 
| MySQL | MongoDB |
| --- | --- |
| database | database |
| table | collection |
| index | index |
| row | BSON document |
| column | BSON field |
| join | embedding and linking |

| SQL | Mongo SQL |
| --- | --- |
| CREATE TABLE users(a int, b int) | db.createCollection(mycollection) |
| INSERT INTO users VALUES(3,5) | db.users.insert({a:3, b:5}) |
| SELECT a,b FROM users | db.users.find({},{a:1,  b:1}) |
| SELECT * FROM users | db.users.find() |
| SELECT * FROM users WHERE age=33 | db.users.find({age:33}) |
| SELECT a,b FROM users WHERE age=33 | db.users.find({age:33}, {a:1, b:1}) |
| SELECT * FROM users WHERE age=33 ORDER BY name | db.users.find({age:33}.sort({name:1})) |
| SELECT * FROM users WHERE age>33 | db.users.find({age:{$gt:33}}) |
| SELECT * FROM users WHERE age<33 | db.users.find({age:{$lt:33}}) |
| SELECT * FROM users WHERE name LIKE “%Joe%” | db.users.find({name:/Joe/}) |
| SELECT * FROM users WHERE name LIKE “Joe%” | db.users.find({name:/^Joe/}) |
| SELECT * FROM users WHERE age>33 AND age≤40 | db.users.find({age:{&gt:33,$lt:40}}) |
| SELECT * FROM users ORDER BY name DESC | db.users.find().sort({name:-1}) |
| SELECT * FROM users WHERE a=1 AND b=’q’ | db.users.find({a:1, b:’q’}) |
| SELECT * FROM users LIMIT 10 SKIP 20 | db.users.find().limit(10).skip(20) |
| SELECT * FROM users WHERE a=1 OR b=2 | db.users.find({$or:[{a:1},{b:1}]}) |
| SELECT * FROM users LIMIT 1 | db.users.findOne() |
| SELECT COUNT(*y) FROM users | db.users.count() |
| SELECT DISTINCT last_name FROM users | db.users.distinct(”last_name”) |
| SELECT COUNT(*y) FROM users WHERE age>30 | db.users.find({age:{$gt:30}}).count() |
| SELECT COUNT(age) FROM users | db.users.find({age:{$exists:true}}).count() |
| CREATE INDEX myindexname ON users(name) | db.users.ensureIndex({name:1}) <under v.2>
db.users.createIndex({name:1}) |
| CREATE INDEX myindexname ON users(name, ts DESC) | db.users.ensureIndex({name:1,ts:-1}) <under v.2>
db.users.createIndex({name:-1}) |
| EXPLAIN SELECT * FROM users WHERE z=3 | db.users.find({z:3}).explain() |
| UPDATE users SET a=1 WHERE b=”q” | db.users.update({b:”q”},{$set:{a:1}},false,true) |
| UPDATE users SET a=a+2 WHERE b=”q” | db.users.update({b:”q”},{$inc:{a:2}},false,true) |
| DELETE FROM users WHERE z=”abc” | db.users.remove(z:”abc”}) |
