<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/s3-antivirus-cli/blob/master/lib/s3_antivirus/help/completion.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

## Examples

    s3-antivirus completion

Prints words for TAB auto-completion.

    s3-antivirus completion
    s3-antivirus completion hello
    s3-antivirus completion hello name

To enable, TAB auto-completion add the following to your profile:

    eval $(s3-antivirus completion_script)

Auto-completion example usage:

    s3-antivirus [TAB]
    s3-antivirus hello [TAB]
    s3-antivirus hello name [TAB]
    s3-antivirus hello name --[TAB]
