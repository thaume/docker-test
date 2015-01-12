# Docker test

## Build your project and start the server
- Install docker & boot2docker (brew install docker && brew install boot2docker)

### Start boot2docker
```
boot2docker init
boot2docker up
```
You might need to copy/paste some env vars.

### Build the container
```
docker build -t thaume/docker-test:0.2 .
```

### Start redis
```
docker run -d --name="myredis" -p 6379:6379 dockerfile/redis
```

### Run the container
```
docker run -i -t --rm -p 3000:3000 -v `pwd`:/src --name="myapp" --link myredis:myredis -e REDIS_HOST="myredis" thaume/docker-test:0.2
```

### Install dependencies & nodemon & start the server
```
npm i && npm i -g nodemon@dev
nodemon app.js
```

## Error troubleshooting

### Port forwarding
In the context of your machine (not from within boot2docker)
```
VBoxManage controlvm boot2docker-vm natpf1 "docker-test,tcp,127.0.0.1,3000,,3000"
```
