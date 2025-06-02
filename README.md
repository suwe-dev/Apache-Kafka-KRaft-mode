# Apache Kafka KRaft Cluster Setup

This project implements a robust Apache Kafka cluster using the KRaft (Kafka Raft) consensus protocol, eliminating the need for ZooKeeper. The setup consists of 6 nodes in total: 3 nodes operating as both controllers and brokers (nodes 1-3), and 3 dedicated broker-only nodes (nodes 4-6), providing a highly available and scalable Kafka environment.

## Prerequisites

- Docker Engine (version 20.10.0 or later)
- Docker Compose (version 2.0.0 or later)
- At least 10GB of free disk space

## Getting Started

### Clone and Navigate
```bash
git clone Apache-Kafka-KRaft-mode
cd Apache-Kafka-KRaft-mode
```

### Start the Cluster
```bash
docker compose up -d
```

### Access Kafka UI
Open your browser and navigate to:
```
http://localhost:9000
```

### Shut Down the Cluster
```bash
docker compose down
```

## Configuration Explanations

### User Root Permission (`user: root`)
The `user: root` configuration is used in our setup for the following reasons:
- To ensure proper permissions for log directory access and management
- java.nio.file.AccessDeniedException will be resolved
- To allow Kafka to bind to lower-numbered ports if needed
- To handle volume mounts and data persistence effectively

### Volumes Configuration
Volumes are used in this setup for several critical purposes:
- Data persistence across container restarts
- Independent storage management for each broker
- Prevention of data loss during container updates or crashes
- Improved I/O performance through Docker's volume management

### Depends On Configuration
The `depends_on` parameter is utilized to:
- Ensure proper startup order of services
- Guarantee that controller nodes (1-3) are available before broker-only nodes start
- Maintain cluster stability by preventing race conditions during startup
- Enable the UI to start only after all Kafka brokers are running

Each broker-only node (4-6) depends on the controller nodes (1-3) to ensure the cluster has established leadership before attempting to join. Similarly, the Kafka UI service depends on all brokers to ensure it can properly connect to the entire cluster.
