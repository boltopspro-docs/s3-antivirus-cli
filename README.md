<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/s3-antivirus-cli/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# S3 AntiVirus with ClamAV CLI Tool

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This tool is a part of the [S3 AntiVirus Setup Instructions](https://github.com/boltopspro-docs/s3-antivirus/blob/master/docs/instructions-overview.md). Please refer to that doc for the setup steps.

This is a companion tool to the [boltopspro/s3-antivirus](https://github.com/boltopspro-docs/s3-antivirus) blueprint. It provides commands that allow  you to quickly enable s3-antivirus protection for s3 buckets quickly.

* You can enable, disable, show, list an S3 bucket protection setting. IE: Bucket Event Notification Configuration
* You can batch enable a list of buckets quickly.

It also comes with a `scan` command that detects if files uploaded to s3 contain a virus with [ClamAV](https://www.clamav.net/) and auto-deletes or tags them.  Works by processing an SQS Queue that contain messages from [S3 Bucket Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/enable-event-notifications.html).

* Downloads file from s3, scans it, and tags or deletes the file.
* Supports polling for events from buckets in multiple regions.

## Usage Locally

Locally, you can use the tool to enable the S3 Bucket Event Notifications. Summary:

    s3-antivirus bucket enable BUCKET --sqs-arn SQS_ARN
    s3-antivirus bucket disable BUCKET
    s3-antivirus bucket show BUCKET
    s3-antivirus bucket list # to check all buckets protection settings, both enabled and disabled
    s3-antivirus bucket list --status false # to check which buckets have protection disabled

The tool allows you to add the event notification configuration to your bucket quickly. Example:

    s3-antivirus bucket enable s3-event-test-bucket --sqs-arn arn:aws:sqs:us-west-2:112233445566:s3-antivirus-Queue-10XBEVN1HG0BH

The enable command:

1. Creates an regional SNS topic with CloudFormation
2. Connects the SNS Topic to the SQS Queue provided
3. Connects the SNS Topic to the S3 Bucket as a S3 Event topic configuration

So it sets up this event chain:

![](https://img.boltops.com/boltopspro/blueprints/s3-antivirus/s3-antivirus-cli.png)

You can also remove the notification configuration from the bucket

    s3-antivirus bucket disable s3-event-test-bucket

When disabling the bucket notification configuration, the tool provides some safeguard checks to make sure it does not remove additional bucket configurations.

## Batch Commands

You can run the individual command with the wrapper batch command and passing it a FILE.txt containing a list of buckets. Example:

    s3-antivirus batch bucket enable --sqs-arn SQS_ARN encrypt FILE.txt # FILE.txt should always be at the end
    s3-antivirus batch bucket disable FILE.txt

The format of FILE.txt is a list of S3 buckets separated by newlines.  Example:

FILE.txt:

    my-bucket-1
    my-bucket-1

This allows you to enable and disable many buckets quickly.

## Usage on Server

To start a loop that polls SQS and continously scans:

    s3-antivirus scan

## CloudFormation

CloudFormation is used to create the SNS Topic to ensure that it is consistently managed. It also allows you to delete the SNS Topic and associated resources easily. So you can experiment things, and cleanly remove the resources if you wish. Additionally, it designed as as a separate stack so that it is decoupled from the [boltopspro/s3-antivirus](https://github.com/boltopspro-docs/s3-antivirus) blueprint stack.

## Installation

Install with:

    git clone git@github.com:boltopspro/s3-antivirus-cli.git
    cd s3-antivirus-cli
    rake install
    s3-antivirus -h # the s3-antivirus command is now available

Note: The repo is called `s3-antivirus-cli` and the command is called `s3-antivirus`.

### s3-antivirus.conf file

The library is configurable with a s3-antivirus.conf file. This file is generated as part of the [s3-antivirus blueprint](https://github.com/boltopspro-docs/s3-antivirus) so you don't have to generally worry about it. Here is an example for reference though:

/etc/s3-antivirus.conf:

    alerts_topic: arn:aws:sns:us-west-2:112233445566:s3-antivirus-AlertsTopic-5TMHI9I0LGEG
    cloudwatch_metrics: false
    cloudwatch_metrics_log_always: true
    delete: true
    main_queue: https://sqs.us-west-2.amazonaws.com/112233445566/s3-antivirus-Queue-1I1Y8K6PQPN7K
    notify_statuses: clean,infected,oversized
    tag_files: true
    tag_key_prefix: scan
    volume_size: 16
