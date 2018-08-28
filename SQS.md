# SQS

distributed queue system

- messages can contain up to 256Kb of text in any format.
- ensures delivery of each message at least once
- no first in, first out delivery of messages, message can be delivered multiple times in any order
- 30 seconds default timeout, 12 hours visilibity timeout max, `ChangeMessageVisilility` restarts timeout period using new value.
- billed at 64Kb "chunks"
- first 1M sqs requests are free
- single request can have from 1 ti 10 messages
- each 64Kb is billed as 1 request
- 0.5$ per 1M requests per month
- SQS long polling, doesn't return a response until a message arrives, or the long poll times out (max long poll timeout = 20 seconds)
- max retention period for message: 14 days

Visibility timeout starts when worker pulls message from the queue. If processing successfull -> remove message from queue. If no - after visilibily timeout message will appear in queue again.

## Fan out

Message -> SNS topic -> multiple SQL queues.

## Delay queues

If you create a delay queue, any messages that you send to the queue remain invisible to consumers for the duration of the delay period. The minimum delay for a queue is 0 seconds. The maximum is 15 minutes.

For standard queues, the per-queue delay setting is not retroactive—changing the setting doesn't affect the delay of messages already in the queue.

For FIFO queues, the per-queue delay setting is retroactive—changing the setting affects the delay of messages already in the queue.

Delay queues are similar to visibility timeouts because both features make messages unavailable to consumers for a specific period of time. The difference between the two is that, for delay queues, a message is hidden when it is first added to queue, whereas for visibility timeouts a message is hidden only after it is consumed from the queue. The following diagram illustrates the relationship between delay queues and visibility timeouts.

![alt](./images/sqs-delay-queues-diagram.png)

To set delay seconds on individual messages, rather than on an entire queue, use message timers to allow Amazon SQS to use the message timer's `DelaySeconds` value instead of the delay queue's `DelaySeconds` value.

## Billing

- billed at 64Kb "chunks"
- first 1M sqs requests are free
- single request can have from 1 t0 10 messages
- each 64Kb is billed as 1 request
- 0.5$ per 1M requests per month