# Docker Fastapi Postgres Project Template

A Dockerized FastAPI Postgres project template using Make, and Docker Compose,
that includes **SQLAlchemy**, **Alembic** and an integration test setup.

##  Installation

The only requirements to develop are **Docker** and **Make**.
Docker makes it easy to get started and enables easier switching between projects, operating systems and machines.

To start up the project locally you first clone the project, and then run the following command in the cloned directory:
```sh
$ git clone https://github.com/ashleyramdin/docker-fast-api-postgres-boilerplate.git
$ cd docker-fast-api-postgres-boilerplate
$ make up
```
Then to update the schema using alembic, in another shell:
```sh
$ make migrate
```

The app is set up and should be running at [localhost:5000/docs](localhost:5000/docs).
Code changes are automatically detected using a mounted docker volume.


### Makefile

---
The Makefile is the 'entrypoint' for the tools in this structure,
such that you can easily run different commands without remembering the exact arguments.
Run `make help` to get an overview of the available commands:
```sh
$ make help
up: 
 Run the application
done: lint test 
 Prepare for a commit
test: utest itest  
 Run unit and integration tests
check: 
 Check the code base
lint: 
 Check the code base, and fix it
clean_test:  
 Clean up test containers
migrations: 
 Generate a migration using alembic
migrate: 
 Run migrations upgrade using alembic
downgrade: 
 Run migrations downgrade using alembic
help: 
 Display this help message
```

---

### Installation without Docker
To install a local copy of the python environment (to get code-completion for example),
you must have **Poetry** installed.
Create a poetry environment by running `poetry install` at the root of the project.
To start up the server in the poetry environment and talk to a test sqlite database in `./test.db`, run
```bash
$ export DB_STRING=sqlite:///test.db/
$ poetry run alembic upgrade head && poetry run uvicorn api.main:app --port 5000 --reload
```
Again, the app should be all set up and running at [localhost:5000/docs](localhost:5000/docs).

### Tests

---

The tests are containerized.
They are written using Pytest.
You can run the tests using:
```bash
$ make test
```
This runs the integration & unit tests. If you want to run them separately, use `make itest` to run the integration tests and `make utest` to run the unit tests.

