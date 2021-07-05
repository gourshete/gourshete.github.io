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

| Canned ACL | Applies to | Permissions added to ACL |
| ----------- | ----------- | ----------- |
| private | Bucket and object | Owner gets FULL_CONTROL. No one else has access rights (default). |
| public-read	 | Bucket and object | Owner gets FULL_CONTROL. The AllUsers group gets READ access. |
| public-read-write | Bucket and object | Owner gets FULL_CONTROL. The AllUsers group gets READ and WRITE access. Granting this on a bucket is generally not recommended. |
| aws-exec-read | Bucket and object | Owner gets FULL_CONTROL. Amazon EC2 gets READ access to GET an Amazon Machine Image (AMI) bundle from Amazon S3. |
| authenticated-read | Bucket and object | Owner gets FULL_CONTROL. The AuthenticatedUsers group gets READ access. |
| bucket-owner-read | Object | Object owner gets FULL_CONTROL. Bucket owner gets READ access. If you specify this canned ACL when creating a bucket, Amazon S3 ignores it. |
| bucket-owner-full-control | Object | Both the object owner and the bucket owner get FULL_CONTROL over the object. If you specify this canned ACL when creating a bucket, Amazon S3 ignores it. |
| log-delivery-write | Bucket | The LogDelivery group gets WRITE and READ_ACP permissions on the bucket. |


<br>
*Note* - You can specify only one of these canned ACLs in your request.

---

References -

- <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html" target='_blank'>https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html</a>
