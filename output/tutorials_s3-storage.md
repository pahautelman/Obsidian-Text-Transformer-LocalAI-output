# Switching to S3 Storage

## Key Concepts
- Community contribution tutorial
- Switching storage from local to Amazon S3
- Prerequisites for setup (AWS account, Docker)
- Required environment variables
- Running Open WebUI with S3 storage
- Testing the S3 integration

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/s3-storage](https://docs.openwebui.com/tutorials/s3-storage)

### Overview
This tutorial guides you through switching the default local storage in Open WebUI to Amazon S3. It is a community-contributed guide and not officially supported by the Open WebUI team.

### Prerequisites

Before starting, ensure you have the following:

- **AWS Account:** An active AWS account.
- **AWS Credentials:** Active AWS Access Key and Secret Key.
- **IAM Permissions:** Necessary permissions to create and put objects in S3.
- **Docker:** Installed on your system.

### What is Amazon S3?

Amazon S3 (Simple Storage Service) is an object storage service provided by AWS. It offers:

- Industry-leading scalability
- High data availability
- Robust security
- Excellent performance

S3 is designed for 99.999999999% durability and is used globally for various applications, including data lakes, websites, backups, machine learning, and analytics.

For more information, visit the [Amazon S3 Official Page](https://aws.amazon.com/s3/).

### Required Environment Variables

To configure Open WebUI to use Amazon S3, you need the following environment variables:

- **S3_ACCESS_KEY_ID:** Identifier for your AWS account's access key.
- **S3_SECRET_ACCESS_KEY:** Secret part of your AWS access key pair.
- **S3_ENDPOINT_URL:** URL directing to your S3 service endpoint.
- **S3_REGION_NAME:** AWS region where your S3 bucket resides (e.g., "us-east-1").
- **S3_BUCKET_NAME:** Unique name of your S3 bucket.

For a complete list of available S3 endpoint URLs, see [Amazon S3 Regular Endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html).

### Running Open WebUI with S3 Storage

Before launching Open WebUI, set the `STORAGE_PROVIDER` environment variable to "s3". This tells Open WebUI to use Amazon S3 for storage.

Here is an example Docker command to run Open WebUI with S3:

```bash
docker run -d \
  -p 3000:8080 \
  -v open-webui:/app/backend/data \
  -e STORAGE_PROVIDER="s3" \
  -e S3_ACCESS_KEY_ID="ABC123" \
  -e S3_SECRET_ACCESS_KEY="SuperSecret" \
  -e S3_ENDPOINT_URL="https://s3.us-east-1.amazonaws.com" \
  -e S3_REGION_NAME="us-east-1" \
  -e S3_BUCKET_NAME="my-awesome-bucket-name" \
  -e ENV="dev" \
  --name open-webui \
  ghcr.io/open-webui/open-webui:main
```

### Testing the Setup

To verify that Open WebUI is correctly configured to use Amazon S3:

1. **Upload a File:** Upload a simple text file (e.g., "Hello, World").
2. **Verify Storage:** Check the AWS Management Console to ensure the file is stored in your specified S3 bucket.
3. **Inspect File:** Use Open WebUI's Swagger docs and the `/api/v1/files/{id}` endpoint to retrieve information about the uploaded file.

## Summary
This tutorial walks you through switching Open WebUI from local storage to Amazon S3, including setting up necessary environment variables and verifying the integration. By following these steps, you can leverage the scalability and durability of Amazon S3 for your storage needs.

# Tags
#s3 #storage #tutorial #aws #docker