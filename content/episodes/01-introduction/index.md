+++
title = "Introduction"
weight = 10
teaching = 10
exercises = 5
questions = ["What should a modern lesson template preserve from the old Carpentries stack?"]
objectives = ["Identify the teaching features that matter more than the old implementation details.", "Recognise which pieces should live in a shared module versus in a lesson repository."]
keypoints = ["Preserve pedagogy and author ergonomics, not the historical implementation.", "A thin lesson repo plus a shared module gives a much cleaner update path."]
+++

This workflow was made so that users with access to CERN's REANA cluster can utilize its computing backends to simulate their own collision dataset. The tutorial will walk you through the steps of using the workflow to simulate the dataset you need.

## Workflow Steps

The workflow implements the [CMS Monte Carlo](https://opendata.cern.ch/docs/cms-mc-production-overview) steps, which follow the progression of generation (GEN), simulation (SIM) which includes the digi2raw, hlt and pat steps, and finally the reconstruction (RECO) and NANO steps.

![CMS Monte Carlo Prodcution Overview](/static/fig/CMS_Monte_Carlo_Overview.png)

You can find the implementation on [Github](https://github.com/cms-opendata-processing-tasks/FullSimulationReanaWorkflow).


## Tools 

The workflow utilizes Snakemake as the tool that maps out the workflow, it has defined rules for each step where 
it then maps out the workflow and submits the jobs to REANA, where it then takes the mapped out workflow and runs it on the available cluster nodes.

## Parameters

All you have to do is define specific parameters in the `reana.yaml` for your use case and then run the workflow:

- `record_id` - the record id of the dataset you want to simulate

- `events` - the total number of events you want to simulate

- `eventsPerJob` - the number of events each job will run

- `eos_outdir` - the path of the folder you want the final root files and plots to be saved at

{{< learner >}}
As you read the example lesson, look for the places where metadata becomes visible structure: questions, objectives, key points, and active-learning prompts.
{{< /learner >}}

{{< instructor >}}
This first episode is a good place to explain the module/template split before diving into syntax. Learners usually care less about the build system than maintainers do.
{{< /instructor >}}
