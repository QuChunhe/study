# Idea

data
- partitions
- replication

# Papers
[1] Patrick O'Neil, Edward Cheng, Dieter Gawlick, Elizabetch O'Neil. The log-structured merge-tree (LSM-tree). Acta Informatica, 1996, 33(4): 351-385.




# Books

#### Ajay D. Kshemkalyani and Mukesh Singhal. Distributed Computing: Principles, Algorithms, and Systems. Cambridge University Press. 2008

[51] The timestamps assigned to events obey the fundamental monotonicity property; that is, if an event a causally affects an event b, then the timestamp of a is smaller than the timestamp of b.

[52] Elements of T form a partially ordered set over a relation <. This relation is usually called the happened before or causal precedence.


clock consistency condition v.t. strongly consistent

[52] Implementation of logical clocks requires addressing two issues [19]: data structures local to every process to represent logical time and a protocol (set of rules) to update the data structures to ensure the consistency condition.


A local logical clock v.t. A logical global clock,



# Course




# Open Source

## Zookeeper

### command

srvr

### configuration

		tickTime=2000
		dataDir=/var/lib/zookeeper
		clientPort=2181
		#the initLimit is the amount of time to allow followers to connect with a leader.
		initLimit=20
		#The syncLimit value limits how out-of-sync followers can be with the leader.
		syncLimit=5
		
		#server.X=hostname:peerPort:leaderPort
		server.1=zoo1.example.com:2888:3888
		server.2=zoo2.example.com:2888:3888
		server.3=zoo3.example.com:2888:3888




## Kafka

### Broker Configuration

		zookeeper.connect
		broker.id
		


