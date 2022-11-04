# Wordpress App using Docker
![version](https://img.shields.io/badge/version-1.0-blue)

<sup>Wordpress web app deployed using docker containers having a *main container* with Apache2, Wordpress and PHP configurations and a *database container* with MySQL</sup>

***@author:*** Lazlo Meli \< https://github.com/lazlomeli >

> Built with :

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-%23117AC9.svg?style=for-the-badge&logo=WordPress&logoColor=white)
![Apache](https://img.shields.io/badge/apache-%23D42029.svg?style=for-the-badge&logo=apache&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white)

_________

### 1. Dependencies

> For Windows:
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)

> For Linux:

Install [Docker Desktop](https://www.docker.com/products/docker-desktop/) and do the following in the command line:
```
$ sudo apt install -y docker.io
$ sudo snap install docker
```
### 2. Installation
Clone the repostory in your desired folder. After doing so, `git pull` just to make sure you have the latest version.

_________

### 2. Running the project

Docker Desktop has to be open and running. Once opened, the bottom left window should look like this:
> Docker Desktop succesfully running:

![image](https://user-images.githubusercontent.com/72606659/199951437-a8d591dc-7643-44b4-9bec-e54a0eaa748c.png)

Now, we run the project:

> Using *docker compose*:


> Using *terminal*:

First we create a network to link the containers that we will create
```
$ docker network create nw
```

There are two containers to be built. First go to the `webapp` directory and build the image with the tag `webapp_img`
```
$ cd webapp
$ docker build -t webapp_img .
```

Now run a container with this image using the following command:
```
$ docker run --name webapp -p 8000:80 -v webapp_vol:/var/www/html --network=nw webapp_img
```
> Learn about this command's flags [here](https://docs.docker.com/engine/reference/run/)

The container should look like this in Docker Desktop:

![image](https://user-images.githubusercontent.com/72606659/199953656-7f434c18-916e-468f-9177-29c1e10eee3a.png)

Do the same with the MySQL container:
> Build image:
```
$ cd ..
$ cd mysql
$ docker build -t db .
```
> Run the container:
```
$ docker run --name db --network=nw -v db_vol:/var/lib/mysql db_img
```
The container should appear like this:

![image](https://user-images.githubusercontent.com/72606659/199954099-92d568f6-41db-4f7e-92d1-41a6041616b7.png)

> Check each container configuration using:
```
$ docker inspect containerName
```

Go on `localhost:8000`. You should get this:

<img src="https://user-images.githubusercontent.com/72606659/199954616-3cc6ac41-4ee3-4753-a897-173888ef3ee4.png" width="350" height="400">

Fill up the requested data and you got yourself a fully set up wordpress dashboard:

<img src="https://user-images.githubusercontent.com/72606659/199955262-c5be1491-872f-4e56-97e0-e2ba163a36b8.png" width="400" height="400">

_________

### 3. Performance Testing:
> Apache Benchmark version 2.3 was used

The following command was used to test the server:

`ab -k -n{numberOfRequests} -c{concurrentRequests} http://127.0.0.1:8000/`

> To learn more about the flags used in this command, [here](https://httpd.apache.org/docs/2.4/programs/ab.html) you can find the official Apache documentation about it.

I tested the server with: 
- **100** petitions with **5** concurrent petitions
- **200** petitions with **20** concurrent petitions
- **300** petitions with **30** concurrent petitions
- **500** petitions with **50** concurrent petitions
- **1000** petitions with **100** concurrent petitions

After all the tests, I collected the data and graphied it:
> Time per request in seconds

![image](https://user-images.githubusercontent.com/72606659/200007245-850798ff-7ebe-4aff-b979-05f55fee0a49.png)

Now, let's compare this project's performance to the [Vagrant Wordpress App project's](https://github.com/lazlomeli/Vagrant) one:

Docker is way more efficient. Aproximately **3x more efficient** than Vagrant where 300 petitions took 1/3 than what Vagrant took. Docker app could also take 1000 petitions with 100 concurrent ones and even more.

______

### 5. End
Learn more about Docker [here](https://www.docker.com/)
