#  Scaling

Scaling refers to the ability of a system to handle an increasing volume of requests or load. This can be achieved by either enhancing the resources of a single machine (vertical scaling) or adding more machines to share the load (horizontal scaling)


## ⚙️ Two Primary Scaling Strategies

### 1. **Vertical Scaling (HULK)**

-   **Description**: Adds more resources (CPU, RAM, Disk) to an existing machine, making it "bulkier."
-   **Advantages**:
    -   **Ease of Management**: With fewer machines, management is simpler.
-   **Drawbacks**:
    -   **Risk of Downtime**: Upgrades can require server reboots, introducing downtime.
    -   **Physical Limitations**: Limited by hardware constraints (e.g., max supported RAM).
-   **Example**: A mobile phone’s maximum ROM support is limited by its internal architecture, which requires matched interface buses.

### 2. **Horizontal Scaling (Minions)**

-   **Description**: Involves adding more machines to distribute the load, known for scaling "outwards."
-   **Advantages**:
    -   **Fault Tolerance**: If one machine fails, others can continue handling requests.
    -   **Linear Amplification**: Capacity increases with each new machine.
    -   **Infinite Scaling Potential**: In theory, you can keep adding machines to meet demand.
-   **Drawbacks**:
    -   **Complex Architecture**: Managing multiple servers and ensuring data consistency is challenging.
-   **Catch**: Stateful components like databases and caches must be able to handle distributed requests.

----------

## 📈 General Scaling Plan

1.  **Gradual Traffic Increase**:
    
    -   Use **Auto-Scaling Groups** to dynamically add or remove instances based on demand.
2.  **Handling Sudden Traffic Spikes**:
    
    -   Auto-scaling may struggle with sudden large surges due to lag time in instance creation.
3.  **Optimization Strategy**:
    
    -   Start with **Vertical Scaling** for simplicity, then scale **Horizontally** as traffic grows.
    -   Perform **load testing** to understand the unit economy (performance-to-cost ratio) of each server type.
4.  **Implementation**:
    
    -   Begin by vertically scaling the API server.
    -   Introduce a **Load Balancer** for distributing traffic and enabling horizontal scaling.

### 📝 Bottom-Up Scaling Principle

-   Scale **bottom-up** to avoid bottlenecks.
    1.  **Scale the database** first.
    2.  **Then scale the API server**.

----------

## 🗄️ Scaling Databases

To keep up with scaling at the application layer, databases must be able to handle increased load. This can be achieved through vertical scaling, replication, or sharding.

### 1. **Vertical Scaling**: Add more resources (e.g., CPU, RAM) to a single database server.

-   **Pros**: Simpler to implement.
-   **Cons**: Limited by hardware constraints.

### 2. **Read Replicas**

-   **Description**: A **tree-like structure** with a **master node** handling writes and **child nodes** (replicas) handling reads.
-   **Leader Election**: If the master fails, replicas can elect a new master.
-   **Implementation**:
    -   **Master DB**: Stores critical information.
    -   **Replica DBs**: Store data that needs fast access and where security isn’t the main concern.
-   **Use Case**: Ideal for read-heavy workloads.

### 3. **Sharding**

-   **Description**: Distributes data across multiple databases or "shards," each holding a subset of the data.
-   **Implementation**: Divide data based on conditions, directing users to specific shards for optimal performance.
-   **Use Case**: Effective for massive databases where data can be split logically (e.g., by user region or ID range).

----------

### 🔑 Key Takeaways for Scaling Success

-   **Auto-scaling is effective for gradual traffic increases** but may struggle with sudden traffic spikes.
-   **Start by scaling vertically**, then gradually shift to horizontal scaling as the demand grows.
-   **Ensure databases are scaled first** (either by vertical scaling, read replicas, or sharding) before scaling application servers.
-   Use **load testing** to find the most cost-effective scaling strategy.
