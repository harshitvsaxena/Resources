<a id="top"></a>

# NodeJS

[Main Page](README.md)

## NodeJS and MySQL

To communicate node.js with MySQL server we need to install mysql module. For this, switch to the directory where you are saving the node modules using `cd`, now:

```sh
$ npm install mysql --save
```

Now in your `server.js` file that is the server file write this:

```javascript
var mysql = require("mysql");

// First you need to create a connection to the db
var con = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "password",
  database: "database_name"
});

con.connect(function(err){
  if(err){
    console.log('Error connecting to Db');
    return;
  }
  console.log('Connection established');
});

con.query('SELECT * FROM customers',function(err,rows){
  if(err) throw err;
  console.log('Data received from Db:\n');
  console.log(rows);
});

con.end(function(err) {
  // The connection is terminated gracefully
  // Ensures all previously enqueued queries are still
  // before sending a COM_QUIT packet to the MySQL server.
});
```


---

Resource: https://www.sitepoint.com/using-node-mysql-javascript-client/

[Main Page](README.md) | [Top](#top)

---

## Thank You
