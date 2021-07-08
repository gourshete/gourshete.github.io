---
layout: post
title:  "Understanding Amazon S3 ACLs"
date:   2021-06-28
keywords: "ruby rails aws acl learning swapnil gourshete ruby on rails"
image: assets/images/aws-icon.png
categories: [ AWS ]
---

The AWS provides built in options for fine grain control over s3 objects and buckets. One of them is ACL - Access Control List.

In this post we will try to understand different types of ACL options with their permissions provided by AWS.

From AWS Docs -

*Amazon S3 access control lists (ACLs) enable you to manage access to buckets and objects. Each bucket and object has an 
ACL attached to it as a subresource. It defines which AWS accounts or groups are granted access and the type of access. 
When a request is received against a resource, Amazon S3 checks the corresponding ACL to verify that the requester has 
the necessary access permissions.*

You can grant **read**, **write** and **full-control** permissions using ACL. They can be applied on bucket and/or object.
When granted on bucket, the permissions are scoped to bucket. When granted on object, they are scoped to objects. All of these
permissions can be applied on both bucket & objects except write. It is not applicable to objects.

<h4>Mapping of ACL permissions and access policy permissions</h4>

ACL allows only a finite set of permissions, compared to the number of permissions you can set in an access policy. Each
of these permissions allows one or more Amazon S3 operations.

<h3>Canned ACL</h3> 

Canned ACLs are predefined grants provided by S3. In most of the use cases these canned ACL will suit in. Each canned ACL
has predefined set of grantees and permissions as shown in table below -

- `private`: owner gets full control. No one else has access rights.
- `public-read`: owner gets full control. The AllUsers group gets read access
- `public-read-write`: owner gets full control. The AllUsers group gets read and write access. Granting this on a bucket is generally not recommended.
- `aws-exec-read`: owner gets full control. Amazon EC2 gets read access to GET an Amazon Machine Image &#40;AMI&#41; bundle from Amazon S3.
- `authenticated-read`: owner gets full control. The AuthenticatedUsers group gets read access.
- `bucket-owner-read`: object owner gets full control. Bucket owner gets read access. If you specify this canned ACL when creating a bucket, Amazon S3 ignores it.
- `bucket-owner-full-control`: both the object owner and the bucket owner get full control over the object. If you specify this canned ACL when creating a bucket, Amazon S3 ignores it.
- `log-delivery-write`: the LogDelivery group gets write and read_acp permissions on the bucket.

<br>
*Note* - You can specify only one of these canned ACLs in your request.

---

References -

- <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html" target='_blank'>https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html</a>
