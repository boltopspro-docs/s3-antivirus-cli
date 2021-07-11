<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/s3-antivirus-cli/blob/master/lib/s3_antivirus/help/bucket/enable.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

## Example

    s3-antivirus bucket enable my-bucket --sqs-arn arn:aws:sqs:us-west-2:111111111111:s3-antivirus-Queue-123456EXAMPLE

If there's an existing bucket notification, you should inspect it and see if it's safe to override it. To see the existing bucket notification:

    s3-antivirus bucket show my-bucket

To override it, use the `--override` option:

    s3-antivirus bucket enable my-bucket --sqs-arn arn:aws:sqs:us-west-2:111111111111:s3-antivirus-Queue-123456EXAMPLE --override