# Create-custom-wordpress-using-docker

## Description

Here we create custom wordpress using docker. We use docker volume, MySQL docker image and WordPress docker image. Let's move on to the process.

## Installation

If you need to download docker to the EC2 instance, then follow this:

~~~sh
sudo yum install docker -y
sudo systemctl restart docker.service
sudo systemctl enable docker.service
sudo systemctl status docker.service
sudo usermod -a -G docker ec2-user
~~~

Please exit from the instance and login back to reflect the above changes

## Steps performed

## To create network

~~~sh
docker network create wpnet
~~~

## To create volumes for MySQL and WordPress

~~~sh
docker volume create mysql-vol
docker volume create wp-vol
~~~

## To create MySQL container

> Here we use multiline command with the help of \

~~~sh
docker container run \
-d \
--name database \
--network wpnet \
-v mysql-vol:/var/lib/mysql/ \
-e MYSQL_ROOT_PASSWORD="mysqlroot@123" \
-e MYSQL_DATABASE="wordpress" \
-e MYSQL_USER="wpuser" \
-e MYSQL_PASSWORD="wpuser@123" \
mysql:5.6
~~~

## To create WordPress container

> Here we use multiline command with the help of \

~~~sh
docker container run \
-d \
--name wordpress \
--network wpnet \
-v wp-vol:/var/www/html/ \
-p 80:80 \
-e WORDPRESS_DB_HOST=database \
-e WORDPRESS_DB_USER="wpuser" \
-e WORDPRESS_DB_PASSWORD="wpuser@123" \
-e WORDPRESS_DB_NAME="wordpress" \
wordpress:latest
~~~

>Result
![image](https://user-images.githubusercontent.com/100773863/162557137-0e55e617-30b6-44fd-b4f6-821c43a5683d.png)

Now, access the domain using the EC2 IP or EC2 hostname and set up the site:
 >![image](https://user-images.githubusercontent.com/100773863/162557184-82a618d3-422b-4122-9eff-3a60327da29b.png)


Conclusion
This is how we create wordpress site using docker. Please contact me when you encounter any difficulty error while using this terrform code. Thank you and have a great day!


### ⚙️ Connect with Me
<p align="center">
<a href="https://www.instagram.com/dev_anand__/"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/dev-anand-477898201/"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a>






