+++
title = "aws_rds_snapshots Resource"
platform = "aws"
draft = false
gh_repo = "inspec-aws"

[menu.inspec]
title = "aws_rds_snapshots"
identifier = "inspec/resources/aws/aws_rds_snapshots Resource"
parent = "inspec/resources/aws"
+++

Use the `aws_rds_snapshots` InSpec audit resource to test the properties of a collection of AWS RDS snapshots.

## Installation

{{% inspec_aws_install %}}

## Syntax

 Ensure you have three snapshots.

```ruby
describe aws_rds_snapshots do
  its('db_snapshot_identifiers.count') { should cmp 3 }
end
```

## Parameters

This resource does not expect any parameters.

See also the [AWS documentation on RDS](https://docs.aws.amazon.com/rds/?id=docs_gateway).

## Properties

`db_snapshot_identifiers`
: The unique IDs of the RDS snapshots returned.

`entries`
: Provides access to the raw results of the query, which can be treated as an array of hashes.

## Examples

**Ensure a specific snapshot exists.**

```ruby
describe aws_rds_snapshots do
  its('db_snapshot_identifiers') { should include 'RDS-12345678' }
end
```

**Requests the IDs of RDS snapshots and ensures the snapshots are encrypted with sensible size.**

```ruby
aws_rds_snapshots.db_snapshot_identifiers.each do |db_snapshot_identifier|
  describe aws_rds_snapshot(db_snapshot_identifier) do
    it { should be_encrypted }
  end
end
```

## Matchers

For a full list of available matchers, please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

The control will pass if the describe returns at least one result.

Use `should_not` to test the entity should not exist.

```ruby
describe aws_rds_snapshots do
  it { should exist }
end
```

```ruby
describe aws_rds_snapshots do
  it { should_not exist }
end
```

## AWS Permissions

{{% aws_permissions_principal action="RDS:Client:DBSnapshotMessage" %}}

You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon EC2](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonec2.html), and [Actions, Resources, and Condition Keys for Identity And Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_identityandaccessmanagement.html).
