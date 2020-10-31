# README

This is a and simple Flask project created following different web tutorials, meant to be deployed in Docker with a mysql database also running in docker. It is assumed that you have already installed Docker. Follow the instructions below to get the app running in your PC.

- Clone this repository to a local folder
- Run the following command to get a mysql database up and running
``` 
docker run --name mysql -d -e MYSQL_RANDOM_ROOT_PASSWORD=yes -e MYSQL_DATABASE=microblog -e MYSQL_USER=microblog -e MYSQL_PASSWORD=tantanakuy mysql/mysql-server:5.7
``` 
- Run the following command to build and run the app image
``` 
docker build -t microblog:latest .
docker run --name microblog -d -p 8080:5050 --rm --link mysql:dbserver -e DATABASE_URL=mysql+pymysql://microblog:tantanakuy@dbserver/microblog microblog:latest
``` 
- Access localhost:8080 in your web browser and start playing around
- To enter as an administrator to the blog, go to http://localhost:8080/admin. For being able to access you must first register and loggin as ADMIN_USER (check .env file ;D )

Note: many files and requirements are left just for the development version, they are not used in deployment


## API test

In application/api/api_routes you can choose to use basic_auth or token_auth for each route by commenting each.

### API test with browser (basic auth in API routes)

http://localhost:8080/api/users
http://localhost:8080/api/users/1

### API test with console (token auth in API routes) 

``` 
virtualenv –python python3 venv
source venv/bin/activate
pip install httpie
``` 

- REQUEST WITH BASIC AUTH:
``` 
http --auth Usuario2:password2 GET http://localhost:8080/api/users
http --auth Usuario2:password2 GET http://localhost:8080/api/users/1
``` 

- GET TOKEN (requires basic auth):
``` 
http --auth user:password POST http://localhost:8080/api/tokens
``` 

- REQUEST WITH TOKEN:
``` 
http GET http://localhost:8080/api/users "Authorization:Bearer AwZTkTz430ORkdivnFnfQqPEgaAK3OrO"
``` 

- DELETE TOKEN:
``` 
http DELETE http://localhost:8080/api/tokens Authorization:"Bearer AwZTkTz430ORkdivnFnfQqPEgaAK3OrO"
``` 
















