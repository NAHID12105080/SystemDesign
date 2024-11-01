#  Caching
A mechanism that stores frequently accessed data to prevent repeated, expensive calculations or I/O operations. Caching optimizes performance by serving data from faster storage layers closer to the application, reducing latency and load on the main database.

### 🧊 Caching at Different Levels

### 1. **Main Memory of API Server**

-   **Description**: Caches stored in the main memory (RAM) of an API server.
-   **Advantages**:
    -   Useful for startups with single API endpoints that handle specific cases.
    -   Quick access due to the proximity of the data to the processing server.
-   **Drawbacks**:
    -   **Limited Size**: RAM is finite, limiting the cache's capacity.
    -   **Inconsistency**: As multiple API servers are added, caches can become inconsistent.
    -   **Local Scope**: Each server’s cache is isolated, so other servers can’t access it.

### 2. **Centralized Cache**

-   **Description**: A shared, centralized cache (e.g., Redis or Memcached) accessible by all API servers.
-   **Advantages**:
    -   **Consistency**: All API servers can access the same cached data.
    -   **Scalability**: Reduces redundant cache entries and keeps caches synchronized across servers.
-   **Use Case**: Ideal for distributed systems needing shared data access, such as user sessions or product details.

### 3. **Database Views (Materialized Views)**

-   **Description**: Precomputed views in the database that store the result of a complex query.
-   **Advantages**:
    -   **Efficient Data Access**: Avoids recalculating complex joins or aggregations, reducing query time.
    -   **Consistency with Source Data**: Automatically refreshed based on the underlying data.
-   **Use Case**: Useful for analytics, reporting, or dashboards with complex queries.

### 4. **Browser Cache (Local Storage)**

-   **Description**: Data stored on the client side (e.g., local storage, cookies).
-   **Advantages**:
    -   **Reduced Server Load**: Offloads data storage and retrieval to the client.
    -   **Personalized Experience**: Ideal for user-specific data, such as ranking data in a recommendation system.
-   **Drawbacks**:
    -   **Limited Storage**: Browser storage is restricted in size.
    -   **Data Privacy**: Sensitive data should not be stored in the browser due to potential security risks.

### 5. **Content Delivery Network (CDN)**

-   **Description**: A network of geographically distributed servers that cache responses to reduce latency.
-   **Advantages**:
    -   **Reduced Latency**: Requests are served from the closest CDN edge server, reducing the load on the origin server.
    -   **Lower Database Load**: Requests do not need to go to the main database, decreasing overhead.
-   **Use Case**: Best for static content, media files, and content-heavy sites.

### 6. **Disk Cache of API Server**

-   **Description**: Data is stored on the disk of an API server, which can be larger than memory-based caches.
-   **Advantages**:
    -   **Increased Capacity**: Disk storage is generally larger and can hold more data than memory caches.
    -   **Durability**: Data persists across server restarts.
-   **Drawbacks**:
    -   **Slower Access**: Disk access is slower than memory, introducing latency.
-   **Use Case**: Suitable for large datasets that aren’t accessed as frequently but should persist beyond server reboots.

### 7. **Load Balancer (API Gateway) Cache**

-   **Description**: Load balancers or API gateways that cache responses to reduce redundant requests to API servers.
-   **Advantages**:
    -   **Optimized Traffic Management**: Reduces the number of requests reaching the backend by caching popular responses.
    -   **Enhanced System Scalability**: By caching frequently accessed responses, reduces the load on API servers and databases.
-   **Use Case**: Best suited for frequently accessed, read-heavy endpoints like product catalogs, public profiles, or common resources.

----------
