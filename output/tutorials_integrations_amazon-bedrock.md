# Integrate with Amazon Bedrock

## Key Concepts
- Community contribution tutorial
- Integration of Open WebUI with Amazon Bedrock
- Prerequisites for integration (AWS account, Docker)
- Overview of Amazon Bedrock
- Steps to integrate:
  - Verify access to base models
  - Configure the Bedrock Access Gateway
  - Add connection in Open-WebUI
  - Start using Bedrock Base Models

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/amazon-bedrock](https://docs.openwebui.com/tutorials/integrations/amazon-bedrock)

### Overview
This tutorial, contributed by the community, demonstrates how to integrate Open WebUI with Amazon Bedrock. It is not officially supported by the Open WebUI team but serves as a valuable guide for customizing Open WebUI for specific use cases.

### Prerequisites

Before starting, ensure you have the following:
- An active AWS account
- Active AWS Access Key and Secret Key
- IAM permissions in AWS to enable Bedrock models or already enabled models
- Docker installed on your system

### What is Amazon Bedrock?

Amazon Bedrock is a fully managed service offering high-performing foundation models (FMs) from leading AI companies. It provides capabilities for building generative AI applications with security, privacy, and responsible AI practices.

Key features include:
- Experimenting with top FMs
- Customizing models with techniques like fine-tuning and Retrieval Augmented Generation (RAG)
- Building agents that execute tasks using enterprise systems and data sources

For more information, visit the [Amazon Bedrock's Official Page](https://aws.amazon.com/bedrock).

### Step-by-Step Integration

#### Step 1: Verify Access to Amazon Bedrock Base Models
Before integrating with Bedrock, verify access to at least one base model. At the time of writing (Feb 2025), there were 47 available models.

- **Access Verification:**
  - Ensure you have "✅ Access Granted" next to the models.
  - Refer to [Amazon Bedrock's Model Access Docs](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html) for enabling models.

#### Step 2: Configure the Bedrock Access Gateway (BAG)
The BAG acts as a proxy, exposing endpoints compatible with OpenAI's schema required by Open-WebUI.

**Setup Steps:**
1. Clone the [Bedrock Access Gateway Repo](https://github.com/your-repo/bag).
2. Remove the default Dockerfile.
3. Rename `Dockerfile_ecs` to `Dockerfile`.
4. Build and launch the Docker container:
   ```bash
   docker build . -f Dockerfile -t bedrock-gateway
   docker run -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY="$AWS_SECRET_ACCESS_KEY" -e AWS_REGION=us-east-1 -d -p 8000:80 bedrock-gateway
   ```
5. Access the BAG's Swagger page at [http://localhost:8000/docs](http://localhost:8000/docs).

#### Step 3: Add Connection in Open-WebUI
1. Go to **Admin Panel** > **Settings** > **Connections**.
2. Use the "+" button to add a new connection under **OpenAI**.
3. Set the URL to `http://host.docker.internal:8000/api/v1`.
4. Use the default password "bedrock".
5. Click **"Verify Connection"** and ensure you see the "Server connection verified" alert.

#### Step 4: Start Using Bedrock Base Models
You should now see all your Bedrock models available in Open-WebUI.

### Other Helpful Tutorials

For further assistance, refer to these tutorials:
- [Connecting Open WebUI to AWS Bedrock](https://gauravve.medium.com/connecting-open-webui-to-aws-bedrock-a1f0082c8cb2)
- [Using Amazon Bedrock with OpenWebUI for Sensitive Data](https://jrpospos.blog/posts/2024/08/using-amazon-bedrock-with-openwebui-when-working-with-sensitive-data/)

## Summary
This tutorial guides users through integrating Open WebUI with Amazon Bedrock, covering prerequisites, setup steps, and configuration details. It emphasizes the importance of verifying access to base models and configuring the Bedrock Access Gateway for seamless integration.

# Tags
#integration #amazonbedrock #openwebui #tutorial #aws