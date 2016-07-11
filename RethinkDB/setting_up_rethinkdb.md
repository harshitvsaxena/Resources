<a id="top"></a>

# RethinkDB

[Main Page](README.md)

## Setting up RethinkDB

Starting a rethinkdb server:

```sh
$ rethinkdb
```

Now to view the console of rethinkDB, go to: http://localhost:8080

Follow following commands for setting up rethinkDB for the timeline code:

1. Go to: http://localhost:8080
2. Find `Tables` on the top panel. Click it.
3. Click on the `Add Database` Button on this page.
4. Write the name as `SampleDatabase`.
5. Now on the same page inside `SampleDatabase` panel click on `Add Table`.
6. Enter the name of table as `sampleTable`.

### To view the data in table

1. Find "Data Explorer" on the top panel. Click it.
2. Copy and paste the below code into Data Explorer Input Box and hit enter.

```javascript
r.db("SampleDatabase").table("sampleTable");
```

---

References:
1. https://www.rethinkdb.com/docs/install-drivers/javascript/
2. https://www.rethinkdb.com/docs/start-a-server/

[Main Page](README.md) | [Top](#top)

---

## The End
