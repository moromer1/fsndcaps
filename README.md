# Coffee Shop Backend

## Getting Started

URL : https://fsndcaps.herokuapp.com/

To signup/login and check JWT: https://fsndcaps.herokuapp.com/login

To logout: https://fsndcaps.herokuapp.com/logout

### Installing Dependencies

#### Python 3.9.4

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Environment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virtual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by running:

```bash
pip3 install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) and [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) are libraries to handle the lightweight sqlite database. Since we want you to focus on auth, we handle the heavy lift for you in `./database/models.py`.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Before running the server

Uncomment line 26 in './app.py' in order to populate the database, and comment it again to prevent resetting it after any server restart.

Ensure you have imported/run './setup.sh' to your environment.

## Running the server

Ensure you are working using your created virtual environment.

Each time you open a new terminal session, run:

Linux users:

```bash
export FLASK_APP=api.py;
```

Windows Users:

```bash
set FLASK_APP=api.py;
```

To run the server (it will reload automatically; it is forced to run in debug mode in the bottom of ./app.py'), execute:

```bash
flask run
```

## Tasks

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
   - in API Settings:
     - Enable RBAC
     - Enable Add Permissions in the Access Token
5. Create new API permissions:
   - `get:drinks-detail`
   - `post:drinks`
   - `patch:drinks`
   - `delete:drinks`
6. Create new roles for:
   - Barista
     - can `get:drinks-detail`
   - Manager
     - can perform all actions
7. Test your endpoints with [Postman](https://getpostman.com).
   - Register 2 users - assign the Barista role to one and Manager role to the other.
   - Sign into each account and make note of the JWT.
   - Import the postman collection `./udacity-fsndcaps.postman_collection.json`
   - Right-clicking the collection folder for barista and manager, navigate to the authorization tab, and including the JWT in the token field (you should have noted these JWTs).
   - Run the collection and correct any errors.

## API ARCHITECTURE AND TESTING

### Endpoint Library

@app.errorhandler decorators are used to format and return error responses as JSON objects. @requires_auth decorator are used for Authorization based on roles of the user. Two roles are assigned to this API: 'Manager' and 'Barista'. Public users can GET '/drinks', even if they are not registered fsndcaps users, but have limits on their navigation, i.e: public users can only access '/drinks' by GET.

### All Endpoints

GET '/drinks'
POST '/drinks'
PATCH '/drinks/1'
DELETE '/drinks/1'



# AS A PUBLIC USER:

#### GET '/drinks'

Returns a list of all available drinks belonging to the user, total number of products, and a success value.
Sample curl:
curl --request GET 'https://fsndcaps.herokuapp.com/drinks'

Sample response output:
