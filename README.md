# Draining-Swarm-Node-Docker

Steps to drain a Swarm Node-

```

1. List all the active nodes
$ sudo docker node ls

2. Start a replicated service using the redis image
$ sudo docker service create --replicas 3 \
> --name redis --update-delay 10s redis:3.0.6

3. Check the tasks assigned to different nodes by the swarm manager
$ sudo docker service ps redis

4. Drain a node that has a task assigned to it
$ sudo docker node update --availability \
> drain hostname_Worker1
Note: Replace hostname_Worker1 with the IP address of your worker1 node. In this case it is ip-172-31-26-147

5. Inspect the drained node and check the Availability of the node
$ sudo docker node inspect --pretty hostname_Worker1

6. Check the updated task assignments for the redis service by the swarm manager
$ sudo docker service ps redis

7. Return the drained worker1 node to an active state
$ sudo docker node update --availability \
> active hostname_Worker1

8. Inspect the worker1 node again to see the updated Availability status
$ sudo docker node inspect --pretty hostname_Worker1

```



