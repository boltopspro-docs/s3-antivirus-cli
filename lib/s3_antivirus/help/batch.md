<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/s3-antivirus-cli/blob/master/lib/s3_antivirus/help/batch.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

## Batch Commands

There are some supported batch commands:

    s3-antivirus batch bucket enable --sqs-arn SQS_ARN encrypt FILE.txt # FILE.txt should always be at the end
    s3-antivirus batch bucket disable FILE.txt

The format of FILE.txt is a list of S3 buckets separated by newlines.  Example:

FILE.txt:

    my-bucket-1
    my-bucket-1

