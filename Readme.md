# Full Stack Capstone Backend
The Casting Agency models a company that is responsible for creating movies and managing and assigning actors to those movies. You are an Executive Producer within the company and are creating a system to simplify and streamline your process.

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Database Setup
For creating database, run the next commands in the terminal:
```bash
(for windows)
CREATE DATABASE casting_agency;
python manage.py db init
python manage.py db migrate
python manage.py db upgrade
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `app.py` file to find the application. 

## Casting Agency Specifications

### Models :
- Movies with attributes title and release date.
- Actors with attributes name, age and gender.

### Endpoints :
- GET /actors and /movies
- DELETE /actors/ and /movies/
- POST /actors and /movies and
- PATCH /actors/ and /movies/

### Roles:
- Casting Assistant
    - Can view actors and movies
- Casting Director
    - All permissions a Casting Assistant has and…
    - Add or delete an actor from the database
    - Modify actors or movies
- Executive Producer
    - All permissions a Casting Director has and…
    - Add or delete a movie from the database


### Tests:
- One test for success behavior of each endpoint
- One test for error behavior of each endpoint
- At least two tests of RBAC for each role


## Server References:
- http://localhost:5000/ 
- https://casting-agency-application.herokuapp.com/

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
    - in API Settings:
        - Enable RBAC
        - Enable Add Permissions in the Access Token
5. Create new API permissions:
    - `get:actors`
    - `get:movies`
    - `post:actors`
    - `post:movies`
    - `patch:actors`
    - `patch:movies`
    - `delete:actors`
    - `delete:moviess`
6. Create new roles for:
    - Producer
        - can `get:movies/actors`
        - can `post:movies/actors`
        - can `patch:movies/actors`
        - can `delete:movies/actors`
    - Director
        - can `get:movies/actors`
        - can `patch:movies/actors`
        - can `post:actors`
        - can `delete:actors`
    - Assistant
        - can `get:movies/actors`
7. Test your endpoints with [Postman](https://getpostman.com). 
    - Register 3 users - assign the Producer role to one and Director role to the other and Assistant role to the third.
    - Sign into each account and make note of the JWT.
    - Import the postman collection `./starter_code/backend/udacity-fsnd-udaspicelatte.postman_collection.json`
    - Right-clicking the collection folder for barista and manager, navigate to the authorization tab, and including the JWT in the token field (you should have noted these JWTs).
    - Run the collection and correct any errors.
    - Export the collection overwriting the one we've included so that we have your proper JWTs during review!
  
## Endpoints

#### GET '/actors'
 - General
    - Returns list of actors objects, and value of success.
- Sample: curl --location --request GET 'http://127.0.0.1:5000/actors' \ --header 'Authorization: Bearer $TOKEN_VALUE

`{
    "actors": [
        {
            "age": 33,
            "gender": "female",
            "id": 1,
            "name": "Emilia Clark"
        },
        {
            "age": 50,
            "gender": "male",
            "id": 2,
            "name": "Gerard Butler"
        },
        {
            "age": 22,
            "gender": "female",
            "id": 3,
            "name": "Omnia Lashen"
        }
    ],
    "success": true
}`

#### GET '/movies'
 - General
    - Returns list of movies objects, and value of success.
- Sample: curl --location --request GET 'http://127.0.0.1:5000/movies' \ --header 'Authorization: Bearer $TOKEN_VALUE

`{
    "movies": [
        {
            "actor_id": 2,
            "id": 1,
            "release_date": "Sun, 02 Feb 2020 00:00:00 GMT",
            "title": "inception"
        },
        {
            "actor_id": 1,
            "id": 2,
            "release_date": "Tue, 03 Mar 2020 00:00:00 GMT",
            "title": "the impossiple"
        },
        {
            "actor_id": 2,
            "id": 3,
            "release_date": "Sat, 04 Apr 2020 00:00:00 GMT",
            "title": "law abiding citic=zen"
        },
        {
            "actor_id": 3,
            "id": 4,
            "release_date": "Mon, 04 May 2020 00:00:00 GMT",
            "title": "aquamarine"
        },
        {
            "actor_id": 3,
            "id": 5,
            "release_date": "Mon, 04 May 2020 00:00:00 GMT",
            "title": "aquamarine"
        }
    ],
    "success": true
}`

#### POST '/actors'
 - General
    - Returns list of actors objects after adding new one, and value of success.
- Sample: curl --location --request POST 'http://127.0.0.1:5000/actors' \ --header 'Authorization: Bearer $TOKEN_VALUE' \ --header 'Content-Type: application/json' \ --data-raw ' {
    "name": "dina",
    "age": 22,
    "gender": "female"
}'

`{
    "actors": [
        {
            "age": 33,
            "gender": "female",
            "id": 1,
            "name": "Emilia Clark"
        },
        {
            "age": 50,
            "gender": "male",
            "id": 2,
            "name": "Gerard Butler"
        },
        {
            "age": 22,
            "gender": "female",
            "id": 3,
            "name": "Omnia Lashen"
        },
        {
            "age": 23,
            "gender": "male",
            "id": 4,
            "name": "Muhammad"
        },
        {
            "age": 22,
            "gender": "female",
            "id": 5,
            "name": "dina"
}
    ],
    "success": true
}`
#### POST '/movies'
 - General
    - Returns list of movies objects after adding new one, and value of success.
- Sample: curl --location --request POST 'http://127.0.0.1:5000/movies' \ --header 'Authorization: Bearer $TOKEN_VALUE' \ --header 'Content-Type: application/json' \ --data-raw '{
 "title":"greenland",
 "release_date":"9/5/2020",
 "actor_id":4
}'

`{
    "movies": [
        {
            "actor_id": 2,
            "id": 1,
            "release_date": "Sun, 02 Feb 2020 00:00:00 GMT",
            "title": "inception"
        },
        {
            "actor_id": 1,
            "id": 2,
            "release_date": "Tue, 03 Mar 2020 00:00:00 GMT",
            "title": "the impossiple"
        },
        {
            "actor_id": 2,
            "id": 3,
            "release_date": "Sat, 04 Apr 2020 00:00:00 GMT",
            "title": "law abiding citic=zen"
        },
        {
            "actor_id": 3,
            "id": 4,
            "release_date": "Mon, 04 May 2020 00:00:00 GMT",
            "title": "aquamarine"
        },
        {
            "actor_id": 3,
            "id": 5,
            "release_date": "Mon, 04 May 2020 00:00:00 GMT",
            "title": "aquamarine"
        },
        {
            "actor_id": 4,
            "id": 6,
            "release_date": "Sat, 09 May 2020 00:00:00 GMT",
            "title": "greenland"
        }
    ],
    "success": true
}`

#### DELETE '/actors'
 - General
    - Returns the id of the deleted actor, and value of success.
- Sample: curl --request DELETE 'http://127.0.0.1:5000/actors/5' \ --header 'Authorization: Bearer $TOKEN_VALUE''

`{
    "deleted": 5,
    "success": true
}`

#### DELETE '/movies'
 - General
    - Returns the id of the deleted movie, and value of success.
- Sample: curl --request DELETE 'http://127.0.0.1:5000/movies/5' \ --header 'Authorization: Bearer $TOKEN_VALUE''

`{
    "deleted": 5,
    "success": true
}`

#### PATCH '/actors'
 - General
    - Returns list of actors after updating the required actor, and value of success.
- Sample: curl --location --request PATCH 'http://127.0.0.1:5000/actors/5' \ --header 'Authorization: Bearer $TOKEN_VALUE' \ --header 'Content-Type: application/json' --data-raw '{
    "age":22
}'

`{
    "actors": [
        {
            "age": 33,
            "gender": "female",
            "id": 1,
            "name": "Emilia Clark"
        },
        {
            "age": 50,
            "gender": "male",
            "id": 2,
            "name": "Gerard Butler"
        },
        {
            "age": 22,
            "gender": "female",
            "id": 3,
            "name": "Omnia Lashen"
        },
        {
            "age": 22,
            "gender": "male",
            "id": 4,
            "name": "Muhammad"
        }
    ],
    "success": true
}`

#### PATCH '/movies'
 - General
    - Returns list of movies after updating the required actor, and value of success.
- Sample: curl --location --request PATCH 'http://127.0.0.1:5000/movies/3' \ --header 'Authorization: Bearer $TOKEN_VALUE' \ --header 'Content-Type: application/json' --data-raw ''

`{
    "movies": [
        {
            "actor_id": 2,
            "id": 1,
            "release_date": "Sun, 02 Feb 2020 00:00:00 GMT",
            "title": "inception"
        },
        {
            "actor_id": 1,
            "id": 2,
            "release_date": "Tue, 03 Mar 2020 00:00:00 GMT",
            "title": "the impossiple"
        },
        {
            "actor_id": 2,
            "id": 3,
            "release_date": "Sat, 04 Apr 2020 00:00:00 GMT",
            "title": "law abiding citizen"
        },
        {
            "actor_id": 3,
            "id": 4,
            "release_date": "Mon, 04 May 2020 00:00:00 GMT",
            "title": "aquamarine"
        },
        {
            "actor_id": 4,
            "id": 6,
            "release_date": "Sat, 09 May 2020 00:00:00 GMT",
            "title": "greenland"
        }
    ],
    "success": true
}`

## Testing by unittest
- test_app.py is implementing the unittest, so go into the worked directory of your project and run in your terminal setup.sh