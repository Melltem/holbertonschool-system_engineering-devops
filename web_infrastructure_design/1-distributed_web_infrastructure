![Diagram](https://i.imgur.com/ahm7KRs.png)


. What is Added and Why?
A load balancer (HAProxy) is added to distribute incoming traffic evenly across two servers. This improves availability and scalability by preventing any single server from becoming overloaded.

Each server contains:

Nginx web server: handles HTTP requests and static content.

Application server: runs backend code for dynamic content.

MySQL database: with one node as Primary (handles writes) and one as Replica (handles reads).

. What is the Load Balancer’s Distribution Algorithm and How Does It Work?
The load balancer uses a round-robin algorithm, which sends each new incoming request to the next server in the list in order. This balances traffic evenly between Server 1 and Server 2.

. Does the Load Balancer Enable Active-Active or Active-Passive Setup? Explain the Difference.
This setup is Active-Active, meaning both servers actively handle requests simultaneously.
In contrast, Active-Passive means one server actively handles all requests while the other waits silently as a backup to take over if the active server fails.

. How Does a Database Primary-Replica (Master-Slave) Cluster Work?
The Primary database node handles all write operations and replicates data asynchronously to the Replica node. The Replica node handles read requests to reduce load on the Primary.

. What is the Difference Between the Primary Node and the Replica Node Regarding the Application?
The application sends write queries only to the Primary node and read queries can be sent to the Replica node to improve performance and scalability.

. What Are the Issues With This Infrastructure?

Single Points of Failure (SPOF): The load balancer itself is a SPOF; if it fails, no requests can be routed. The Primary database is also a SPOF for writes.

Security Issues: There is no firewall or HTTPS encryption, so data may be intercepted or servers attacked.

No Monitoring: Without monitoring tools, issues might go unnoticed, delaying fixes.
