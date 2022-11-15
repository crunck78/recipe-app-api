# Section 1:Introduction
## Technical Requirements
1. Machine : Windows / macOS / Linux (Capable of running Docker)
2. GitHub account with the free 2000 actions minutes
3. If using Windows
    - install chocolatey package manager

## API details & Upgrades
1. Features :
    - User Authentication
    - Creating Objects
    - Filtering & Sorting Object
    - Uploading and View Images
2. Software Upgrades
    - Django 3.2 (app will need to be upgraded as newer versions are available)
3. Instead of rebuilding the course as newer versions are available, see how to perform Upgrades. You will learn how to maintain it.
4. Commit to watching start to end, follow the steps and do the quizzes.
    - Speed Up / Slow Down on your own pays.
    - Use a second Screen
    - Answer questions in the Q&A. (Best way to cement your knowledge, put it into practice, and establish confidence in your skills)

## Course Structure
1. App Design (Plan the API and list all technologies needed)
2. Intro to TDD
3. System Setup (prepare our system by installing tools needed during development)
4. Project Setup (Create Project on Github, write Docker file and Docker compose configuration, setup code lending checks and start a new Django project)
5. Github actions (automate running listing and unit tests)
6. TDD with Django
7. Configure Database (install postgres adapter, configure Django to use Database and learn about migrations)
8. Create User Model (first database model add to project)
9. Setup Django Admin (used to manage data in the database through the web browser)
10. API Documentation (Enable automated API documentation used to test our APIs)
11. Build APIs (implement the API endpoints)
12. Image Upload (add support for image upload and filtering)
13. Deploy to AWS (using Docker and Docker components)
14. Summary
15. Upgrades (on new versions of dependencies)

