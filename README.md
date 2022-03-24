<img src="https://github.com/dbmi-bgm/cgap-pipeline/blob/master/docs/images/cgap_logo.png" width="200" align="right">

# CGAP Upstream Pipeline - GATK

This repository contains components for the CGAP upstream pipeline using GATK (Genome Analysis Toolkit):

  * CWL workflows
  * CGAP Portal Workflows and MetaWorkflows objects
  * ECR (Docker) source files, which allow for creation of public Docker images (using `docker build`) or private dynamically-generated ECR images (using [*cgap pipeline utils*](https://github.com/dbmi-bgm/cgap-pipeline-utils/) `deploy_pipeline`)

The pipeline can process paired `fastq` files up to analysis ready `bam` files.
For more details check the [*documentation*](https://cgap-pipeline-main.readthedocs.io/en/latest/Pipelines/Upstream/upstream_GATK/index-upstream_GATK.html "upstream pipeline GATK").

### Version Updates

#### v1.0.0
* v27 -> v1.0.0, we are starting a new more comprehensive versioning system
* Added some change in metaworkflows to accomodate the changes in foursight
* Updated GATK version to fix vulnerability

#### v27
* This repo starts from the v26 release of [*cgap-pipeline*](https://github.com/dbmi-bgm/cgap-pipeline) and contains the first half of the original pipeline (starting from `fastq` files and producing `bam` files)
* Changes in repo structure to allow for compatibility with new pipeline organization
