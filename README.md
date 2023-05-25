# NorthSec CTF 2023 AWS Track
This projet contains the necessary files to deploy the AWS track named "Annual Review" from the NorthSec CTF 2023 developed by [@marcan2020](https://twitter.com/marcan2020) and [@simondotsh](https://twitter.com/simondotsh).

## Requirements
* An AWS account
* A web server to serve files and retrieve information from access logs such as credentials sent by a Lambda function during provisioning.

## Deploying
1. Host the [track source code](provisioning/ba7a69b978e62108b77ac3b0c92d547c2eb923d3.zip) at the root of a web server. Ensure you can read access logs.
2. Using the AWS CloudFormation service, create a stack using the [template](provisioning/template.yaml).
3. When requested, fill the `ProvisioningUrl` parameter with the URL of your web server, e.g. `http://44.209.164.138`.
4. Once created, wait 5 to 10 minutes for the resources to be available.
5. In your web server's access logs, you should see the following:
```
44.213.65.17 - - [24/May/2023:20:41:25 -0400] "GET /ba7a69b978e62108b77ac3b0c92d547c2eb923d3.zip HTTP/1.1" 200 14419320 "-" "Python-urllib/3.9"
44.202.66.80 - - [24/May/2023:20:43:30 -0400] "GET /nsec_aws?raw=588100578632,44.214.5.185,vlMfvX0w5ZqRrs6k92dz HTTP/1.1" 404 162 "-" "Python-urllib/3.9"
```

The last line contains the information `Account_ID,IP,Password`. You will need the IP and the password to access the challenge.

## Accessing the Track
* URL: `http://$IP:8080/employee-review/`
* Username: `120875ABAB`
* Password: the one noted from the previous step

Note that the web server may take 5 minutes to be available due to installing updates on the EC2 after you have received the information on your web server.

## Flags
See [flags](flags/flags.md) for the list of flags and return strings.

## Walkthrough
See [walkthrough](walkthrough/walkthrough.md).

## License
See the LICENSE file for legal wording. Essentially it is MIT, meaning that we cannot be held responsible for whatever results from using this code, and do not offer any warranty. By agreeing to this, you are free to use and do anything you like with the code.
