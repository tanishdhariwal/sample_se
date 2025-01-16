78% of storage used … If you run out, you can't create, edit, and upload files.
[nagios]
docker pull jasonrivers/nagios:latest
docker run --name nagiosdemo -p 8888:80 jasonrivers/nagios:latest



[tomcat-users.xml]

<role rolename="admin-gui,manager-gui,manager-script,manager-status, manager-jmx"/>
<user username="admin" password="1234" roles="manager-gui,admin-gui,manager-script"/>




[Jenkins cicd scripts]

pipeline {
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages {
        stage('git repo & clean') {
            steps {
                bat "rmdir  /s /q SampleMavenJavaProject"
                bat "git clone https://github.com/{ur_git_link}/SampleMavenJavaProject.git"
                bat "mvn clean -f SampleMavenJavaProject"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f SampleMavenJavaProject"
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f SampleMavenJavaProject"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f SampleMavenJavaProject"
            }
        }
    }
}


[docker file redis]
FROM redis:latest  
CMD ["redis-server"]


[docker file calc]
FROM node:16-alpine
WORKDIR /app
COPY calculator.js /app
CMD ["node" , "calculator.js"]


[wordpress docker compose]
version: '3'

services:
  # Database
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    networks:
      - wpsite
    # Wordpress
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - '8000:80'
    restart: always
    volumes: ['./:/var/www/html']
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
    networks:
      - wpsite
networks:
  wpsite:
volumes:
  db_data:



[AWS dockerfile]
FROM nginx:alpine
COPY . /usr/share/nginx.html


[AWS mavenweb dockerfile]
FROM tomcat:9-jdk21
COPY target/*war /usr/local/tomcat/webapps/


[for someone that is fucking up html]
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    ZA WARUDO
</body>
</html>
