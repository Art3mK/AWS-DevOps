# Cloudwatch

- CloudWatch does not support metric deletion.
- CloudWatch stores metrics for terminated Amazon EC2 instances or deleted Elastic Load Balancers for 15 months.
- Alarm history is available for 14 days

## putting metrics

- Each metric data point must be marked with a time stamp. The time stamp can be up to two weeks in the past and up to two hours into the future. If you do not provide a time stamp, CloudWatch creates a time stamp for you based on the time the data point was received.
- Metrics exist only in the region in which they are created. Metrics cannot be deleted, but they automatically expire after 15 months if no new data is published to them. Data points older than 15 months expire on a rolling basis; as new data points come in, data older than 15 months is dropped.
- `PutMetricData` or `aws cloudwatch put-metric-data`
- `aws cloudwatch put-metric-data --metric-name Buffers --namespace MyNameSpace --unit Bytes --value 231434333 --dimensions InstanceId=1-23456789,InstanceType=m1.small`
- `aws cloudwatch put-metric-data --metric-name PageViewCount --namespace MyService --value 2 --timestamp 2016-10-20T12:00:00.000Z`

## EC2

*no* RAM monitoring by default

Host Level Metrics:
* CPU
* Network
* Disk
* Status check
    - system status checks
        ```
            checks physical host where instance is running
            Examples:
              - Loss of connectivity
              - Loss of system power
              - software/hardware issues on host
              - resolve by stop/start (migrate to another host)
        ```
    - instanse status checks
        ```
            checks instance, can set manually via API
            Examples:
                - misconfigured networking/startup config
                - lack of memory
                - corrupted file system
                - incompatible kernel
                - resolve by reboot (fix guest OS)
        ```

---

performance monitoring

- Standard = 5 minutes
- Detailed = 1 minute

---

* Dashboards
* Alarms
* Events
* Logs
    - real time application and system monitoring
        ```
        CloudWatch Logs can track the number of errors that occur in your application logs and send you a notification whenever the rate of errors exceeds a threshold you specify.
        ```
    - long term log retention
        ```
        You can use CloudWatch Logs to store your log data indefinitely in highly durable and cost effective storage without worrying about hard drives running out of space. The CloudWatch Logs Agent makes it easy to quickly move both rotated and non rotated log files off of a host and into the log service. You can then access the raw log event data when you need it.
        ```
    - Cloudwatch agent log
        * Supported platforms:
            - Amazon Linux
            - Ubuntu
            - CentOS
            - Red Hat Enterprise Linux
            - Windows

## API

`GetMetricStatistics` API

## Logs

Log archiving.

ec2 instance -> cloudwatch logs -> check patterns -> alert

free agents:
- ubuntu
- amazon linux
- windows

- log streams
    `Deleted after 2 months of expiration of the last piece of data in stream`
- log groups
    `same retention, monitoring, ACLs`
- metric filters
    - doesn't work on existing data
    - return the first 50 results
- retention settings

### Real time log processing

- subscription filters
    - Kinesis streams
    - Lambda
    - Kinesis Firehose

## Alarms

-> SNS
-> Autoscaling

- period should be equal or greater than the metric frequency
- actions must be in the same region as the alarm
- no metrics from unattached EBS
- 5k alarms per AWS account
- `mon-put-metric-alarm` command
- `mon-(enable|disable)-alarm`
- `mon-describe-alarms`
- you can create an alarm before you've created the metric

## Retention period

* Data points with a period of less than 60 seconds are available for 3 hours. These data points are high-resolution custom metrics.
* Data points with a period of 60 seconds (1 minute) are available for 15 days
* Data points with a period of 300 seconds (5 minute) are available for 63 days
* Data points with a period of 3600 seconds (1 hour) are available for 455 days (15 months)

You can retrieve data from any terminated EC2 or ELB

## Events

- near real-time stream of events
- route events to lambda, kinesis, SNS streams, other built-in targets

Components:
- Events
- Rules
- Targets, multiple targets allowed
    - lambda
    - kinesis streams
    - SNS topics
    - built-in
