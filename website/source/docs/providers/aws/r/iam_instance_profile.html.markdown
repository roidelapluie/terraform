---
layout: "aws"
page_title: "AWS: aws_iam_instance_profile"
sidebar_current: "docs-aws-resource-iam-instance-profile"
description: |-
  Provides an IAM instance profile.
---

# aws\_iam\_instance\_profile

Provides an IAM instance profile.

~> **NOTE:** Either `roles` or `role` must be specified in the IAM Instance Profile.

## Example Usage

```hcl
resource "aws_iam_instance_profile" "test_profile" {
  name  = "test_profile"
  role = "${aws_iam_role.role.name}"
}

resource "aws_iam_role" "role" {
  name = "test_role"
  path = "/"

  assume_role_policy = <<EOF
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": "sts:AssumeRole",
            "Principal": {
               "Service": "ec2.amazonaws.com"
            },
            "Effect": "Allow",
            "Sid": ""
        }
    ]
}
EOF
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Optional, Forces new resource) The profile's name. If omitted, Terraform will assign a random, unique name.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`.
* `path` - (Optional, default "/") Path in which to create the profile.
* `roles` - (Optional) A list of role names to include in the profile.  The current default is 1.  If you see an error message similar to `Cannot exceed quota for InstanceSessionsPerInstanceProfile: 1`, then you must contact AWS support and ask for a limit increase. `WARNING: This will be deprecated in a future version of Terraform`.
* `role` - (Optional) The role name to include in the profile.

## Attribute Reference

* `id` - The instance profile's ID.
* `arn` - The ARN assigned by AWS to the instance profile.
* `create_date` - The creation timestamp of the instance profile.
* `name` - The instance profile's name.
* `path` - The path of the instance profile in IAM.
* `roles` - The list of roles assigned to the instance profile.
* `role` - The role assigned to the instance profile
* `unique_id` - The [unique ID][1] assigned by AWS.

  [1]: https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_Identifiers.html#GUIDs


## Import

Instance Profiles can be imported using the `name`, e.g.

```
$ terraform import aws_iam_instance_profile.test_profile app-instance-profile-1
```
