+++
title = "Introduction"
weight = 10
teaching = 10
exercises = 5
questions = ["Who is this workflow for?", "What does the workflow simulate?", "How does the workflow work?"]
objectives = ["Understand if this is a worfklow you can use.", "Understand what the workflow does.", ""]
keypoints = ["Those with access to CERN resources can use the workflow to data simulation.", "The workflow simulates the CMS Monte Carlo steps.", "Snakemake maps out the workflow while REANA runs the simulation."]
+++

## Is the Workflow for You?

This workflow was made so that users with access to CERN's REANA cluster can utilize its computing backends to simulate their own collision dataset or attempt to reproduce and existing dataset. The tutorial will walk you through the steps of using the workflow to simulate the dataset you need.

Only continue if you have set up the evironment needed for the tutorial. If not then go back to [Setup]({{< relref "/learners/setup.md" >}}).

## Workflow Steps

The workflow implements the [CMS Monte Carlo](https://opendata.cern.ch/docs/cms-mc-production-overview) steps, which follow the progression of generation (GEN), simulation (SIM) which includes the digi2raw, hlt and pat steps, and finally the reconstruction (RECO) and NANO steps.

![CMS Monte Carlo Prodcution Overview](fig/CMS_Monte_Carlo_Overview.png)

Each step of the workflow requires its own environment for processing. Which is why the workflow parses the CMSSW environment of the step from its metadata utilizing releases and tags specific to the dataset. You can find the implementation on [Github](https://github.com/cms-opendata-processing-tasks/FullSimulationReanaWorkflow).


## Tools 

The workflow utilizes [Snakemake](https://snakemake.readthedocs.io/en/stable/) as the tool that maps out the workflow,
with defined rules showing each steps input and output requirements. It then builds a Directed Acyclic Graph (DAG) of the jobs to have the workflow planned out and then that plan is sent to REANA.

REANA recieves the workflow plan and assign jobs to the available cluster nodes, while keeping the order specified by the DAG.