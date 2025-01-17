# Introduction
This repository is used to test a local Confluent Platform cluster integrating with a Confluent Cloud cluster. It was used as the basis of a demonstration during the Confluent Cloud workshop, and is provided for participants to try out the scripted process.

This repo demonstrates a fully scripted event streaming system that spans on-prem and fully-managed on cloud. Most of the setup commands use the "ccloud" cli - the Confluent Cloud CLI. The "start-aws" (and similar) scripts in this demo assume you have download and unpacked Confluent Platform on your laptop https://www.confluent.io/download. Alternatively use examples-5.5.1-post/ccloud/start-docker.sh to start the Dockerized version of this demo.

This more advanced demo showcases an on-prem Kafka cluster and [Confluent Cloud](https://www.confluent.io/confluent-cloud/?utm_source=github&utm_medium=demo&utm_campaign=ch.examples_type.community_content.top) cluster, and data copied between them with Confluent Replicator <br><img src="examples-5.5.1-post/ccloud/docs/images/services-in-cloud.jpg" width="450">

The completed script will:

* Create a new service account on Confluent Cloud
* Generate a local configuration file to use the service account
* Create a new environment on Confluent Cloud
* Create a new managed cluster on Confluent Cloud
* Create a new ksqlDB service on Confluent Cloud
* Start a local Confluent Platform cluster
* Start a local Confluent Control Centre attached to Confluent Cloud and local Confluent Platform
* Create topics in the local cluster
* Create a data generator in the local Confluent Platform for users and pageviews
* Start a local Connect cluster that connects to Confluent Cloud
* Create ACLs to secure the Confluent Cloud cluster
* Start replicator to move date from the local Confluent Platform to Confluent Cloud
* Create a ksqlDB streaming application in Confluent Cloud

# Before you start
This script will setup a cluster on Confluent Cloud. This account will be **incurring costs**, so don't leave the account up and running longer than required.

If you want to try out Confluent Cloud you can receive $200 credit per month for three months by visting https://www.confluent.io/confluent-cloud/ and clicking the "Try Free" button.

Also note that this repository is designed to demonstrate approaches to scriptable depoyments suitable for CI/CD pipelines, but you may need to adapt to your specific use cases.

Additionally, the script uses your Confluent Cloud username and password, which is simple for the demonstration, but **not suitable for being shared across a team**. Use API keys and service accounts if you plan on operationalising these scripts.

# Pre-requisites
1. Install Confluent Cloud CLI
   * Darwin/x64 - https://s3-us-west-2.amazonaws.com/confluent.cloud/ccloud-cli/archives/1.7.0/ccloud_v1.7.0_darwin_amd64.tar.gz 
   * Windows/x64 - https://s3-us-west-2.amazonaws.com/confluent.cloud/ccloud-cli/archives/1.7.0/ccloud_v1.7.0_windows_amd64.zip
   * Linux/x64 - https://s3-us-west-2.amazonaws.com/confluent.cloud/ccloud-cli/archives/1.7.0/ccloud_v1.7.0_linux_amd64.tar.gz
   * Linux/386 - https://s3-us-west-2.amazonaws.com/confluent.cloud/ccloud-cli/archives/1.7.0/ccloud_v1.7.0_linux_386.tar.gz
2. Install Confluent Platform
   * zip - curl -O http://packages.confluent.io/archive/5.5/confluent-5.5.1-2.12.zip
   * tar - curl -O curl -O http://packages.confluent.io/archive/5.5/confluent-5.5.1-2.12.tar.gz
   * Follow instructions on - https://docs.confluent.io/5.5.1/quickstart/ce-quickstart.html#ce-quickstart
3. Install jq
4. Have a Confluent Cloud account in place

# Getting started
1. Clone the repository
2. Copy `.ccworkshop.default` to `.ccworkshop`. 
3. Replace the `<USER_EMAIL>` and `<PASSWORD>` fields in the `.ccworkshop` file with your Confluent Cloud credentials. This file will be ignored by git.
4. Run the script appropriate to your choice of cloud provider. Eg: `./runme-aws`

# Destroying the cluster
1. Navigate to confluentcloud_workshop/examples-5.5.1-post/ccloud
2. Run the `stop.sh` command which you would see at the end of `runme` command

# Going further
Confluent have a large number of examples available online. Visit https://github.com/confluentinc/examples
