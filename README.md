
## Steps to install dependencies and run the frontend with docker and docker-compose

Clone the project:
```shell
git clone git@github.com:pedrocarreira1/birds-frontend-vue.git
```

Change directory to the project folder:
```shell
cd birds-frontend-vue
```

Build the service containers with docker-compose:
```shell
docker-compose build
```

Start and run containers:
```shell
docker-compose up
```

Open the browser and access the frontend at:
```
http://localhost:8080/
```
