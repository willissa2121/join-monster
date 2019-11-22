Contributing to Join Monster
========================

All development of Join Monster happens on GitHub. We actively welcome and appreciate your [pull requests](https://help.github.com/articles/creating-a-pull-request)!

## Issues

Bugs and feature requests are tracked via GitHub issues. Make sure bug descriptions are clear and detailed, with versions and stack traces. Provide your code snippets if any.


## Pull Requests

Begin by forking our repository and cloning your fork. Once inside the directory, you'll need to provide a PostgreSQL and MySQL URI in your environment in the `PG_URL` and `MYSQL_URL` variables (omit the database name from the URI, but keep the trailing slash, e.g. `postgres://user:pass@localhost/` and `mysql://user:pass@localhost/`).

You will also need to create the test databases in Postgres (`test1`, `test2`, and `demo`) and mysql (`test1` and `test2`), and install `sqlite3` to complete the tests.

Setting this up might look something like this on MacOS (in a perfect world).
```sh
# install SQLite3
brew install sqlite3

# install PostgreSQL and get DBs created, skipping creating a user
brew install postgres
brew services start postgres
createdb test1
createdb test2
createdb demo

# install MySQL, create a user, and a database
brew install mysql
brew services start mysql
mysql -u root -e "CREATE USER 'andy'@'%' IDENTIFIED BY 'password';"
mysql -u root -e "ALTER USER 'andy'@'%' IDENTIFIED WITH mysql_native_password BY 'password';"
mysql -u root -e "GRANT ALL PRIVILEGES ON *.* TO 'andy'@'%' WITH GRANT OPTION;"
mysql -u andy -p -e "CREATE DATABASE test1;"
mysql -u andy -p -e "CREATE DATABASE test2;"

export MYSQL_URL=mysql://andy:password@localhost/
export PG_URL=postgres://localhost/

npm install
npm run db-build
npm test
```

Run `npm install` and `npm run db-build` to prepare the fixture data. Check the `scripts` in the `package.json` for easily running the example data and the demo server with GraphiQL. Now you can begin coding.

Before commiting your changes, **run the lint, tests, and coverage to make sure everything is green.** After making your commits, push it up to your fork and make a pull request to our master branch. We will review it ASAP.

## Release on NPM

We will make timely releases with any new changes, so you do not need to worry about publishing. Tagged commits to the master branch will trigger a new build on NPM. Travis-CI will publish the package. Do not publish manually from the command line.

New versions MUST be compliant with [semver](http://semver.org/).

## License

By contributing to Join Monster, you agree that your contributions will be licensed under the LICENSE file in the project root directory.