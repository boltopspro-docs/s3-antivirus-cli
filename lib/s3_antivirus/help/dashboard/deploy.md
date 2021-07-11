<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/s3-antivirus-cli/blob/master/lib/s3_antivirus/help/dashboard/deploy.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

## Examples

### Required options

All the asg, dashboard-name, dead-letter, main-queue options are required. This is because it reflects how this library is used with CloudFormation. This specific CLI command is available as another means for testing only. Example:

    s3-antivirus dashboard deploy --asg s3-antivirus-Asg-1SR73KS433XE8 --dashboard-name S3Antivirus --dead-letter-queue s3-antivirus-Dlq-1C9FX1FZLVACE --main-queue s3-antivirus-Queue-1I1Y8K6PQPN7K

A way to save previous finger-typing energy is to use a variable:

    OPTS="--asg s3-antivirus-Asg-1SR73KS433XE8 --dashboard-name S3Antivirus --dead-letter-queue s3-antivirus-Dlq-1C9FX1FZLVACE --main-queue s3-antivirus-Queue-1I1Y8K6PQPN7K"
    s3-antivirus dashboard deploy $OPTS

We'll use $OPTS in the rest of examples.

### buckets option

The `--buckets` option interpretates 2 values specially: all and regional.

    s3-antivirus dashboard deploy $OPTS --buckets all # build dasbhoard with all buckets on AWS account
    s3-antivirus dashboard deploy $OPTS --buckets regional # build dasbhoard with buckets within the current region

Otherwise the `--buckets` option takes a comma separate list of bucket names:

    s3-antivirus dashboard deploy $OPTS --buckets test-bucket-1
    s3-antivirus dashboard deploy $OPTS --buckets test-bucket-1,test-bucket2

The default `--bucket` option value is `all`.

### ignore-buckets option

There is also an `--ignore-buckets` option that tells the dashboard builder to not include specific buckets in the dashboard.

    s3-antivirus dashboard deploy $OPTS --ignore-buckets non-scanned-bucket-1,non-scanned-bucket-2
