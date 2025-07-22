![Diagram](https://i.imgur.com/4HhJnMS.png)



. What is Added and Why?

1 Server: A new server is added to split the components — instead of having all services on the same machine, now each component (web server, app server, database) runs on a dedicated server. This allows better performance, easier scaling, and clearer separation of responsibilities.

1 Load Balancer (HAProxy) configured in a cluster with another load balancer for high availability. If one fails, the other takes over. This removes the single point of failure (SPOF) at the load balancer level.

. Web Server vs Application Server
(As explained on f5.com/glossary)

Web Server (e.g., Nginx): Handles HTTP requests, serves static files (HTML, CSS, images), and forwards dynamic requests to the application server.

Application Server (e.g., Gunicorn, uWSGI): Processes dynamic content by running the backend application code (e.g., Python, PHP, Node.js), connects to the database, and returns responses to the web server.

Splitting these two lets each handle only what it's best at, increasing efficiency and making it easier to scale parts independently.

Why Split Components?
Web Server (Nginx): Handles incoming HTTP requests efficiently, especially static content. Splitting it ensures it doesn’t get slowed down by app/database tasks.

Application Server: Runs dynamic code (business logic), and can be scaled independently of other services if traffic increases.

Database Server (MySQL): Centralized data management, write and read handling, and replication (if needed). Isolated for performance and security.

Load Balancer Cluster Setup
HAProxy Cluster (Active-Passive):

One load balancer handles all traffic (active)

Second is on standby (passive) and automatically takes over if the active one fails

Ensures high availability and removes the load balancer as a SPOF
