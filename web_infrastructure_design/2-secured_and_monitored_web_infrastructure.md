![Diagram](https://i.imgur.com/8X43K41.png)



. What is Added and Why?

3 Firewalls: One per server, to restrict incoming/outgoing traffic to only essential ports (e.g., 80/443, 3306).

1 SSL Certificate: To enable HTTPS and encrypt user data in transit.

3 Monitoring Agents: One on each server to send logs, metrics, and usage data to a centralized monitoring system like SumoLogic.

. What Are Firewalls For?
Firewalls help prevent unauthorized access by filtering incoming and outgoing traffic based on a set of security rules. They protect each server from external threats, limit exposure, and enforce network security policies.

. Why is the Traffic Served Over HTTPS?
HTTPS encrypts the data exchanged between users and the server using SSL/TLS. This protects sensitive information from being intercepted, ensures data integrity, and confirms the server's authenticity to the user.

. What is Monitoring Used For?
Monitoring allows engineers to observe system performance, detect problems early, and respond to errors or downtime. It ensures high availability and helps with debugging and optimization.

. How is the Monitoring Tool Collecting Data?
Each server has a monitoring agent (client) installed. This agent collects logs, metrics (CPU, memory, disk usage), application performance data, and sends it to a central dashboard (like SumoLogic) over a secure connection.

. What to Do If You Want to Monitor Web Server QPS (Queries Per Second)?
You can:

Enable logging on the Nginx web server

Use a monitoring agent or script to count the number of requests per second

Send that data to the monitoring platform, and visualize it on a dashboard with alerts if QPS exceeds thresholds

Issues With This Infrastructure
. Why Terminating SSL at the Load Balancer Level Is an Issue
If SSL is terminated at the load balancer, the traffic between the load balancer and the backend servers is unencrypted. This can expose sensitive data if someone gains access to the internal network. A better approach is end-to-end encryption or re-encryption between load balancer and servers.

. Why Having Only One MySQL Server Capable of Accepting Writes Is an Issue
If the single Primary MySQL server fails, no write operations can be performed. The system becomes read-only until a failover mechanism is manually or automatically triggered. This creates a single point of failure for database writes.

. Why Having Servers With All the Same Components Might Be a Problem
When each server includes web server, application server, and database, it increases complexity in synchronization, resource use, and troubleshooting.

Database replication lag can cause inconsistency

Overhead of running multiple databases on each server

Difficult to scale components independently (e.g., scale web servers separately from DBs)