## Getting Help
- 9 out of 10 when you have problem with your code, it is because you have a typo that you can not locate it.
- Bespoke Tool : Code Checker, checks your source code against the original source code and shows diffs.
- Strengthen your problem solving skills by trying to find the answer to your question on your on.
- Problem solving is the most importing skill a developer can have.
- Search for your issue or question first.
- The act of writing the problem down often helps you to understand it in a different way.
- Exhaust all possibilities before posting a new question.
- [How to ask questions on Stack Overflow and get answers](https://londonappdeveloper.com/how-to-ask-questions-on-stack-overflow-and-get-answers/)

# Section 2:App Design
## App Overview
1. App Design
    - Recipe API - Backend Component of a Recipe App
    - Focus is on the backend and the database of the app.
    - Features :
        - 19 API Endpoints : Managing users, recipes, tags, ingredients
        - User Authentication
        - Browsable Admin Interface (Django Admin)
        - Browsable API (Swagger)

    - API Endpoints Overview :
        1. health-check API (Check that our API is healthy, online)
        2. recipe-ingredients API (Get, a list of ingredients using HTTP GET, Put, Patch, Delete a specific ingredient)
        3. recipe API (Get, a list of recipe, Post a new Recipe and specific id endpoints that allow to get a particular recipe, or update using put and patch and delete using a id)
        4. upload API (uploading images to recipes)
    - Keep different data types in different API endpoints because it is easier to use it that way in frontend.

5. tags API (Allow to create and manage tags in the system)
6. schema API (allows to get a schema document which basically defines our API and that is how swagger creates this page an automatically generated API that is added with the Django Framework)
7. users API (creates an user and an authentication token)

## Technologies
1. Python Programming Language used to build our API. Foundation of our API
2. Django Python Web Framework
- Handles :
    - URL Mappings of APIs
    - Object Relational Mapper (Create and manage objects in our database using Python and the admin site.)
    - Admin Site
3. Django REST Framework
    - Django add-on (Adds features for building rest APIs)
4. PostgreSQL
    - Database stores API Data
5. Docker
    - Containerization software. Runs services for each of different applications.
    - Run a Dockerize service of the API and of the Database.
    - Allows to create a development environment used to Build the application.
    - Allows to easily deploy our application to the server.
6. Swagger UI. Generate Automated documentation for API.
    - Use in Browser to view and test different endpoints.
7. Github Actions. Handles the automation of the application.
    - Run testings and linting every time changes are make in the code and push the code on Github.

## Django project structure
- Django Projects are split into various apps.
    1. app/ - Django project
    2. app/core/ - Code shared between multiple apps (database definition using Django models)
    3. app/user/ - User related code (user registration & authentication tokens)
    4. app/recipe/ - Recipe related coe (handling, updating and managing recipes, ingredients and tags)

# Section 3:Test Driven Development
## Test Driven Development
- A development practice.
    1. Write Test
    2. Write code that passes the test code.
    3. Refactor
    4. Rerun Test.
- Unit test is code that tests code.
    - sets up conditions / inputs
    - runs a piece of code
    - check outputs using "assertions"
    - Many benefits
        - Ensures code runs as expected
        - Catches / reduces bugs
        - Improves reliability
        - Provide confidence (Good test coverage)
        - better understanding of code

# Section 4:System Setup
## What to install
- VSCode
- Docker Desktop / Docker for Linux
- Git-SCM

## Setup confirmation

# Section 5:Project Setup
## New Project Overview
- Why use Docker?
    1. Consistent dev and prod environment
        - Docker Image can be use for development as for production.
        - Easier collaboration. (all dependencies are  inside Docker Image )
        - Capture all dependencies as code
            -  Python requirements
            - Operation system dependencies
        - Easier cleanup
- How to use Docker
    - Define Dockerfile (contains all the operating system level dependencies that our project needs)
    - Create Docker Compose configuration (instruct Docker how to run the images that are created from our Docker file configuration)
    - Run all commands via Docker Compose
- Docker on Github Actions
    - Docker Hub introduced rate limit:
        - 100 pulls/ 6hr for unauthenticated users
        - 200 pulls/ 6hr for authenticated users
    - Github Actions is a shared service
        - 100 pulls/ 6hr applied for all users
    - Authenticate with Docker Hub
        - Create account
        - Setup credentials
        - Login before running job
        - Get 200 pulls/ 6hr for free!

## Creating Github project
1. Create Github Account
2. Create Docker Account
3. Create Repository (public, .gitignore for Python, Readme.md)
4. Clone Repository Locally
5. Set the project up with the credentials needed to authenticate with Docker Hub
6. Docker -> Username -> Settings -> Create new Access Token -> Give a description to Token (!Do not close the Window)
7. Github -> Settings -> Secrets -> New repository secret -> Name -> DOCKERHUB_USER -> Value <dockerhub-username> -> Add Secret
8. New repository secret -> Name -> DOCKERHUB_TOKEN -> Value -> <dockerhub-access-token> (You can close the Window on point 6) -> Add Secret
- To revoke access to the project, delete Dockerhub Access Token from Docker.

## Docker and Django
Resource : https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
- Recommended to use Docker when working with Django projects.
- Drawbacks
    - VSCode unable to access interpreter of Python project
    - More difficult to use interactive features (Debugger, Linting tools)
- Configure Docker
    - Create a Dockerfile
    - Lists of steps for creating image
        - Choose a base image (python)
        - install dependencies
        - setup users (inside Docker Container)
- Docker Compose
    - Defines how Docker image(s) should be used
    - Define images as "services"
        - Name (eg:app)
        - Port mappings
        - Volume mappings
- Using Docker Compose
    - Run all commands through Docker Compose
        command : docker-compose run --rm app sh -c "python manage.py collectstatic"
        - docker-compose runs a Docker Compose command
        - run will start a specific container defined in config
        - --rm remove the container as it starts running
        - app is the name of the service
        - sh -c passes in a shell command
        - Command to run inside container
1. First part of command : docker-compose run --rm app is Docker Compose syntax
2. Second part of command : sh -c "python manage.py collectstatic" runs on the container

## Define Python Requirements
1. Create file requirements.txt lists all Python requirements needed in Project
- Add each requirement by a specific version for ex.: Django>=3.2.4,<3.3

## Create project Dockerfile
1. In Project Root add Dockerfile
2. Define use base image [DockerHub](hub.docker.com) here you can search for all base images.
3. Define Maintainer
4. Unbuffer Python (does not buffer the output, the output from python will be printed directly to the console)
5. Copy requirements.txt file from local machine to Docker Image (use to install python requirements)
6. Copy app directory that contain our Django app, inside Docker Image
7. Set WORKDIR, this is the default directory commands are going to be run from when running commands on Docker Image
8. Set EXPOSE port, exposing Port from our container to our machine on container run, allowing to access that port on the container that's running from Docker image.
9. Add command that installs dependencies on our machine.
10. Run command on python alpine image (for each RUN in Dockerfile a image layer is created, avoid this to keep images lightweight as possible by breaking the commands in multiple line by using "&& \" syntax)
    - python -m venv /py (creates python virtual environment as a safeguard against any conflicting dependencies with python image)
    - /py/bin/pip install --upgrade pip (Define a full path for virtual environment, and upgrade pip inside our virtual environment)
    - /py/bin/pip install -r /tmp/requirements.txt (install the list of requirements inside Docker image in virtual environment)
    - rm -rf /tmp (remove tmp directory, we need no extra dependencies on our image once created, best practice is to keep Docker images as lightweight as possible )
    - adduser --disabled-password --no-cached-home django-user (adds a new user inside our image, best practice is not to use the root user. DON'T RUN YOUR APPLICATION USING THE ROOT USER!)
11. ENV updates the environment variable inside the image
12. USER line should be last line of DOckerfile, specifies the user to switch to. Before this line everything is done as ROOT user, after this line everything is done as what the USER was set to.
13. Create .dockerignore file
    - This specifies files to exclude from Docker context.
    - When running Docker image, it uses a so called Docker Context, which is the directory where you running from.

    - Some standard .dockerignore file :
        ".git
        .gitignore

        ## Docker
        .docker

        ## Python
        app/__pycache__/
        app/*/__pycache__/
        app/*/*/__pycache__/
        app/*/*/*/__pycache__/
        .env/
        .venv/
        venv/"
14. Build Docker image
    - command : docker build .

## Create Docker Compose configuration
- Docker Compose Files consist of services needed by application.
- filename : docker-compose.yml
1. Docker Compose version syntax used
2. Define Services
    - app (a service that will run our dockerfile)
        - build :
            - context : . (This means build our docker file in current directory)
        - ports :
            - "8000:8000" (maps port 8000 from local machine to port 8000 inside Docker container)
        - volumes :
            - ./app:/app (maps app directory from local machine to /app  inside Docker container)
        - command : >
            "command that is used to run the service"

command : docker-compose build (It builds the docker image, same as with "docker build .")

## Linting and Testing
- Linting is a tool that check your code formatting
- Handle Linting
    1. Install flake8 package (linting tool)
    2. Run it through Docker Compose
        - command : docker-compose run --rm app sh -c "flake8" (fix linting errors from the bottom-up)
- Testing
    1. Use Django testing suite (comes with django)
    2. Setup tests per Django app
    3. Run test through Docker Compose
        - docker-compose run --rm app sh -c "python manage.py test"

## Configure Flake8
- We do not need flake8 package when we deploy application
1. Add a requirements.dev.txt file.
    - on costume step of build so this requirements are install only when we build an image for our local development server
2. Add list of dev dependencies to requirements.dev.txt file
3. Configure docker-compose on build to install Dev Requirements
4. Configure dockerfile if dev build to install Dev Requirements
5. Configure flake9 to exclude directories and files that we do not need to lint
    - add .flake config file
        - add files to be excluded

## Create Django Project
command : docker-compose run --rm app sh -c "django-admin startproject app ." (Creates a django project named app in the current directory.)
- Because Django is install in Docker Image, run the CLI command just as were on our local machine.
- Sync was made by the volumes we defined in Docker compose.
- Because of that, everything that we create in our local machine, gets mapped to Docker image and vice versa.

## Run project with Docker Compose
command : docker-compose up (command to start docker services)
- Open browser at : 127.0.0.1:8000
- Stop the development server with ctrl + c

## Project setup overview

## Quiz Docker and Docker Compose
1. What is defined in the Dockerfile ?
    - Operation system level dependencies.
    (The Dockerfile is used to build our image, which contains a mini Linux Operating System with all the dependencies needed to run our project.
)
2. What types of issues does linting highlight ?
    - Syntax errors, typos and formatting issues.
    (That's right! Linting is used to ensure code is formatted correctly. It highlights issues like invalid tab spacing and line lengths.)

# Section 6:Configure Github Actions
## What is Github Actions?
    - An automation tool.
    - Similar to Travis-CI, GitLAb CI/CD, Jenkins
    - Allows to run Jobs when code changes
    - Automate tasks
- Common uses
    - Handle deployment (not covered here, complex tasks for DevOps)
    - Code linting
    - Run unit test.
- How it works?
    1. Setup triggers. This are anything that happens to your project on Github.
        - This are documented on [Github Actions Page](https://docs.github.com/en/actions).
    2. Used trigger will be whenever code is pushed to Github. (Push trigger).
    3. Setup jobs when trigger is hit.
        - Our trigger will be Run unit tests.
    4. After job runs, there will be an output of that job, either successful or fail.
- Pricing
    - Charged per minutes. (per jobs run)
    - 2.000 free minutes for Github free accounts
    - Various plans available

## Configuring Github Actions
1. Create a config file at .github/workflows/checks.yml
2. Create triggers in config.
3. Add some steps for running our testing and linting on the project.
4. Docker Hub
    - Needed to pull base images from Docker to local machine
    - Rate limits. (limited to a number of images you can pull in a certain time frame.)
        - Anonymous : 100pulls/6h
        - Authenticated : 200/6h
    - Github Actions uses shared IP Address
        - Limit applied to all users
    - Authenticate with Docker Hub
        - 200pulls/6h all to ourselves
        - More than enough for most projects
        - Additional plans available

    - How to authenticate with Docker Hub?
        1. Register account on https://hub.docker.com
        2. Use docker login during our job
        3. Add secrets to Github project (used to authenticate with docker hub)
            - They allow you to add encrypted variables to the project, so that you store variables that can be used in your jobs.
            - The secrets are encrypted.
            - They are decrypted automatically when they're needed for the jobs you run in Github actions.

## Create Github actions config
Resource : https://github.com/marketplace/actions/docker-login
Resource : https://github.com/marketplace/actions/checkout
Resource : https://github.com/marketplace?type=actions
1. Add .github folder on root of the project
2. Inside .github folder add new folder workflows
3. Add a file inside workflows folder. Name is arbitrarily, extension muss end with .yml
4. Inside .yml file add "---" signifying that is a .yml file
5. Add name : "arbitrarily" it shows on Github actions.
6. Add on : [push] this is the name of the trigger
7. Add jobs:
        test-lint:
            name: Test and lint
            runs-on: ubuntu-20.04
    - Defines a new job called test-lint (idea of the job)
    - Friendly name to see in Github actions
    - runs-on is the runner that we're going to running our job on (there are various runners on the Github ACtions website)
        - This is the operating system that we're going to be running the job on.
8. Add steps. They are different things that run for the job.
    steps:
      - name: Login to Docker Hub
        uses: docker/login-actions@v1 (this action is used to login with docker)
        with:
          username: ${{ secrets.DOCKERHUB_USER }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      - name: Checkout
        uses: actions/checkout@v2 (action provided by Github automatically, checks our code out inside our Github actions job)
      - name: Test
        run: docker-compose run --rm app sh -c "python manage.py test" (runs tests)
      - name: Lint
        run: docker-compose run --rm app sh -c "flake8" (run linting)
- If any of the actions fails, that means they return anything other than exit zero, which is the Linux exit signal for successful exit.
- Docker Compose comes pre-installed in Ubuntu 20.04 runner.

## Test Github ACtions
1. On Github Project -> Actions after you push changes, the job should be visible.

## Quit Github Actions configuration
1. What are common uses for GitHub Actions?
    - Handling deployment, linting and unit tests (These tasks are often automated using GitHub Actions)
2. What language do you use to define GitHub actions?
    - YAML (YML)
3. Why do we need to authenticate with Docker Hub?
    - Because there is a cap on the number of image pulls you can do. (Yes, in order to ensure we can use our 200 free pulls, we need to authenticate.)

# Section 7:Test Driven Development with Django
## Testing in Django
- Django test framework is build into Django and comes out of the box.
    - Based on the unittest library that comes out of the box with Python, but Django test framework adds some additional features.
    - Django adds features
        - Test client - dummy web browser
        - Simulate authentication
        - Temporary database
    - Django REST Framework adds features
        - API test client
- Where do you put test?
    - Placeholder tests.py added to each app
    - Or, create tests/ subdirectory to split tests up
    - Keep in mind:
        - Only use tests.py or tests/ directory (not both)
        - Test modules must start with test_
        - Test directories must contain __init__.py
- Test Database
    - Test code that uses the DB
    - Specific database for tests
        Runs test -> Clears data
    - Happens fr every test (by default)
- Test classes
    - SimpleTestCase
        - No database integration
        - Useful if no database is required for your test
        - Save time executing tests
    - TestCase
        - Database integration
        - Useful for testing code that uses the database
- Writing tests
    - import test class
        - SimpleTestCase - No database
        - TestCase - Database
    - import objects to test
    - Define test class
    - Add test method
    - Setup inputs
    - Execute code to be tested
    - Check output

## Writing tests

## Writing a test using TDD

## Mocking
- Override or change behavior of dependencies
- Avoid unintended side effects
- Isolate code being tested
- Why use mocking?
    - Avoid relying on external services
        - Can't guarantee they will be available
        - Makes tests unpredictable and inconsistent
    - Avoid unintended consequences
        - Accidentally sending emails
        - Overloading external services
- Example :
    register_user() --> create_in_db() --> send_welcome_email() -->
    - Prevent email being send
    - Ensure send_welcome_email() called correctly
- Another benefit :
    - Speed up tests
    check_db() --> sleep() --> check_db()
    - Replace sleep function with a mock so test is faster
- How to mock code ?
    - Use unittest.mock
        - MagicMock/Mock - Replace real objects
        - patch - Overrides code for tests

## Testing web requests
- Testing APIs
    - Make actual request
    - Check result
-  Django REST Framework APIClient
    - Based on the Django's TestClient
    - Make requests
    - Check result
    - Override authentication
- Using the APIClient
    - import APIClient
    - Create client
    - Make request
    - Check result using assertions

## Common testing problems
- Test not running
- Ran less tests than you have
- Possible reasons for tests not running
    - Missing __init__.py in tests/ dir
    - Indentation of test cases
    - Missing test prefix for method (all tests methods muss start with test_)
    - ImportError when running tests
        - Both tests/ dir and tests.py exist.

## Quiz: TDD with Django
1. How does Django detect tests in our project?
    - By looking for modules which start with "test" (The Django test running will look for modules beginning with "test". For example, this could be a test.py file or tests/test_something.py.)
2. What is Mocking in the context of writing unit tests?
    - When you override or change behavior of dependencies for testing purposes. (This helps to isolate the code being tested and avoid unintended side effects)

# Section 8:Configure Database
## Database architecture Overview
- PostgreSQL
    - Popular open source DB
    - Integrates well with Django
- Docker Compose
    - Defined with project (re-usable)
    - Persistent data using volumes
    - Handles network configuration
    - Environment variable configuration
- Architecture
    - Docker Compose
        - Database (PostgreSQL)
        - App (Django)
- Network connectivity
    - Set depends_on on app service to start db first
    - Docker compose creates a network
    - The app service can use db hostname
- Volumes
    - Persistent data
    - Maps directory in container to local machine
## Add database service
- Inside docker-compose.yml
1. Add new service for database
     db:
    image: postgres:13-alpine
    volumes:
      - dev-db-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=devdb
      - POSTGRES_USER=devuser
      - POSTGRES_PASSWORD=changeme
2. Add volumes at the end of the file
    volumes:
        dev-db-data:
3. Update app service that depends on database service
    environment:
      - DB_HOST=db
      - DB_NAME=devdb
      - DB_PASS=changeme
    depends_on:
      - db
    (environments muss match database environments )

## Database configuration with Django
Resource : https://www.psycopg.org/docs/install.html##build-prerequisites
- Configure Django
    - Tell Django how to connect
- Install database adaptor dependencies
    - Install the toll Django uses to connect
- Update Python requirements.txt
- Django needs to know...
    - Engine (type of database)
    - Hostname (IP or Domain name for database)
    - Port
    - Database Name
    - Username
    - Password
- All these settings are defined in settings.py
- Environment variables
    - Pull config values from environment variables
    - Easily passed to Docker containers
    - Used in local dev or prod
    - Single place to configure project
    - Easy to do with Python
-Psycopg2
    The package that you need in order for Django to connect to our database.
- Most popular PostgreSQL adaptor for Python
- Supported by Django
- Installation options
    - psycopg2-binary
        - OK for development
        - Not good for production (not optimized for the production operating system)
    - psycopg2
        - Compiled from source
        - Required additional dependencies
        - easy to install with Docker
- Install psycopg2
    - List of package dependencies in docs
       - C compiler
       - python3-dev
       - libpg-dev
    - Equivalent packages for Alpine
        - postgresql-client
        - build-base
        - postgresql-dev
        - musl-dev
    - Found by searching and trial and error
    - Docker best practice
        - Clean up build dependencies

## Install PostgreSQL database adaptor
1. In docker File
    1. After install pip -> apk add --update --no-cache postgresql-client && \ (needed to connect to postgresql )
    2. Group packages installed ->  apk add --update --no-cache --virtual .tmp-build-deps \ (used to remove this packages later inside docker file)
    3. List packages to install ->  build-base postgresql-dev musl-dev && \
    4. Remove .tmp-build-deps installed packages -> apk del .tmp-build-deps
    5. Update requirements.txt -> psycopg2>=2.8.6,<=2.9

## Configure database in Django

- In Django's settings.py File
1. import os (needed to pull environments variables)
2. Configure Django's DATABASE
// ## Database
// ## https://docs.djangoproject.com/en/3.2/ref/settings/##databases

DATABASES = {
    'default': {
       'ENGINE' : 'django.db.backends.postgresql',
       'HOST' : os.environ.get('DB_HOST'),
       'NAME' : os.environ.get('DB_NAME'),
       'USER' : os.environ.get('DB_USER'),
       'PASSWORD' : os.environ.get('DB_PASS')
    }
}

HOST,NAME,USER,PASSWORD matchup docker-compose environments

3. Remove if created the sqlite Database created by default.

## Fixing database race condition

- Problem with Docker compose
    - using depends_on ensure service starts
     - doesn't ensure application is running
- Docker services timeline
    - Django app may connect to DB before database is Ready!
- Solution
    - Make Django "wait for db"
        - Check for database availability
        - COntinue when database ready
    - Create custom Django management command

- New timeline
    - Django app waits for database ready.

- When is this an issue?
    - Running docker-compose locally
    - Running on deployed environment

## Create core app

- Create new django app (docker-compose run --rm app sh -c "python manage.py startapp core"
)
- Remove tests.py from core, because  we are going to use tests/ dir.
- Remove views.py (core app does not serve any views, it is used for models and things like management command )

## Write test for wait_for_db command

Resource : https://docs.djangoproject.com/en/3.2/howto/custom-management-commands/
Resource : https://docs.python.org/3/library/unittest.mock.html##unittest.mock.Mock.side_effect
Resource : https://docs.djangoproject.com/en/3.2/topics/testing/tools/##django.test.SimpleTestCase

(Creating Django custom command is documented in the official documentation of django )

1. Create command file.
2. import BaseCommand
3. Define Command class
4. in Command class define handle

- Add unit test
    - create py test file for custom commands
    - Mock behavior of database (@patch('core.management.commands.wait_for_db.Command.check'))
    - create test method for database ready
      def test_wait_for_db_ready(self, patched_check):
        """Test waiting for database if database ready."""
        patched_check.return_value = True

        call_command('wait_for_db')

        patched_check.assert_called_once_with(database=['default'])
    - create test method for database fail
     @patch('time.sleep')
    def test_wait_for_db_delay(self, patched_sleep, patched_check):
        """Test waiting for database when getting OperationError."""
        patched_check.side_effect = [Psycopq2Error] * 2 + \
            [OperationalError] * 3 + [True]

        call_command('wait_for_db')

        self.assertEqual(patched_check.call_count, 6)
        patched_check.assert_called_with(database=['default'])

## Add wait_for_db_command

class Command(BaseCommand):
    """Django command to wait for database."""

    def handle(self, *args, **options):
        """Entrypoint for command."""
        self.stdout.write('Waiting for database...')
        db_up = False
        while db_up is False:
            try:
                self.check(databases=['default'])
                db_up = True
            except (Psycopq2Error, OperationalError):
                self.stdout.write('Database unavailable, waiting 1 second...')
                time.sleep(1)

        self.stdout.write(self.style.SUCCESS('Database available!'))

- Temporarily Suppress Linting for unused imports
    - add after unused import ## noqa (tells flake8 to ignore line error)

## Database migrations
- Django ORM
    - Object Relational Mapper (ORM)
    - Abstraction layer for data
        - Django handles database structure and changes
        - Focus on Python code
        - Use any database (within reason)

- Using the ORM
    1. Define models
    2. Generate migration files
    3. Setup database
    4. Store data

- Models
    - Each model maps to a table
    - Models contain
        - Names
        - Fields
        - Other metadata
        - Custom Python logic

- Model general Example
class Ingredient(models.Model):
    """Ingredient for recipes."""
    name = models.CharField(max_length=255)
    user = model.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
   )

- Creating migrations
    - Ensure app is enabled in settings.py
    - Use Django CLI
        - command : python manage.py makemigrations

- Applying migrations
    - Use Django CLI
        - command : python manage.py migration
    - Run it after waiting for database (best practice)

## Update Docker Compose and CI/CD configuration

- Update Docker Compose Command
    command: >
      sh -c  "python manage.py wait_for_db &&
              python manage.py migrate &&
              python manage.py runserver 0.0.0.0:8000"

- Update Checks Command
    run: docker-compose run --rm app sh -c "python manage.py wait_for_db && python manage.py test"

## Summary

- Configured PostgreSQL service
- Set Django database configuration
- Handled race condition
- Added migrations command

## The Django user model

- Django authentication
    - Built in authentication system
    - Framework for basic features
        - Registration
        - Login
        - Auth
    - Integrates with Django admin

- Django user model
    - Foundation of the Django auth system
    - Default user model
        - Username instead of email
        - Not easy to customize
    - Create a custom model for new projects (easer to customize later)
        - Allows for using email instead of username
        - Future proof project for later changes to user model

- How to customize user model
    - Create model
        - Base from AbstractBaseUser and PermissionsMixin
    - Create custom manager
        - Used for CLI integration
    - Set AUTH_USER_MODEL in settings.py
    - Create and run migrations

- AbstractBaseUser
    - Provides features for authentication
    - Doesn't include fields

- PermissionsMixin
    - Support for Django permission system
    - Includes fields and methods

- Common Issues
    - Running migrations before setting custom model
        - Set custom model first
    - Typos in config
    - Indentation in manager or model

## Design custom user model

- User fields
    - email(EmailField)
    - name(CharField)
    - is_active(BooleanField)
    - is_staff(BooleanField)
- User model manager
    - Used to manage objects
    - Custom logic for creating objects
        - Hash password
    - Used by Django CLI
        - Create superuser

- BaseUserManager
    - Base class for managing users
    - Useful helper methods
        - normalize_email : for storing emails consistently
    - Methods we'll define
        - create_user : called when creating user
        - create_superuser : used by ht eCLI to create a superuser (Admin)

## Add user model tests
Resource : https://docs.djangoproject.com/en/3.2/topics/auth/customizing/##django.contrib.auth.get_user_model
Resource : https://docs.djangoproject.com/en/3.2/topics/auth/customizing/##django.contrib.auth.models.AbstractBaseUser.check_password

1. Add test_models.py
from django.test import TestCase
from django.contrib.auth import get_user_model


class ModelTests(TestCase):
    """Test models."""

    def test_create_user_with_email_successful(self):
        """Test creating a user with an email is successful."""
        email = 'test@example.com'
        password = "testpass123"
        user = get_user_model().objects.create_user(
            email=email,
            password=password
       )

        self.assertEqual(user.email, email)
        self.assertTrue(user.check_password(password))

    - best practice go get user model from django.contrib.auth import get_user_model

## Implement custom user model

Resource : https://docs.djangoproject.com/en/3.2/ref/settings/##auth-user-model

1. Clear out models.py
2. Create custom user model
class User(AbstractBaseUser, PermissionsMixin):
    """User in the system"""
    email = models.eMailField(max_length=255, unique=True)
    name = models.CharField(max_length=255)
    is_active = models.BooleanField(default=True)
    is_staff = models.BooleanField(default=False)

    USERNAME_FIELD = 'email'
3. Create user model manager
class UserManager(BaseUserManager):
    """Manager for users."""

    def create_user(self, email, password=None, **extra_field):
        """Create, save and return a new user."""
        user = self.model(email=email, **extra_fields)
        user.set_password(password)
        user.save(using=self._db)

        return user

- Assigne Usermanager to User Model Class objects = UserManager()
- Set AUTH_USER_MODEL = 'core.User' to settings.py

- Make migrations
- docker-compose run --rm app sh -c "python manage.py makemigrations" creates or updates migrations folder
- docker-compose run --rm app sh -c "python manage.py wait_for_db && python manage.py migrate"
django.db.migrations.exceptions.InconsistentMigrationHistory: Migration admin.0001_initial is applied before its dependency core.0001_initial on database 'default'.
- clear the volume (refreshes our database, clear all data in our development database)
    command : docker volume ls (list all volumes)
    command : docker volume rm <volume-name>
    (Error response from daemon: remove recipe-app-api_dev-db-data: volume is in use - [87f2f92562112b44fc86b69db977ddf943015bf7f8fc3e889e9076e03bf46e4d])
    command : docker-compose down (clear  any containers using the volume)
    again command : docker volume rm <volume-name>

- Run test to check that they pass

## Normalize user email.

- Add test_normalize_user :
def test_new_user_email_normalized(self):
        """Test email is normalized for new users."""
        sample_emails = [
            ['test1@EXAMPLE.com', 'test1@example.com'],
            ['Test2@Example.com', 'Test2@example.com'],
            ['TEST3@EXAMPLE.COM', 'TEST3@example.com'],
            ['test4@example.COM', 'test4@example.com']
        ]
        for email, expected in sample_emails:
            user = get_user_model().objects.create_user(email, 'sample123')
            self.assertEqual(user.email, expected)


- Add normalize_email on create user :
def create_user(self, email, password=None, **extra_fields):
        """Create, save and return a new user."""
        user = self.model(email=self.normalize_email(email), **extra_fields)
        user.set_password(password)
        user.save(using=self._db)

        return user

## Require email input
- create test
def test_new_user_without_email_raises_error(self):
        """Test that creating a user without an email raises a ValueError."""
        with self.assertRaises(ValueError):
            get_user_model().objects.create_user('', 'test123')
- implement feature
class UserManager(BaseUserManager):
    """Manager for users."""

    def create_user(self, email, password=None, **extra_fields):
        """Create, save and return a new user."""
        if not email:
            raise ValueError('User must have an email address.')
        user = self.model(email=self.normalize_email(email), **extra_fields)
        user.set_password(password)
        user.save(using=self._db)

        return user

## Add superuser support
- create test
def test_create_superuser(self):
        """Test creating a superuser."""
        user = get_user_model().objects.create_superuser(
            'test@example.com',
            'test123',
       )

        self.assertTrue(user.is_superuser)
        self.assertTrue(user.is_staff)
- implement feature
def create_superuser(self, email, password):
        """Create and return a new superuser"""
        user = self.create_user(email, password)
        user.is_staff = True
        user.is_superuser = True
        user.save(using=self._db)

        return user

## Test user model
- create superuser credentials using CLI
    - command : docker-compose run --rm app sh -c "python manage.py createsuperuser"
- run the app
    - command : docker-compose up
- open browser at http://127.0.0.1:8000/admin/
- enter superuser credentials

## Setup Django Admin
- Django Admin is a Graphical User Interface for models
    - Create, Read, Update, Delete
- Very little coding required

## Enable Django admin
- Enable per model
- Inside admin.py
    - admin.site.register(YourModel)

- Customizing
    - Create class based off ModelAdmin or UserAdmin
    - Override/set class variables

- Changing list of objects
    - ordering : changes order items appear
    - list_display : fields to appear in list

- Add/update page
    - fieldsets: control layout of page
    - readonly_fields : fields that cannot be changed

- Add page
    - add_fieldsets : fields displayed only on add page

## Write tests for listing users

Resource : https://docs.djangoproject.com/en/3.2/topics/testing/tools/##overview-and-a-quick-example
Resource : https://docs.djangoproject.com/en/3.1/ref/contrib/admin/##reversing-admin-urls

- create test_admin.py
- create adminsitetests class
class AdminSiteTests(TestCase):
    """Test for Django admin."""

    def setUp(self):
        """Create user and client."""
        self.client = Client()
        self.admin_user = get_user_model().objects.create_superuser(
            email='admin@example.com',
            password='testpass123'
       )
        self.client.force_login(self.admin_user)
        self.user = get_user_model().objects.create_user(
            email='user@example.com',
            password='testpass123',
            name='Test User'
       )

    def test_users_list(self):
        """Test that users are listed on page."""
        url = reverse('admin:core_user_changelist')
        res = self.client.get(url)

        self.assertContains(res, self.user.name)
        self.assertContains(res, self.user.email)

## Make Django admin list users
- inside core app open admin.py and clear file
- add following
"""
Django admin customization
"""
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin as BaseUserAdmin (used default django auth system)

from core import models


class UserAdmin(BaseUserAdmin):
    """Define the admin pages for users."""
    ordering = ['id']
    list_display = ['email', 'name'] ## type: ignore


admin.site.register(models.User, UserAdmin)

## Support modifying users
- add test
def test_edit_user_page(self):
        """Test the edit user page works."""
        url = reverse('admin:core_user_change', args=[self.user.id])
        res = self.client.get(url)

        self.assertEqual(res.status_code, 200)
- implement feature
    - integrate translation
    from django.utils.translation import gettext_lazy as _
    - update UserAdmin
    fieldsets = (
        (None, {'fields': ('email', 'password')}),
        (
            _('Permissions'),
            {
                'fields': (
                    'is_active',
                    'is_staff',
                    'is_superuser',
               )
            }
       ),
        (_('Important dates'), {'fields': ('last_login',)}),
   )
    readonly_fields = ['last_login']

## Support creating users in Django admin
- create test
def test_create_user_page(self):
        """Test to create user page works."""
        url = reverse('admin:core_user_add')
        res = self.client.get(url)

        self.assertEqual(res.status_code, 200)
- add customization to user admin
add_fieldsets = (
        (None, {
            'classes': ('wide',), ## optionally, just about how the page looks
            'fields':(
                'email',
                'password1',
                'password2',
                'name',
                'is_active',
                'is_staff',
                'is_superuser',
           ),
        }),
   )

## API Documentation
- Importance
    -APIs are designed for developers to use
    - Need to know how to use it
    - An API is only as good as its documentation

- What to document
    - Everything needed to use the API
    - Available endpoints (paths)
        - /api/recipes (example)
    - Supported methods
        - GET, POST, PUT, PATCH, DELETE
    - Format of payloads (inputs)
        - Parameters
        - Post JSON format
    - Format of responses(outputs)
        - Response JSON format
    - Authentication process

- Options for documentation
    - Manual
        - Word doc
        - Markdown
        - Drawback (manually maintained)
    - Automated
        - Use metadata from code (comments)
        - Generate documentation pages

## Auto docs with DRF (Django REST Framework)
- Auto generate docs (with third party library)
    - drf-spectacular
- Generates schema (Document format JSON or YAML)
- Browsable web interface
    - Make test requests
    - Handle auth

- How it works
    1. Generate "schema" file
    2. Parse schema into GUI
- OpenAPI Schema
    - Standard for describing APIs
    - Popular in industry
    - Supported by most API documentation tools
    - Uses popular formats: YAML/JSON

## Quiz : Documentation
- What should you include in your API documentation?
    - Everything needed to use your API (That’s right, ideally your documentation includes everything a developer would need to consume your API.)
- What is an API schema used for?
    - Opening up in tools (eg: Swagger) which can convert it into human readable docs. (The schema file is designed to be loaded into other tools to generate docs.)

## Install drf-spectacular

Resource : https://drf-spectacular.readthedocs.io/en/latest/index.html
Resource : https://pypi.org/project/drf-spectacular/
Resource : https://drf-spectacular.readthedocs.io/en/latest/readme.html##installation

- add it to  requirements.txt (drf-spectacular>=0.15.1,<0.16)
- run docker-compose build to make sure drf-spectacular gets installed
- in app/settings.py
    - in installed_apps add :
        - 'rest_framework',
        - 'drf_spectacular',
- configure rest_framework to generate the schema using drf-spectacular
    - at settings.py bottom add
        - REST_FRAMEWORK = {
            'DEFAULT_SCHEMA_CLASS': 'drf_spectacular.openapi.AutoSchema',
        }

## Configure URLS to serve the documentation

Resource : https://drf-spectacular.readthedocs.io/en/latest/readme.html##take-it-for-a-spin

- add urls to schema and docs in urls.py
    from drf_spectacular.views import (
    SpectacularAPIView,
    SpectacularSwaggerView,
)
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/schema/', SpectacularAPIView.as_view(), name='api-schema'),
    path(
        'api/docs',
        SpectacularSwaggerView.as_view(url_name='api-schema'),
        name='api-docs',
   )
]

## Test Swagger UI

 - start server : docker-compose up
 - navigate to 127.0.0.1:8000/api/docs

## Build user API
- User API
    - User registration
    - Create auth token
    - Viewing/updating profile

- Endpoints
    - user/create/
        - POST Register new user
    - user/token/
        - POST - Create new token
    - user/me
        - PUT/PATCH - Update profile
        - GET - View profile

## Create user app
- command :  docker-compose run --rm app -c "python manage.py startapp user"
- change standard folder to :
    - folder tests
        - __ini__.py
    - apps.py
    - views.py
- add user app to settings.py

## Write test for create user API
- inside user tests create file test_user_api.py
- add following

"""
Tests for the user API.
"""
import email
from django.test import TestCase
from django.contrib.auth import get_user_model
from django.urls import reverse

from rest_framework.test import APIClient
from rest_framework import status


CREATE_USER_URL = reverse('user:create')


def create_user(**params):
    """Create and return a new user."""
    return get_user_model().objects.create_user(**params)


class PublicUserApiTests(TestCase):
    """Test the public features of the user API."""
    def setUp(self):
        self.client = APIClient()

    def test_create_user_success(self):
        """Test creating a user is successful."""
        payload = {
            'email': 'test@example.com',
            'password': 'testpass123',
            'name': 'Test Name',
        }
        res = self.client.post(CREATE_USER_URL, payload)

        self.assertEqual(res.status_code, status.HTTP_201_CREATED)
        user = get_user_model().objects.get(email=payload('email'))
        self.assertTrue(user.check_password(payload['password']))
        self.assertNotIn('password', res.data)

    def test_user_with_email_exists_error(self):
        """Test error returned if user with email exists."""
        payload = {
            'email': 'test@example.com',
            'password': 'testpass123',
            'name': 'Test Name',
        }
        user = create_user(**payload)
        res = self.client.post(CREATE_USER_URL, payload)

        self.assertEqual(res.status_code, status.HTTP_400_BAD_REQUEST)

    def test_password_too_short_error(self):
        """Test an error is returned if password less than 5 chars."""
        payload = {
            'email': 'test@example.com',
            'password': 'pw',
            'name': 'Test Name',
        }
        res = self.client.post(CREATE_USER_URL, status.HTTP_400_BAD_REQUEST)
        user_exists = get_user_model().objects.filter(
            email=payload['email']
       ).exists()
        self.assertFalse(user_exists)

## Implement create user API
- add new serializer for creating objects
    - create serializers.py
    - add following
"""
Serializers for the user API View.
"""
from django.contrib.auth import get_user_model

from rest_framework import serializers


class UserSerializer(serializers.ModelSerializer):
    """Serializer for the user object."""

    class Meta:
        model = get_user_model()
        fields = ['email', 'password', 'name']
        extra_kwargs = {'password': {'write_only': True, 'min_length': 5}}

    def create(self, validated_data):
        """Create and return a user with encrypted password."""
        return get_user_model().objects.create_user(**validated_data)

- create view that uses the serializer
"""
Views for the user API.
"""
from rest_framework import generics

from user.serializers import UserSerializer


class CreateUserView(generics.CreateAPIView):
    """Create a new user in the system."""
    serializer_class = UserSerializer

- Wire up this view to a url
    - create urls.py in user app
    - add following
"""
URL mappings for the user API.
"""
from django.urls import path

from user import views

app_name = 'user'

urlpatterns = [
    path('create/', views.CreateUserView.as_view(), name='create'),
]

- app_name = 'user' used by the reverse mapping defined in test user api

- name='create' is used by the reverse mapping defined in test user api

- connect view in main app
 path('api/user/', include('user.urls')),

 ## Authentication
- Types
    - Basic
        - Send username and password with each request (not recommended)
    - Token
        - Use a token in the http header
    - JSON Web Token (JWT)
        - Use an access and refresh token (mostly used on big databases)
    - Session
        - Use cookies (common)

- Token authentication
    - Balance of simplicity and security
    - Supported out of box by DRF
    - Well support by most clients

- How it works
    1. Create token (post username/password)
    2. Store token on client (Session storage, Local Storage, Cookie, Client Side Database)
    3. Include token in http headers

- Pros and cons
    - Pros
        - Supported out of the box
        - Simple to use
        - Supported ny all clients
        - Avoid sending username/password each time
    - Cons
        - Token needs to be secure on client side
        - Requires database requests

- Logging out
    - Happens on the client side
    - Delete token

- Why no logout API?
    - Unreliable
        - No guarantee it will be called
    - Not useful on API

## Quiz Authentication
1. What is a drawback of using Basic authentication?
    - It requires the client stores the user username and password
    (This is not ideal because it means an attacker could retrieve the user's credentials in clear text.)

## Write tests fot token API
    - add tests to user test api file
def test_create_token_for_user(self):
        """Test generates token for valid credentials."""
        user_details = {
            'name': 'Test Name',
            'email': 'test@example.com',
            'password': 'test-user-password123'
        }
        create_user(**user_details)

        payload = {
            'email': user_details('email'),
            'password': user_details('password')
        }
        res = self.client.post(TOKEN_URL, payload)

        self.assertIn('token', res.data)
        self.assertEqual(res.status_code, status.HTTP_200_OK)

    def test_create_token_bad_credentials(self):
        """Test returns error if credentials invalid."""
        create_user(email='test@xample.com', password='goodpass')

        payload = {'email': 'test@example', 'password': 'badpass'}
        res = self.client.post(TOKEN_URL, payload)

        self.assertNotIn('token', res.data)
        self.assertEqual(res.status_code, status.HTTP_400_BAD_REQUEST)

    def test_create_token_blank_password(self):
        """Test posting a blank password returns an error."""
        payload = {'email': 'test@example.com', 'password': ''}
        res = self.client.post(TOKEN_URL, payload)

        self.assertNotIn('token', res.data)
        self.assertEqual(res.status_code, status.HTTP_400_BAD_REQUEST)

## Implement Token API
1. settings.py add in INSTALLED_APPS 'rest_framework.authtoken',
2. Create new serializer

class AuthTokenSerializer(serializers.Serializer):
    """Serializer for the user auth token."""
    email = serializers.EmailField()
    password = serializers.CharField(
        style={'input_type': 'password'},
        trim_whitespace=False,
   )

    def validate(self, attrs):
        """Validate and authenticate the user."""
        email = attrs.get('email')
        password = attrs.get('password')
        user = authenticate(
            request=self.context.get('request'),
            username=email,
            password=password,
       )
        if not user:
            msg = _('Unable to authenticate with provided credentials.')
            raise serializers.ValidationError(msg, code='authorization')
        attrs['user'] = user
        return attrs
- And update imports
from django.contrib.auth import (
    get_user_model,
    authenticate,
)
from django.utils.translation import gettext as _

from rest_framework import serializers
3. Create Token View
class CreateTokenView(ObtainAuthToken):
    """Create a new auth token for user."""
    serializer_class = AuthTokenSerializer
    renderer_classes = api_settings.DEFAULT_RENDERER_CLASSES
- Update imports
from rest_framework import generics
from rest_framework.authtoken.views import ObtainAuthToken
from rest_framework.settings import api_settings

from user.serializers import (
    UserSerializer,
    AuthTokenSerializer,
)
4. Add new url path to app/user/urls.py
  path('token/', views.CreateTokenView.as_view(), name='token'),

## Write test for manage user API
- add ME_URL = reverse('user:me')
- add tests
    def test_retrieve_user_unauthorized(self):
        """test authentications is required for users."""
        res = self.client.get(ME_URL)

        self.assetEqual(res.status_code, status.HTTP_401_UNAUTHORIZED)


class PrivateUSerApiTests(TestCase):
    """Test API request that require authentication."""

    def setUp(self):
        self.user = create_user(
            email='test@example.com',
            password='testpass123',
            name='Test Name',
       )
        self.client = APIClient()
        self.client.force_authenticate(user=self.user)

    def test_retrieve_profile_success(self):
        """Test retrieving profile for logged in user."""
        res = self.client.get(ME_URL)

        self.assertEqual(res.status_code, status.HTTP_200_OK)
        self.assertEqual(res.data, {
            'name': self.user.name,
            'email': self.user.email,
        })

    def test_post_me_not_allowed(self):
        """Test post is not allowed for the me endpoint."""
        res = self.client.post(ME_URL, {})

        self.assertEqual(res.status_code, status.HTTP_405_METHOD_NOT_ALLOWED)

    def test_update_user_profile(self):
        """Test updating the suer profile for the authenticated user."""
        payload = {'name': 'Update name', 'password': 'newpassword123'}

        res = self.client.patch(ME_URL, payload['name'])

        self.user.refresh_from_db()
        self.assertEqual(self.user_name, payload['name'])
        self.assertEqual(self.user.check_password(payload['password']))
        self.assertEqual(res.status_code, status.HTTP_200_OK)
## Implement manage user API
- override update in serializer
def update(self, instance, validated_data):
        """Update and return user."""
        password = validated_data.pop('password', None)
        user = super().update(instance, validated_data)

        if password:
            user.set_password(password)
            user.save()

        return user
- Update views.py
class ManageUserView(generics.RetrieveUpdateAPIView):
    """Manage the authenticated user."""
    serializer_class = UserSerializer
    authentication_classes = [authentication.TokenAuthentication]
    permission_classes = [permissions.IsAuthenticated]

    def get_object(self):
        """Retrieve and return the authenticated user."""
        return self.request.user

## Recipe API Design
- Features
    - Create
    - List
    - View details
    - Update
    - Delete
- Endpoints
    - /recipes/
        - GET - list all recipes
        - POST - Create recipe
    - /recipes/<recipe_id>
        - GET - View details of recipe
        - PUT/PATCH - Update recipe
        - DELETE - Delete recipe

## APIView vs ViewSets
- What is a view?
    - Handles a request made to a URL
    - Django uses functions
    - DRF uses classes
        - Reusable logic
        Override behaviour
    - DRF also supports decorators
    - APIView and Viewsets = DRF base classes

- APIView
    - Focused around HTTP methods
    - Class methods for HTTP methods
        - GET, POST, PUT, PATCH, DELETE
    - Provide flexibility over URLs and logic
    - Useful for non CRUD APIs
        - Avoid for simple Create, Read, Update, Delete APIs
        - Bespoke logic (eg: auth, jobs, external apis)

- Viewsets
    - Focused around actions
        - Retrieve, list, update, partial update, destroy
    - Map to Django models
    - Use Routers to generate URLs
    - Great for CRUD operations on models

## Write test for recipe model
commit d66e4d01ab6e6e756d717f397e6ebdc41135125c
## Implement recipe model
- ForeignKey allows to set up a relationship between this recipe model and another model
    - Best practice is to reference it from the settings
- Make migrations
    - command : docker-compose run --rm app sh -c "python manage.py makemigrations"
commit 0f1a842620f5c5ea22020ecb9d137e690e478e7b
## Create recipe app
- Create recipe app command : docker-compose run --rm app sh -c "python manage.py startapp recipe"
commit b87b6c0711de91277b79ddcbfd121d67d7786129
## Write tests for listing recipes
commit e64343ee245df27d34de745a268c050256e864ac
## Implement recipe listing
commit d6eaa52ff8b0066e955e78a878a9318e83bd98dc
## Write tests for recipe details API
commit c9ec699e3e8ea38e1fac8a3d9ab8284cdb804aff
## Implement recipe detail API
Resource : https://www.django-rest-framework.org/api-guide/generic-views/##get_serializer_classself
commit 15ccaac4d7e1cdafc6b7bb0f5d2a80c1dea8635a
## Write test for creating recipes
Resource : https://docs.python.org/3/library/functions.html##getattr
commit bc512f7bc5eea9148ede43a0979e72ef9cb53f83
## Implement create recipe API
Resource : https://www.django-rest-framework.org/api-guide/generic-views/##get_serializer_classself
commit b67f3370173e5f577303585f7a13ba61d1c4fd31
## Add additional tests
commit a5045fe4cf9d3b48f5b4a83a3852ac778438928e
## Tags API Design
- Add ability to add recipe tags
- Create model for tags
- Add tag API endpoints
- Update recipe endpoint
    - Adding and listing tags

- Tag Model
    - name
    - user
    - Endpoints
        - api/recipe/tags
            - POST, PUT/PATCH, DELETE, GET
## Add Tag model
- After creating the tests and the model, makemigrations : docker-compose run --rm app sh -c "python manage.py makemigrations"
commit 8da792ff092eea990e1dd89f0ec8badf63fb627a
## Write tests for listing tags
commit 0be43d2b81c556115a075b50672b582bcfad60b6
## Implement tag listing API
commit 56f790f8b883f252388024e72a180924edeb7fdd
## Write tests for updating tags
commit 67a3d08c77da09b0df4f4fc27b901502a3d09e07
## Implement update tag API
commit 7349ee5b9395b64e3f0f10f97261a431d4ff029a
## Write tests for deleting tags
commit 576387112eae6d1f992045bc41f68a6b47839cd9
## Implement delete tag API
commit 2bc6251880e37af0147021429da2dcfb79daf37d
## Nested serializers
- What are nested serializers?
    - Serializer within a serializer
    - Used for fields which are objects
- Example nested data
{
    "title": "Some title",
    "user": "Jeff",
    "tags": [
        {"name": "Tag 1"}, //<--Nested serializer>
        {"name": "Tag 2"}  //<--Nested serializer>
    ]
}
- Limitations
    - Read only by default
    - Custom logic to make writable
## Write tests for creating tags
commit 2b4a3e3981e0f5fe8d68e3e66f102b02f233d80a
## Implement create tag feature
commit 42554b05bdbbb53a8fe7de22c4cb06f1d0040bfa
Resource : https://www.django-rest-framework.org/api-guide/relations/##writable-nested-serializers
Resource : https://www.django-rest-framework.org/api-guide/serializers/##saving-instances
## Write tests for updating recipe tags
commit 2e1034647a156b5031ecb061eb645d56d6fe0ef2
## Implement update recipe tags feature
commit 85a6077e9fae21e38698756fd0229ab7bf1c10c7
## Review tags API in browser
1. Restart / Start dev-server to auto makemigrations.
    - command : docker-compose up
2. Authenticate via Post User API
3. Login via Get Token API
4. Authorize via Token
5. Test APIs
## Summary
- Implemented tag model
- Added tags API
- Updated recipe endpoint to use tags

# Section 15:Build ingredients API
## Ingredients API Design
- Ability to add ingredients to recipes
- Create model for ingredients
- Add ingredients API
- Update recipe endpoint
    - Create ingredient
    - Manage ingredients
- Ingredients Model
    - name
    - user - Owns ingredient
- Ingredients Endpoint
    - /api/recipe/ingredients
        - GET - List ingredients
    - /api/recipe/ingredients/<id>/
        - GET - Get ingredients details
        - PUT/PATCH - Update ingredient
        - DELETE - Remove ingredient
    - /api/recipe/
        - POST - Create ingredients(as part of recipe)
    - /api/recipe/<id>/
        - PUT/PATCH - Create or modify ingredients
## Add ingredient model
- After creating the model create migrations
    - command : docker-compose run --rm app sh -c "python manage.py makemigrations"
commit e7e46369091993f0cc822618be3ebc1cb0624b07
## Write tests for listing ingredients
commit 79e135870445e22d231df6438afafc13987b52b2
## Implement ingredient listing API
commit 27968886f5d82ccc325333f732069cd8444a1c44
## Write tests for updating ingredients
commit 08968c4269ca2682332da787fd310857a5aa8b92
##  Implement update ingredient API
commit c5db2248403cf462187e77401335b049643834c9
## Write tests for deleting ingredients
commit 9607937b803db780cfa7b7c21f841ef831ef769f
## Implement delete ingredient API
commit 1656757acfeafa7fc0661e0c8166e7aab60f42af
## Write tests for creating ingredients
commit 94d43a2efff845aa8b831fc49643939b300b9002
## Implement create ingredients feature
commit 64bf8ff7d76a26e26d565401ca6f3ea6d563a18e
## Write tests for updating recipe ingredients
commit 52eb4268ff07b796059e79ebe3b48fe7149f87df
## Implement update recipe ingredients feature
commit 1b91c8da8337e97f6f719c134bdb15f77515713b
## Refactoring
- What is refactoring?
    - Restructure code
        - Easier to read
        - More efficient
        - Less Duplication
    - Improve performance
    - Does the same thing
- TDD Refactoring
    - TDD makes refactoring easy
    - Run test to ensure code still works
## Refactoring recipe views
commit d2f57bb3ead3d3cb733a9281082fb0ed0dc86edf
## Review ingredient API in browser
## Summary
- Added ingredients model
- Implemented ingredients API
- Updated recipe API
- Refactored code
- Tested in browser

# Section 16: Recipe image API
## Recipe image API design
- Handling static/media files
- Adding image dependencies
- Update recipe model with image field
- Add image upload endpoint
- Image API Design
    - /api/recipe/<id>/upload-image/
        - POST - Upload image
- Additional dependencies
    - Pillow (Python Imaging Library)
        - zlib, zlib-dev
        - jpeg-dev
## Add image handling dependencies
commit 209c630561b3559f848a6befd0344201f8e8ad52
- Rebuild docker images command : docker-compose build
## Static files with Django and Docker
Resource : https://docs.djangoproject.com/en/3.2/howto/static-files/
Resource : https://docs.djangoproject.com/en/3.2/howto/static-files/
- Media and Static
    - Files not generated by Python code
        - Images, CSS, Javascript, Icons
    - Two types:
        - Media - Uploaded at runtime (eg: user uploads)
        - Static - Generated on Build (indirect used static file are for eg: django admin, or django rest framework browsable interface)
- Configuration
    - STATIC_URL - Base static URL on web browser (eg: /static/static)
    - MEDIA_URL - Base media URL on web browser (eg: /static/media/)
    - MEDIA_ROOT - Path to media on filesystem (eg: /vol/web/media)
    - STATIC_ROOT - Path to static files on filesystem (eg: /vol/web/static)
- Docker volumes
    - Store persistent data (a directory on the system that is used and maps to our application) that persist between different runs or even different running instances in app
    - Volume we'll setup:
        - /vol/we - store static and media subdirectories
- Mapping (Django development)
    - A Development Server is used
    - Django make it easy to use static files
- Mapping (Django deployed)
    - Typically you need to use a Proxy
        - Recommended is to use NGINX ( Reverse Proxy Service )
        - Proxy is used to handle all static file in the system
- Collect Static
    - Django provides command to gather static files
        - command python manage.py collectstatic
    - Puts all static files to STATIC_ROOT
        - On Served Deployed Apps you need to have all static files together so that they can be served by the reverse proxy service (because you will not use django development server in production )
## Configure our project to use static files
- Change Docker file to support handling our URL
    - Create directories to store out media files (after creating the user in docker file so that they are not created under root user)
    - command : mkdir -p /vol/web/media
    - command : mkdir -p /vol/web/static && \ (creates all subdirectories in specified path)
    - directories to map to volumes used to store out static and media files
    - command : chown -R django-user:django-user /vol && \ (change the owner of directory and subdirectories )
    - command : chmod -R 755 /vol (change permissions that group and owner can any changes)
- Update Docker Compose YML file
    - Add new volume (dev-static-data)
    - Map the volume to app specific location
        - dev-static-data:/vol/web
    - This is to have persistent data when we developing on our local machine
- Update settings.py file
    - Add URLS and ROOTS paths
        STATIC_URL = '/static/static'
        MEDIA_URL = '/static/media/'

        MEDIA_ROOT = '/vol/web/media'
        STATIC_ROOT = '/vol/web/static/'
- Update urls.py file
    - Add supporting media file with our development server
    - Mimic the behavior that we expect when we are using our django development server allowing it to serve media files
    <code>
    if setting.DEBUG:
    urlpatterns += static(
        settings.MEDIA_URL,
        document_root=settings.MEDIA_ROOT
    )
    </code>
commit 175eff8d2f7f0f6bffa4d387d1d1e0442426aed5
## Modify recipe model to handle storing images
- For generating paths is best to us os.path.join because it's creating the path relative to the os(window | linux | mac etc).
- After adding new fields to a Model, command : docker-compose run --rm app sh -c "python manage.py makemigrations"
commit 30927f95fef5057039c6546d6e03513b34af4600
## Write tests for uploading images
Resource : https://docs.python.org/3/library/tempfile.html#tempfile.NamedTemporaryFile
commit 726a3fa798b3bea8fdcd04f542b5a3cafe143067
## Implement image API
Resource : https://drf-spectacular.readthedocs.io/en/latest/faq.html#filefield-imagefield-is-not-handled-properly-in-the-schema
commit 09c1000aab56dc7fcd3f920e93b026e2497071a8
## Review image uploading in browser
commit a19acb5d972a0ec8346dbebcac65591cc3221000
## Summary
- Added image upload feature
- Configured volumes
- Tested in Browser

# Section 17:Implement filtering
## Filtering Design
- Filter recipes by ingredients / tags
    - Find certain types of recipes
- Filter tags / ingredients by assigned
    - List filter options for recipes
- Define OpenAPI parameters
    - Update documentation
- Example requests
    - Filter recipe by tag(s):
        - GET /api/recipe/recipes/?tags=1,2,3
    - Filter recipe by ingredient(s):
        - GET /api/recipe/recipes/?ingredients=1,2,3
    - Filter tags by assigned:
        - GET /api/recipe/tags/?assigned_only=1
    - Filter ingredients by assigned:
        - GET /api/recipe/ingredients/?assigned_only=1
- OpenAPI Schema
    - Auto generated schema
    - Some things need to be manually configured
        - Custom query params (filtering)
    - Use DRF Spectacular extend_schema_view decorator
##  Add tests for filtering recipes
Resource : https://drf-spectacular.readthedocs.io/en/latest/customization.html
commit 3f934db72d593d3767e853c2af7fd6312552e1d8
## Implement recipe filter feature
commit f05269fb6e8cdf59a4587b93ca3192be1716de18
## Add tests for filtering tags and ingredients
commit e89bb8b911af836d00187970f2cf113f35e72d56
## Implement tag and ingredient filtering
commit 2054c9135069346ffc65fed975669b9aa2a741fe
## Review filtering in browser
## Summary
- Added filtering recipes by tags/ingredients
- Add filtering tags/ingredients by those assigned to recipes
- Customized OpenAPI Schema
# Section 18:Deployment
## Deployment plan
Resource : https://www.youtube.com/watch?v=IoxHUrbiqUo
- Option 1: Installing directly on a server (old method)
    - Creating a virtual server (Linux)
    - Installing dependencies as needed
        - NGINX, Apache web server
        - Python, Python virtual environment
        - Install and run project on server
- Option 2: Use Docker-compose to run app directly on Linux server (not a best approach for long terms solution)
    - Set up Linux server
    - Run service using Docker-compose
        - Create application, set it up to have all dependencies installed in Docker
        - Then simply run Docker-compose file on the server
- Option 3: A managed Docker orchestration service (more expensive, complex to set up)
    - AWS ECS
    - Kubernetes
        - Google Cloud, AWS, Azure, etc.
- Option 4: Use a serverless technology (tied in with vendor, challenging to move away, need to build app specifically to run on serverless platform)
    - Google App Engine
    - Run a serverless application in the cloud
- Various ways to Deploy Django
    - Directly on server
        - Run directly on server
        - Docker
    - Serverless Cloud
        - Google Cloud Run / Google App Engine
        - AWS Elastic Beanstalk / ECS Fargate
- How we'll deploy
    - Single VPS on AWS (EC2) virtual private server
    - Docker / Docker Compose
- Why this approach?
    - Simple solution
    - Great for testing during development
    - Low cost
- Steps we'll take
    1. Configure project for development
    2. Create server on AWS
    3. Deploy app
## Django deployment overview
- Deploying Django
    1. Setup a proxy
    2. Handle static / media files
    3. Configuration
- Components
    - WSGI (Web server gateway interface)
    - Persistent Data
    - Reverse Proxy (accept any request to our application)
- Why use a reverse proxy?
    - Best practice when deploying Django
    - WSGI server great at executing Python (not supper efficient at serving static files)
        - Not great at serving data
    - Web servers
        - Serve data really efficiently
- Applications we'll use
    - nginx
        - Open source, fast, secure, production grade
    - uWSGI
        - Open source, fast, lightweight, simple to use
    - Docker Compose
        - Pulls it all together
- Docker compose setup
    - app uWSGI service
    - PostgreSQL database
    - reverse proxy nginx service
    - static-data volume
    - postgres-data volume
    - Mix of requests to the reverse proxy
- Handle configuration
    - Various approaches
        - Environment variables (what we'll use, popular approach, simple to use)
        - Secret managers
- How configuration works
    - Create .env file on server
    - Set values in Docker compose
- Using AWS
    - App host on AWS
        - Popular platform
    - Responsible for security and costs
    - Must keep your account secure!
        - Look up best practice on AWS
            - Use MFA
            - Use string passwords
            Don't share your account details
            - Keep your machine secure and update to date
            - Delete unused accounts
## Add uWSGI to project
Resource : https://pypi.org/project/uWSGI/
commit 323dde5afc4f5fc2c716e68c7bdde1380e9d14f8
## Create proxy configs
Resource : https://uwsgi-docs.readthedocs.io/en/latest/Nginx.html#what-is-the-uwsgi-params-file
commit bde4c26c904342cc702b395496d485fd82119156
## Create proxy Dockerfile
Resource : https://hub.docker.com/r/nginxinc/nginx-unprivileged
commit 1185d9af2415426fb69b5b8cbc36099720be51f8
## Handling configuration
- Using environment variables
    - Store configuration in a file
    - Retrieve values with Docker compose
    - Pass to applications
## Create docker compose config
Resource : https://docs.docker.com/compose/environment-variables/
commit cb6325272ce2dd1baa1e4910d57c0ea09d830458
## Update Django settings
command : docker-compose -f docker-compose-deploy.yml down (clear any running container)
commit 9e30133ed5c20192149fa7159ea50b9247bcb371
## Creating a virtual server
Resource : https://chocolatey.org/
- Steps
    1. Create AWS account and user
    2. Login to console
    3. Create new virtual server
- AWS Costs calculator.aws
- Connecting to the server
    - Connect via SSH
    - Use same SSH key as for GitHub
- Windows users
    - Doesn't have SSH by default
    - Install Chocolatey (package manager)
        - Run choco install openssh
## Create AWS account and user
## Upload SSH Key to AWS
## Create EC2 instance
command : ssh ec2-user@3.83.68.31 (connect to ec2 instance server)
## Setup GitHub deploy key
- Resource : https://github.com/LondonAppDeveloper/build-a-backend-rest-api-with-python-django-advanced-resources/blob/main/deployment.md#deployment
- Connect to server
- Create ssh key
    - command : ssh-keygen -t ed25519 -b 4096
    - command : cat ~/.ssh/id_ed25519.pub
    - copy output of ssh key
    - On Github account  add ssh key to deploy key on choice repository (recipe-api) (allow write access not necessary, you only want to pull not to push code from production server)
## Install Docker, Compose and Git
Resource : https://github.com/LondonAppDeveloper/build-a-backend-rest-api-with-python-django-advanced-resources/blob/main/deployment.md#install-and-configure-depdencies
## Clone and configure project
- Clone Repository via SSH Link
    - command : git clone git@github.com:crunck78/recipe-app-api.git
## Run service
Resource : https://github.com/LondonAppDeveloper/build-a-backend-rest-api-with-python-django-advanced-resources/blob/main/deployment.md#running-docker-service
## Updating service
- After making changes and pulling changes to server, rebuild app
    - command : docker-compose -f docker-compose-deploy.yml build app
- Restart app in background with not dependencies (does not install dependencies)
    - command : docker-compose -f docker-compose-deploy.yml up --no-deps -d app
commit dc01894ec0736c30f620cff44ccf5be38bbf548c
## Deployment summary
- Configured project for Deployment
- Created EC2 server instance
- Deployed aplication to server
- Updated service

# Section 19:Summary
## Course overview
- Covered :
    - Setting up a project using Docker configuration
    - Github Actions
    - Adding endpoints for creating and managing users, tags, ingredients, recipes
    - Adding filtering to our list endpoints
    - Uploading images
    - Deploying code to a server
    - Writing lost of unit tests!

# section 20:Upgrades
## Upgrading to Django 4
- command : docker-compose build (we need to rebuild images, after upgrading packages versions)