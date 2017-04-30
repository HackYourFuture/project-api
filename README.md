# HackYourFuture Project-api

This is a HYF Project boilerplate for building a REST API. Let's refresh our minds on this. [READ THIS SO POST](http://stackoverflow.com/questions/671118/what-exactly-is-restful-programming)

## Getting started
Before getting started with this repo, read and repeat the "Getting started" part of the [Angular WebApp Repo](https://github.com/HackYourFuture/project-webapp-angular), and get ready to collaborate in your team

## Step 1: Requirements
Make sure you have these 4 installed
- [Node.js version 7.3.0 or higher](https://nodejs.org/en/) (easily manage Node version with [NVM](https://github.com/creationix/nvm/blob/master/README.md))
- [Docker](https://www.docker.com/community-edition#/download)
- (Windows users only) [Bash](https://www.howtogeek.com/261591/how-to-create-and-run-bash-shell-scripts-on-windows-10/)

## Step 2: Install
Clone your copy of this repo as explained [Angular WebApp Repo](https://github.com/HackYourFuture/project-webapp-angular). Then:
```
// find where you cloned the repo
cd project-api/
npm install // Install NPM dependencies
sh database/create_database.sh // Install database
```

## Step 3: Start the api
```
npm start
```

## Step 4: Read essential docs of these software packages
- [node-db-migrate](https://db-migrate.readthedocs.io/en/latest/) for managing the database structure using migrations
- [expressjs](http://expressjs.com/) for routing
- [mysql2](https://github.com/sidorares/node-mysql2) for talking to MySQL with promise support
- [dotenv](https://github.com/motdotla/dotenv) for saving passwords etc safely.

Nice to read but not required to work:
- [Docker](https://www.docker.com/what-docker)


## Step 5: Try it out (1): Create a MySQL schema
Try to make a new entity (e.g. "products") and its MySQL table
- Go to `package.json` and checkout the `scripts` section. It contains a couple of commands that can execute `node-db-migrate` commands. The most essential ones are: `node run migrate-up` `node run migrate-down` `node run create-migration {{migration-name}}`
- Check if the database is running. Try to connect to the database by running `sh database/connect_database.sh` If it doesn't work, rerun the `sh database/create_database.sh` script to start the db. To see if the mysql docker container is running you can type `docker ps`
- To create a new table we run `npm run create-migration products`
- Go to `./database/migrations/sqls/#####-products-up.sql`
- Write `CREATE TABLE products` command with some fields
- DO NOT FORGET EVER, write the DOWN command by opening the `./database/migrations/sqls/#####-products-down.sql` and writing `DROP TABLE products`. The down migration is always the command that undos the up command`
- Save both migrations
- Run `npm run migrate-up`
- Unless you get errors, your table should be created!
## Step 6: Try it out (2):  Write a route
Try to make a new entity (e.g. "products") and its corresponding route
- Create a file under `./lib/routers` and call it `products.js`
- Take a look at `students.js` or `teachers.js`. What the file does is: start a new `express.Router()` object, add some routes to it (e.g. `router.get` or `router.post` and then export that router). Do the same for `products.js`.
- Add the file to the main express application in `./lib/app.js` by requiring it and giving it a path. Under routers, we define the base path to which our products router will be added. Express will "merge" paths from the main router with the child `products` router.
- Try it out! go to your new path in your browser or using `curl -XGET 'localhost:3000/api/v1/products'`


## (Optional) Connect to MySQL DB from the CLI
```
// Shell:
sh database/connect_database.sh

// Once connected
USE hyf_db;
```
