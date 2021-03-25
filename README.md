##### How to create the sentinel instances along with redis instances:
* Here node1 is the master node & node2, node3 are the slaves node. We need to configure the redis.conf file for every node as here.
Then run the command `redis-server redis.conf` for every node to run the server. some file will be generated `ex:dump.rdb` inside the each node directory 
    * Check if your node1 working as a master & the other two working as a slave by using the following command
    * `redis-cli -p 6379` Now you are in interective mode in address `127.0.0.1:6379`
    * type `INFO replication` it will show you the which node is master & which is slave

* we need to configure the sentinel.conf file for every node & run `redis-sentinel sentinel.conf` for every sentinel






###### Resource: 
* https://medium.com/@amila922/redis-sentinel-high-availability-everything-you-need-to-know-from-dev-to-prod-complete-guide-deb198e70ea6
* https://redis.io/topics/sentinel

