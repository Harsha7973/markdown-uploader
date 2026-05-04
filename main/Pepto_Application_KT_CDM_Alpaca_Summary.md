Source tag : 
      
Note : This extracted file is generated from SharePoint or Wiki content. If the source document contains images, charts, or graphical elements, they may not be fully converted into Markdown format. For complete clarity, please refer to the original source using the source tag provided above.

# Pepto – CDM & Alpaca Cache Populator KT

## Overview

This KT explains the combined CDM and Alpaca pipelines that populate ElasticCache for Pepto applications.

## Pipelines Covered

- Alpaca Cache Populator
- CDM Cache Populator
- Common Lambda and Redis architecture

## Data Flow

1. Source data arrives in S3 (Alpaca/CDM).
2. Databricks processes data.
3. Processed output written to consent S3 bucket.
4. S3 triggers Lambda per partition.
5. Lambda compresses and stores data in Redis.

## Cache Populator Notebook

- Single notebook handles both CDM and Alpaca.
- Filters, groups, and formats data.
- Writes partitioned output to consent bucket.

## Cluster Configuration

- Defined in Pepto Job Config repo.
- Includes Spark version, worker count, executor size.
- Feature branch or main branch must match notebook branch.

## Deployment Repositories

- Notebook repo (code)
- Job config repo (cluster)
- Deployer repo (Databricks workspace + tokens)

## Deployment Steps

1. Make code changes in notebook.
2. Update cluster config if needed.
3. Update deploy config references.
4. Run Azure DevOps pipeline manually.
5. Verify updates in Databricks job UI.

## Monitoring & Debugging

- CloudWatch logs for Lambda.
- Redis metrics (CPU, memory).
- Databricks job run status.

## Outcome

This KT provides a complete picture of how CDM and Alpaca pipelines feed ElasticCache reliably and how engineers should deploy, monitor, and debug them.
