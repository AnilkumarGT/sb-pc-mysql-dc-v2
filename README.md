# sb-pc-mysql-dc-v2

Forked the https://github.com/spring-projects/spring-petclinic repo

My requirements:
- Have a Spring boot based petclinic app that worked with MySql as db and to be used as part of docker compose
- Simple profile switch on the original project would not work, given that the jdbc url has to have a reference to the mysql container name

Changes done:
- Removed all the mvnw, travis files and all other files that i did not need
- Hardcoded the application.properties file to use mysql (h2 was default in the original codebase)
- Add mysql specific db config entires in the applicaiton.properties file

To run the docker:
1. clone the project
2. do a mvn package
3. docker-compose up --build -d



Was hoping the follwing would work, but it does not work due to missing its own network:
To run on docker, without docker-compose:
1. Do a mvn package first 
2. docker build -t gt/petclinic .
3. First launch mysql:
docker run -e MYSQL_ROOT_PASSWORD=petclinic -e MYSQL_DATABASE=petclinic -p 3306:3306 --name pc-db mysql/mysql-server:5.7 

4. Then launch the petclinic app:
docker run --name pc-app gt/petclinic 
