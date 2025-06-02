# Kafka KRaft Setup - 3 Brokers

This project provides a Docker Compose configuration for setting up a Kafka cluster using the KRaft (Kafka Raft) protocol with 3 brokers. KRaft is Apache Kafka's new consensus mechanism that eliminates the need for ZooKeeper.

## Prerequisites

- Docker
- Docker Compose

## Setup Instructions

1. Clone this repository
2. Navigate to the project directory
3. Run the following command to start the Kafka cluster:
   ```bash
   docker-compose up -d
   ```

## Components

This setup includes:
- 3 Kafka brokers configured with KRaft protocol
- All brokers participate in the quorum for metadata management
- No ZooKeeper dependency (KRaft mode)

## Important Notes

- This setup uses KRaft (Kafka Raft) protocol which is the new consensus mechanism in Kafka and is mandatory after version 4.0
- KRaft eliminates the ZooKeeper dependency, simplifying the architecture
- Having 3 brokers provides fault tolerance and high availability
- The cluster can survive the failure of one broker while maintaining operation

## Stopping the Cluster

To stop the Kafka cluster:
```bash
docker-compose down
```

## Configuration

The configuration is defined in the `docker-compose.yml` file, which sets up:
- Multiple Kafka brokers
- Network settings
- Volume mappings
- KRaft-specific configurations
