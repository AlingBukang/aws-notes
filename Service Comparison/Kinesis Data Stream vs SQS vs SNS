# SQS
- retention period: `default 4 days; max 14 days`
- unlimited messages in queue
- consumers "pull data"
- data is deleted after consumed
- can have unlimited consumers(workers)
- no throughput provisioning needed
- ordering guarantees only on FIFO queues
- individual message delay capability
- 120k inflight messages for standard and 20k FIFO messages - messages already received by consumers but not yet deleted from the queue


# Kinesis Data Stream
- retention: `default 24 hours; max 365 days`
- supports provisioned mode or on-demand capacity mode
- standard: pull data (2 mb per shard); enhanced-fan out: push data (2 mb per shard per consumer)
- for real-time big data, analytics and ETL
- can ingest loads of data more than SQS
- data can be replayed
- ordering at shard level


# SNS
- publish/subscribe model (pub/sub)
- pushes data to subscribers
- 12,500 max subscribers
- data is not persisted
- 100,00 max topics
- no throughput provisioning needed
- integrates with SQS fan-out architecture pattern
- FIFO capability for SQS FIFO