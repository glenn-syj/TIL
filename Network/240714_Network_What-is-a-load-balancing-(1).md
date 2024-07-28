# What is a load balancing (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/28
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

When starting a project with a single DB and a single Web Server, there is a concern of server being crashed. One solution is that increasing the number of servers. Then, how can each access from the clients reach the distributed servers? I've found out that there is a load balancer which distributes the requests from the clients among the web servers.

### Tackling Curiosity

**Load Balancer**

Load Balancing is a process which distributes tasks over a set of resource units. It is in the field of parallel computers. A load balancer handles and distributes the requests. Let's checkout the static approaches in this article.

1. Full knowledge of the tasks

The full knowledge here means two things. One is the independency. The tasks themselves are not affected by each other. The other is subdivision. The execution time and the tasks can be subdivided. Then, the prefix sum can optimize the load balancing.

Each processor can be given the same amoumt of computation. This becomes possible from the divisibility and th e independency. The total operational time is determined by the longest one.

Assume that the total amount of the computation is 42 and the number of processors are 4. Each processor has 10 subdivided units, and two processors each get 1 units. So, the 11 would be the time.

Then, what if the tasks cannot be subdivided? It would be much harder than the case of sub-divisilbe tasks, the relatively fair one can be found.

2. Static Load Balancing

If the execution time is not known, the static load balancing would be possible. The static load balancing is used to decide which server is the most proper among the servers.

- Round Robin Scheduling

The first server gets the first request. The second server, the second request. This matching goes through till the every server receives the reqeust, and the next request goes to the first server again.

If there is a priority from the volume or the power in the server, each server can have diffrent weight.

- Randomized Static

Servers could be assigned tasks randomly. If the number of the tasks is known and not easily be changed, a random permutation caculated earlier would be helpful. However, the randomness harms the performance with the maximum size of the tasks.

- IP hashing

Hahsed user IP address decides which server receives the request. Then, requests from the same client are always sent to the same server till the address becomes changed.

It is a kind of sticky session based on the IP address. As the IP address could be changed with dynamic IP assignment or VPN, the session has a chance of unconnect.

### References

https://en.wikipedia.org/wiki/Load_balancing_(computing)

https://www.f5.com/glossary/load-balancer#:~:text=A%20load%20balancer%20enables%20distribution,on%20a%20number%20of%20servers.
