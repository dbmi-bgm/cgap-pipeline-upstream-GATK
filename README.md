<img src="https://github.com/dbmi-bgm/cgap-pipeline/blob/master/docs/images/cgap_logo.png" width="200" align="right">

# CGAP Upstream Pipeline - GATK

This repository contains components for the CGAP upstream pipeline using GATK (Genome Analysis Toolkit):

  * CWL workflow descriptions
  * CGAP Portal *Workflow* and *MetaWorkflow* objects
  * CGAP Portal *Software*, *FileFormat*, and *FileReference* objects
  * ECR (Docker) source files, which allow for creation of public Docker images (using `docker build`) or private dynamically-generated ECR images (using [*cgap pipeline utils*](https://github.com/dbmi-bgm/cgap-pipeline-utils/) `pipeline_deploy`)

The pipeline can process paired-end `fastq` files up to analysis-ready `bam` files.
Documentation for all CGAP Pipelines can now be found here:
https://cgap-pipeline-main.readthedocs.io/en/latest/
