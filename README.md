# s3-acl-viewer by TrackIt

Report AWS S3's permissions to CSV, Excel and Google Spreadsheet.

## What does it do?
- Checks all your buckets for public access
- Generates a report via
  - Standard output
  - Comma-separated values (.csv)
  - Microsoft Excel (.xlsx)
  - Google Spreadsheet

## Requirements

### Create a new IAM User
 - **Create IAM user with AmazonS3ReadOnly policy attached**
   - Go to IAM (https://console.aws.amazon.com/iam/home)
   - Click "Users" on the left hand side menu
   - Click "Add user"
   - Fill in user name and check **Programmatic access**
   - Click "Next: Permissions"
   - Click "Attach existing policies directly"
   - Check **AmazonS3ReadOnly** policy
   - Click "Next: Review"
   - Click "Create user"
   - **Copy the credentials**
     - **Access key ID**
     - **Secret access key**
 - **Create ~/.aws/credentials file or paste the credentials in when you run the script**
   - Put the credentials you copied in the previous step here in this format:
```
[default]
aws_access_key_id = <your access key ID goes here>
aws_secret_access_key = <your secret_access_key goes here>
```
### Use existing configured IAM User
 - **use your existing credentials or profile** if you have a file `~/.aws/credentials` like this:
```
[default]
aws_access_key_id = <your access key ID goes here>
aws_secret_access_key = <your secret_access_key goes here>
[my_profile_name]
aws_access_key_id = <your access key ID goes here>
aws_secret_access_key = <your secret_access_key goes here>
```
 - and pass the profile name in argument (`default` if nothing):
```
$> ./s3-acl-viewer -p my_profile_name
```

### Configure the Google Spreadsheet report

Follow the first step of the instructions at https://developers.google.com/sheets/api/quickstart/python to setup credentials and API access.

## Installation

```
$> git clone git@github.com:trackit/s3-acl-viewer.git
$> cd s3-acl-viewer
$> pip3 install -r requirement.txt
```

## Usage
```
$> ./s3-acl-viewer -h
usage: s3-acl-viewer [-h] [--auth_host_name AUTH_HOST_NAME]
              [--noauth_local_webserver]
              [--auth_host_port [AUTH_HOST_PORT [AUTH_HOST_PORT ...]]]
              [--logging_level {DEBUG,INFO,WARNING,ERROR,CRITICAL}]
              [-p [PROFILE [PROFILE ...]]] [-n NAME] [-g] [-x] [-c] [-s]

optional arguments:
  -h, --help            show this help message and exit
  --auth_host_name AUTH_HOST_NAME
                        Hostname when running a local web server.
  --noauth_local_webserver
                        Do not run a local web server.
  --auth_host_port [AUTH_HOST_PORT [AUTH_HOST_PORT ...]]
                        Port web server should listen on.
  --logging_level {DEBUG,INFO,WARNING,ERROR,CRITICAL}
                        Set the logging level of detail.
  -p [PROFILE [PROFILE ...]], --profile [PROFILE [PROFILE ...]]
                        aws profiles. [default] by default.
  -n NAME, --name NAME  spreadsheet name. [s3_report] by default.
  -g, --gspread         create a google spreadsheet.
  -x, --xlsx            create a xlsx spreadsheet.
  -c, --csv             create a csv file.
  -s, --silent          disable printing.
```

***Note:** Arguments `--auth_host_name`, `-noauth_local_webserver`, `--auth_host_port` and `--loging_level` are generated by the Google Spreadsheet implementation.*


## Example

```
$> ./s3-acl-viewer -p my_profile_1 my_profile_2 -xgc
```

### Output
![print-example](https://s3-us-west-2.amazonaws.com/trackit-public-artifacts/s3-acl-viewer/print-example.png)

### Generated '.csv' file
![csv-example](https://s3-us-west-2.amazonaws.com/trackit-public-artifacts/s3-acl-viewer/csv-example.png)

### Generated auto-uploaded Google Spreadsheet
![gspread-example](https://s3-us-west-2.amazonaws.com/trackit-public-artifacts/s3-acl-viewer/gspread-example.png)

### Generated '.xlsx' file (Microsoft Excel)
![xlsx-example](https://s3-us-west-2.amazonaws.com/trackit-public-artifacts/s3-acl-viewer/xlsx-example.png)

