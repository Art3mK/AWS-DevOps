# RDS

## Multi-AZ failover

- MySQL, Oracle, PostgreSQL -> replication
- SQL Server -> mirroring

`Failover -> RDS DNS endpoint doesn't change`

what for:
- HA
- Backups from secondary
- Restores are take from secondary
- Not a scaling solution
- For scaling use read replicas

You can force failvoer by rebooting instance. `RebootDBInstance` API call

## Read Replicas

scale out for read-heavy workloads, async, `CreateDBInstanceReadReplica` API

- scaling beyond compute or I/O capacity of a single DB instance
- reporting/data warehousing on replicas
- have own DNS endpoint
- could be promoted to standalone DB
- up to 5 read replicas for MySQL, PostgreSQL & MariaDB
- could be in different regions
- async only
- supported for multi-az
- RR can't be multi-az
- chained replication is allowed
- snapshots/automated backups from RR
- `ReplicaLag` cloudwatch metric

## engines

- MySQL
    - native sync
- PostgreSQL
    - native sync
- MariaDB
    - native sync
- Aurora
    * SSD backed virtualized storage layer, replicas share the same storage
- MSSQL
    * no storage scaling

### Aurora

- up to 15 RR
- storage auto-scaling 10Gb -> 64Tb
- backups: retention up to 35 days, stored in S3, no impact on db perf
- data: 6 copies of data across 3 AZ, divided into 10Gb chunks across many disks
    - can lose 2 copies of data without affecting write
    - can lose 3 copies of data without affecting read
    - all storage is self-healing
- replicas
    - aurora replicas: shared volume, up to 15 RR, failover with no data loss
    - MySQL RR: up to 5 RRs, transactional replication, failover with data loss
- security:
    - AES-256 for data in transit
    - can't encrypt unencrypted database

### Creating read replicas

```
if !Mutli-Az
    snapshot of primary DB, brief I/O suspension for ~1 minute
else
    snapshot of secondary DB, no performance hits for primary
```

### Monitoring RDS
* cloudwatch metrics
* RDS monitoring

## Events && EVents Subscriptions

send events to recipients for RDS events via SNS

## Metrics

- DatabaseConnections
- DiskQueueDepth (0 is best)
- FreeStorageSpace
- ReplicaLag (seconds)
- Read|WriteIOPS
- Read|WriteLatency

to-do:
- sharding?