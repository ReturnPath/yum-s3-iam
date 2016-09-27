# yum-s3-iam

This is a [yum](http://yum.baseurl.org/) plugin that allows for
private AWS S3 buckets to be used as package repositories. The plugin
utilizes AWS [Identity and Access Management](http://aws.amazon.com/iam/)
(IAM) roles for authorization, removing any requirement for an access or
secret key pair to be defined anywhere in your repository configuration.

## What is an IAM Role?

IAM Roles are used to control access to AWS services and resources.

For further details, take a look at the AWS-provided documentation:
[docs](http://aws.amazon.com/documentation/iam/).

Why it's useful: when you assign an IAM role to an EC2 instance,
credentials to access the instance are automatically provided by AWS.
This removes the need to store them, change and/or rotate
them, while also providing fine-grain controls over what actions can
be performed when using the credentials.

This particular plug-in makes use of the IAM credentials when accessing
S3 buckets backing a yum repository.

## How to set it up?

There is a great blog post by Jeremy Carroll which explains in depth how to
use this plugin:
[S3 Yum Repos With IAM Authorization](http://www.carrollops.com/blog/2012/09/11/s3-yum-repos-with-iam-authorization/).

## Notes on S3 buckets and URLs

There are 2 types of S3 URLs:
- virtual-hosted–style URL:
  - `https://<bucket>.s3.amazonaws.com/<path>` if region is US East (us-east-1)
  - `https://<bucket>.s3-<aws-region>.amazonaws.com/<path>` in other regions
- path-style URLs:
  - `https://s3.amazonaws.com/<bucket>/<path>` if region is US East (us-east-1)
  - `https://s3-<aws-region>.amazonaws.com/<bucket>/<path>` in other regions

When using HTTP/S and a bucket name containing a dot (`.`) you need to
use the path-style URL syntax.

## Limitations

Currently the plugin does not support:
- Proxy server configuration
- Multi-valued baseurl or mirrorlist

## Testing

Use `make test` to run some simple tests.

## License

Apache 2.0 license. See LICENSE.

## Maintainers

- Mathias Brossard
- Mischa Spiegelmock
- Sean Edge

## Author(s)

- Julius Seporaitis
- [Robert Melas' code](https://github.com/rmela/yum-s3-plugin/) was
  used as a reference. See NOTICE.
