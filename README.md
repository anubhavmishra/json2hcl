# json2hcl

Convert JSON to HCL

## Usage

Download the latest version of `json2hcl` from [releases](https://github.com/anubhavmishra/json2hcl/releases).

### Packer JSON config file to HCL example

Packer JSON config file [examples/packer-config.json](./examples/packer-config.json)

```json
{
  "variables": {
    "aws_access_key": "",
    "aws_secret_key": ""
  },
  "builders": [{
    "type": "amazon-ebs",
    "access_key": "{{user `aws_access_key`}}",
    "secret_key": "{{user `aws_secret_key`}}",
    "region": "us-east-1",
    "source_ami_filter": {
      "filters": {
        "virtualization-type": "hvm",
        "name": "ubuntu/images/*ubuntu-xenial-16.04-amd64-server-*",
        "root-device-type": "ebs"
      },
      "owners": ["099720109477"],
      "most_recent": true
    },
    "instance_type": "t2.micro",
    "ssh_username": "ubuntu",
    "ami_name": "packer-example {{timestamp}}"
  }]
}
```

Convert Packer JSON config file to HCL

```bash
json2hcl < examples/packer-config.json
"variables" = {
  "aws_access_key" = ""

  "aws_secret_key" = ""
}

"builders" = {
  "type" = "amazon-ebs"

  "access_key" = "{{user `aws_access_key`}}"

  "secret_key" = "{{user `aws_secret_key`}}"

  "region" = "us-east-1"

  "source_ami_filter" = {
    "filters" = {
      "virtualization-type" = "hvm"

      "name" = "ubuntu/images/*ubuntu-xenial-16.04-amd64-server-*"

      "root-device-type" = "ebs"
    }

    "owners" = ["099720109477"]

    "most_recent" = true
  }

  "instance_type" = "t2.micro"

  "ssh_username" = "ubuntu"

  "ami_name" = "packer-example {{timestamp}}"
}
```

## Acknowledgements

This project is inspired by [kvz/json2hcl](https://github.com/kvz/json2hcl). This project aims to be
lightweight and only support JSON to HCL conversion. If you want to convert HCL to JSON, please use
[kvz/json2hcl](https://github.com/kvz/json2hcl).
