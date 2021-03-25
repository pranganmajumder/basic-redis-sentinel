#### How to create the sentinel instances along with redis instances:
* Here node1 is the master node & node2, node3 are the slaves node. We need to configure the redis.conf file for every node as here.
Then run the command `redis-server redis.conf` for every node to run the server. some file will be generated `ex:dump.rdb` inside the each node directory 
    * Check if your node1 working as a master & the other two working as a slave by using the following command
    * `redis-cli -p 6379` Now you are in interective mode in address `127.0.0.1:6379`
    * type `INFO replication` it will show you the which node is master & which is slave

* we need to configure the sentinel.conf file for every node & run `redis-sentinel sentinel.conf` for every sentinel . It'll rewrite your sentinel.conf file for every node.
    * Check if your master sentinel is working or not , so go to sentinel interective mode `redis-cli -p 26379`
    * Ask Sentinel about the state of a master `sentinel master mymaster` . It'll show 2 slaves , 2 sentinels. 
    * try to run other command `sentinel replicas mymaster` `sentinel sentinels mymaster`
    * `SENTINEL get-master-addr-by-name mymaster` check which node is master now. 


##### Testing:
###### Set and get key from Database:
  * At first set some key into master node as many as you want 
  * `redis-cli -p 6379` then `set name prangan` 
  * Now check if it's synchonized in the other two slaves or not. if it's in slave also then your setup is ok, otherwise error 
  * Then go to another slave node `redis-cli -p 6381` and try to set a key. But it will show `You can't write against a read only replica` since it's the slave node. you don't have any permission to write there. You can only get a key. 
  * To check all the keys `KEYS *`

###### Testing Failover:
* Run one of those command to down your master node, let's say your master is running on port 6379 
  ```
  redis-cli -p 6379 DEBUG sleep 30   or 
  kill -9 <process id>               or 
  redis-cli -p 6379 DEBUG SEGFAULT

  ```
* Now go to any sentinel using `redis-cli -p 26379` and check which node is master now `SENTINEL get-master-addr-by-name mymaster`  , A new slave will be the new master. 
* Now set some key in the new master, and check if it's being forwarded to the other slave or not. The new key should be forwarded to the slave also.
* Now again restart your previously killed/paused server , like port : 6379 . It'll be added to the slave list. And check if all the set key can be get from your slave 6379. 




###### Resource: 
* https://medium.com/@amila922/redis-sentinel-high-availability-everything-you-need-to-know-from-dev-to-prod-complete-guide-deb198e70ea6
* https://redis.io/topics/sentinel

