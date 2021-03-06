# NodeDB - Android based NoSQL Database

[![](https://jitpack.io/v/rexllc/node-db.svg)](https://jitpack.io/#rexllc/node-db)

A NoSQL Android Database system that aims to be a fast, and lightweight SQL library for Android.

## NodeDB Android
Add NodeDB dependency into your build.gradle

```
dependencies {

	     implementation 'com.github.rexllc:node-db:1.0.6-beta'

	}
```
## Initialize NodeApp
You need to initialize the system before performing any queries, or adding data to your database.
```
NodeApp.initialize(this);
```
## Initialize Database
To start adding data, you need to specify your database path.
```
NodeDB db = NodeDB.getInstance().getDatabase("name");
```
## Create Multiple Table
You can create or add multiple table to your database.
```
db.create().table("users").isDesc(true).build();
```

## Adding data to the database
```
HashMap<String, Object> map = new HashMap<>();
map.put("uid", uid);
map.put("name", "John");
map.put("surname", "Doe");
map.put("age", "20");
db.put(map).prepare().insert();
```

Or alternatively, you can use default NodeDB method

```
db.put("uid", uid);
db.put("name", "John");
db.put("surname", "Doe");
db.put("age", "20");
db.prepare().insert();
```

## Adding data to the specific table

```
db.put(object).table("others").prepare().insert();
```

## Add the listener
Listen for any changes on your database by using `QueryEventListener`
```
db.addQueryEventListener(eventListener);

/*You can also use ValueEventListener to retrieve specific value such user details.*/

db.addValueEventListener(eventListener);

QueryEventListener eventListener;
eventListener = new QueryEventListener() {
     @Override
     public void onQuery(Query query) {
       //For getting single value
       Map<String, Object> map = (Map) query.getData();
       //For getting all list.
       String  list = query.getQuery().toString();
     }
     
     @Override
     public void onError(QueryError error) {}
};
```
## Get single value from the database
To get value from the database with the specific key.
Use `db.child(id).get().addValueEventListener(eventListener);`
it will retrieve all associates records to that id.
Like
```
{
  "key" : "value",
  ...
}
```
## Or get specific value from other table
```
db.child(id).table("users").get();
```
## Delete data from the database
You can also remove a specific data in the table.
```
db.child(id).remove();
```
## Updating data
```
NodeObject nodeObject = new NodeObject();
nodeObject.put("key", "value");
nodeObject.put("key", "value");
nodeObject.put("key", "value");
db.child(id).update(nodeObject).insert();
```
## Delete your database
NodeDB have special method that when you call it will delete your current database instantly.
```
db.delete();
```
Deleting your database isn't recoverable. So, do at your own risk.
