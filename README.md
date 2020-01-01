### Spin up Redis on Docker and some basic commands

#### Creating a Redis container 
```
[root@ip-172-31-37-15 ~]# docker run -d --name redis -p 6379:6379 redis
ed5e3238782f335b2c32e61c955d9dab281de210cf06001d94dbdd0d0c69b1bf
[root@ip-172-31-37-15 ~]# docker container ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
ed5e3238782f        redis               "docker-entrypoint.s…"   13 seconds ago      Up 11 seconds       0.0.0.0:6379->6379/tcp   redis
```
### Executing commands inside the Redis Container
```
[root@ip-172-31-37-15 ~]# docker exec -it redis redis-cli
127.0.0.1:6379> 
```
#### Setting up key - value 

```
127.0.0.1:6379> set name "test-work"
OK
127.0.0.1:6379> get name
"test-work"
127.0.0.1:6379> 
```

#### Setting up key - value with expiration 
```
127.0.0.1:6379> get nametest
"test-work3"
127.0.0.1:6379> get nametest
(nil)
```
#### Checking if the key already exists
```
- Key not existing
127.0.0.1:6379> exists nametest
(integer) 0  

- Key exists 
127.0.0.1:6379> exists name
(integer) 1
```
#### Deleting the key
````
(integer) 1
127.0.0.1:6379> del name
(integer) 1
127.0.0.1:6379> exists name
(integer) 0
127.0.0.1:6379> 
````
#### Appending contents to the key

````
127.0.0.1:6379> append name "test-work"
(integer) 9
127.0.0.1:6379> get name
"test-work"

127.0.0.1:6379> append name "work2"
(integer) 14
127.0.0.1:6379> get name
"test-workwork2"
127.0.0.1:6379> 
````

#### Subscribing channels
````
127.0.0.1:6379> subscribe newvideos 
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "newvideos"
3) (integer) 1
````

#### Publish contents to the channels
````
127.0.0.1:6379> publish newvideos "NEW VIDEO !!!!"
(integer) 1
127.0.0.1:6379> publish newvideos "C# !!!"
(integer) 1


[root@ip-172-31-37-15 ~]# docker exec -it redis redis-cli
127.0.0.1:6379> subscribe newvideos 
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "newvideos"
3) (integer) 1
1) "message"
2) "newvideos"
3) "NEW VIDEO !!!!"
1) "message"
2) "newvideos"
3) "C# !!!"
````
