# Unit 3 Highlights

## Videos
[YouTube - Playlist](https://www.youtube.com/watch?v=-_PSo13jZKY&list=PLvQtbvxnE8UF6gJ0uXawC2cEby557FIon)

## Code
[github.com/Pursuit-Core-6-2/Lessons-Code/unit_3](https://github.com/Pursuit-Core-6-2/Lessons-Code/tree/master/unit_3)

## Postgres & Express.js

* `pg-promise`. NPM package/library/module. PostgreSQL Interface for Node.js. Bridge between `js` and `sql` worlds.
* Install `pg-promise`: `npm install pg-promise`
* `pg-promise` setup and usage:
  ```js
  const express = require('express');
  const router = express.Router();

  // pg-promise setup
  const pgp = require('pg-promise')(); // Import pg-promise
  const connectionString = "postgres://localhost:5432/facebook_db" // URL where Postgres is running
  const db = pgp(connectionString) // Connected db instance

  router.get('/', async (req, res) => {
    try {
      let users = await db.any("SELECT * FROM users")

      res.json({
        payload: users,
        message: "Success. Retrieved all the users"
      });

    } catch (error) {
      res.status(500)
      res.json({
        message: "Error. Something went wrong!"
      })
      console.log(error)
    }
  })
  ```
  Example: [`db.any - server/routes/users.js`](https://github.com/Pursuit-Core-6-2/Lessons-Code/blob/cd1c4f2f3e2f719bcf9c19177e3db489abdc94fe/unit_3/postgres-and-pg-promise/server/routes/usersRouter.js#L10)

* `pg-promise` insert & passing query formatting parameters
  ```js
    db.none("INSERT INTO users(firstname, lastname, age) VALUES($1, $2, $3)", ["Alejo", "Franco", "24"])
  ```
  Example: [`db.none - server/routes/users.js`](https://github.com/Pursuit-Core-6-2/Lessons-Code/blob/cd1c4f2f3e2f719bcf9c19177e3db489abdc94fe/unit_3/postgres-and-pg-promise/server/routes/usersRouter.js#L50)

* `db.one()`. Expect the query to return 1 and only 1 row. Fail if got 0 or more rows.
* `db.any()`. Expect the query to return 0, or more rows. 
* `db.none()`. Expect the query to return no rows at all. Fail if got any rows.
