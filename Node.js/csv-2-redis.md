#node.js api to load csv data to redis

### install csv-2-redis
>npm install csv-2-redis

### Usage: 
#### start docker
>docker run -d --name redis redis

#### load data
>cd node_modules
>node csv-2-redis "../CSTR.csv" "172.18.0.2" "6379" 1

#### Logon redis server
>docker exec -it redis bash
>
>redis-cli

#### redis command
>select1

OK
  
>keys *
  
1) "ActivityInfo:dev:100000-300000/\xe5\xb9\xb4"

2) "ActivityInfo:dev:4000-5500/\xe6\x9c\x88"

>get "ActivityInfo:dev:100000-300000/\xe5\xb9\xb4"

return value matching key
