# What is load balancer

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/14
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

### References
