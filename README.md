# aws-all

`aws-all` is a command that allows you to execute AWS CLI commands across multiple AWS profiles and regions.

## Description

`aws-all` iterates over a list of AWS profiles and regions, executing a specified AWS CLI command in each combination. The output is structured in a JSON or text format.

### Output Example

For JSON output:

```
{
  "region": "us-east-1",
  "profile": "master",
  "output": []
}
```

For text output:

```
Region: us-east-1
Profile: master
Output: 
---
```

## Usage

### Using Command-line Arguments

```
aws-all --profiles "profile1 profile2" --regions "us-east-1 us-east-2" -- <aws-cli-command>
```

Replace `<aws-cli-command>` with the AWS CLI command you want to execute.

Example:

```
aws-all --profiles "profile1 profile2" --regions "us-east-1 ap-northeast-1" -- ec2 describe-availability-zones --query 'AvailabilityZones[].ZoneName'
{
  "region": "us-east-1",
  "profile": "profile1",
  "output": [
    "us-east-1a",
    "us-east-1b",
    "us-east-1c",
    "us-east-1d",
    "us-east-1e",
    "us-east-1f"
  ]
}
{
  "region": "ap-northeast-1",
  "profile": "profile1",
  "output": [
    "ap-northeast-1a",
    "ap-northeast-1c",
    "ap-northeast-1d"
  ]
}
...
```

### Using Environment Variables

You can specify profiles and regions using environment variables.

```
export AWS_PROFILES="profile1 profile2"
export AWS_REGIONS="us-east-1 us-east-2"

aws-all -- <aws-cli-command>
```

### Output format

You can specify the output format using the `--output` option. The available formats are `json` and `text`. By default, the output format is `json`.

## Installation

1. Download the `aws-all` command to your local machine.


2. Make the command executable:

```
chmod +x aws-all
```

3. Move the script to a directory in your PATH:

```
mv aws-all /usr/local/bin
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
