#[Testing of Mongodb](https://github.com/edwardwbli/mongodb.git)

1. build mongodb docker service with https://github.com/edwardwbli/mongodb.git

2. connect mongodb with below info shown in mongodb starting up

```
2016-10-06T08:01:43.934+0000 I NETWORK  [conn2] end connection 127.0.0.1:60981 (0 connections now open)
=> Done!
========================================================================
You can now connect to this MongoDB server using:

    mongo admin -u admin -p eziXxKd2qBR6 --host <host> --port <port>

Please remember to change the above password as soon as possible!
========================================================================
```

3. mongoimport sample, default host(localhost) and port, without -d option, the db will be ```test``` 
```
cat sample.json | mongoimport -c sample -u admin -p eziXxKd2qBR6
```

4. mongo conection to console,default connection to localhost
```
mongo admin -u admin -p eziXxKd2qBR6
```

5. mongo db selection and data return
```
   >use test
   switched to db test
   >show collections
   sample
   >db.sample.find()
   { "_id" : 10, "username" : "peter", "email" : [ "pbbakkum@gmail.com", "pbb7c@virginia.edu" ] }
```