<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/s3-antivirus-cli/blob/master/lib/s3_antivirus/help/scan.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

## Example

    $ s3-antivirus scan
    Polling SQS queue for S3 antivirus findings. Started 2019-12-15 04:07:09 +0000...
    Checking s3://test-bucket/eicar.txt
    Downloading s3://test-bucket/eicar.txt to /tmp/b5e986d1-4356-454a-87fe-bc01e5747a7b...
    Scanning s3://test-bucket/eicar.txt...
    => clamdscan /tmp/b5e986d1-4356-454a-87fe-bc01e5747a7b
    /tmp/b5e986d1-4356-454a-87fe-bc01e5747a7b: Eicar-Test-Signature FOUND

    ----------- SCAN SUMMARY -----------
    Infected files: 1
    Time: 0.001 sec (0 m 0 s)
    s3://test-bucket/eicar.txt is infected (deleting)
    Checking s3://test-bucket/a.txt
    Downloading s3://test-bucket/a.txt to /tmp/56da4b41-a672-42d4-a766-1727f5dc256d...
    Scanning s3://test-bucket/a.txt...
    => clamdscan /tmp/56da4b41-a672-42d4-a766-1727f5dc256d
    /tmp/56da4b41-a672-42d4-a766-1727f5dc256d: OK

    ----------- SCAN SUMMARY -----------
    Infected files: 0
    Time: 0.001 sec (0 m 0 s)
    s3://test-bucket/a.txt is clean (tagging)
