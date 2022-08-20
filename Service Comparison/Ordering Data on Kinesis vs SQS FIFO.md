# Kinesis Data Stream
- user partition key
- same partition key always go to the same shard



# SQS FIFO
- use GroupID
- if Group ID is not used, messages are consumed in the order they are send; good with only one consumer
- use Group ID if there are more than one consumer, group meesages that are related to each other
