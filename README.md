##### Summary:
* Here node1 is the master node & node2, node3 are the slaves node. We need to configure the redis.conf file for every node as here.
Then run the command `redis-server redis.conf` for every node to run the server. some file will be generated in that node directory

* we need to configure the sentinel.conf file for every node & run `redis-sentinel sentinel.conf` for every sentinel


###### Resource: 
* https://medium.com/@amila922/redis-sentinel-high-availability-everything-you-need-to-know-from-dev-to-prod-complete-guide-deb198e70ea6
* https://redis.io/topics/sentinel

