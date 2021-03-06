---
layout: "aws"
page_title: "AWS: aws_elasticache_replication_group"
sidebar_current: "docs-aws-resource-elasticache-replication-group"
description: |-
  Provides an ElastiCache Replication Group resource.
---

# aws\_elasticache\_replication\_group

Provides an ElastiCache Replication Group resource.

~> **Note:** We currently do not support passing a `primary_cluster_id` in order to create the Replication Group.

## Example Usage

```
resource "aws_elasticache_replication_group" "bar" {
  replication_group_id          = "tf-replication-group-1"
  replication_group_description = "test description"
  node_type                     = "cache.m1.small"
  number_cache_clusters         = 2
  port                          = 6379
  parameter_group_name          = "default.redis2.8"
  availability_zones            = ["us-west-2a", "us-west-2b"]
  automatic_failover_enabled    = true
}
```

## Argument Reference

The following arguments are supported:

* `replication_group_id` – (Required) The replication group identifier. This parameter is stored as a lowercase string.
* `replication_group_description` – (Required) A user-created description for the replication group.
* `number_cache_clusters` - (Required) The number of cache clusters this replication group will have.
 If Multi-AZ is enabled , the value of this parameter must be at least 2. Changing this number will force a new resource
* `node_type` - (Required) The compute and memory capacity of the nodes in the node group.
* `automatic_failover_enabled` - (Optional) Specifies whether a read-only replica will be automatically promoted to read/write primary if the existing primary fails. Defaults to `false`.
* `availability_zones` - (Optional) A list of EC2 availability zones in which the replication group's cache clusters will be created. The order of the availability zones in the list is not important.
* `engine_version` - (Optional) The version number of the cache engine to be used for the cache clusters in this replication group.
* `parameter_group_name` - (Optional) The name of the parameter group to associate with this replication group. If this argument is omitted, the default cache parameter group for the specified engine is used.
* `subnet_group_name` - (Optional) The name of the cache subnet group to be used for the replication group.
* `security_group_names` - (Optional) A list of cache security group names to associate with this replication group.
* `security_group_ids` - (Optional) One or more Amazon VPC security groups associated with this replication group. Use this parameter only when you are creating a replication group in an Amazon Virtual Private Cloud 
* `snapshot_arns` – (Optional) A single-element string list containing an
Amazon Resource Name (ARN) of a Redis RDB snapshot file stored in Amazon S3.
Example: `arn:aws:s3:::my_bucket/snapshot1.rdb`
* `snapshot_name` - (Optional) The name of a snapshot from which to restore data into the new node group. Changing the `snapshot_name` forces a new resource. 
* `maintenance_window` – (Optional) Specifies the weekly time range for when maintenance
on the cache cluster is performed. The format is `ddd:hh24:mi-ddd:hh24:mi` (24H Clock UTC).
The minimum maintenance window is a 60 minute period. Example: `sun:05:00-sun:09:00`
* `notification_topic_arn` – (Optional) An Amazon Resource Name (ARN) of an
SNS topic to send ElastiCache notifications to. Example:
`arn:aws:sns:us-east-1:012345678999:my_sns_topic`
* `snapshot_window` - (Optional, Redis only) The daily time range (in UTC) during which ElastiCache will
begin taking a daily snapshot of your cache cluster. Example: 05:00-09:00
* `snapshot_retention_limit` - (Optional, Redis only) The number of days for which ElastiCache will
retain automatic cache cluster snapshots before deleting them. For example, if you set
SnapshotRetentionLimit to 5, then a snapshot that was taken today will be retained for 5 days
before being deleted. If the value of SnapshotRetentionLimit is set to zero (0), backups are turned off.
Please note that setting a `snapshot_retention_limit` is not supported on cache.t1.micro or cache.t2.* cache nodes
* `apply_immediately` - (Optional) Specifies whether any modifications are applied immediately, or during the next maintenance window. Default is `false`. 
* `tags` - (Optional) A mapping of tags to assign to the resource

## Attributes Reference

The following attributes are exported:

* `id` - The ID of the ElastiCache Replication Group
* `primary_endpoint_address` - The address of the endpoint for the primary node in the replication group