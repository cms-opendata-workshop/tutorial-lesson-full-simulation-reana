+++
title = "First Run"
weight = 20
teaching = 15
exercises = 10
questions = ["How to get the workflow locally?", "What are the steps to running the workflow?"]
objectives = ["Learn to run the workflow and simulate the dataset you need."]
keypoints = ["Where and how to set the parameters to fit your use case."]
+++


## Get the Workflow

The code to run the simulation workflow will not utilize your local device's resources, but the workflow itself will 
be started from your device.

### Pull the Code

On your `lxplus` terminal or working environment of choice, make sure that your current working directory is where you want to have the code stored. If you're unsure, then simply store it at your home directory. To get there just run.
```
cd ~
```

Then you can pull the workflow code by running
```
git clone https://github.com/cms-opendata-processing-tasks/FullSimulationReanaWorkflow.git
```

This will create a directory name `FullSimulationReanaWorkflow`, enter the directory by simply running
```
cd FullSimulationReanaWorkflow
```

## Setting your Parameters

All the parameters you need to specify are located in the `reana.yaml` file at the root of your directory. Choose the 
approach you prefer to edit the file itself. 

### 1- Record ID 

To get started you'll need to specify the `record ID` of the dataset you want to simulate. Assuming the source of the dataset is from [opendata.cern.ch](https://opendata.cern.ch) the `record ID` is the 5 digit number in the URL at the top of the page of the dataset, e.g. `opendata.cern.ch/record/12345`.

![URL with Record ID](fig/showing_record_id.png)

Copy the `record ID` and place it in the `reana.yaml` file under the `parameters` section:
```
  parameters:
    # Provide the record ID of the dataset you want to simulate
    record_id: 12345
```

### 2- Events & Events Per Job

You'll need to provide the number of total events you want to simulate, and the number of events to provide each job. To calculate the total number of jobs you'll have simply:

$$\dfrac{\text{\# of events}}{\text{\# of events per job}} = \text{\# of jobs}$$

With a higher number of events per job, there will be less total jobs but each job will take longer to run and the maximum number of events per job is 1600 to avoid artificial duplication during the simulation. 

If you provide a fewer number of events per job, each job will finish more quickly, however you'll have more total jobs and that'll be limited by how many jobs the REANA cluster can run at a time.

These parameters can be specified in the `reana.yaml` file under the parameters sections
```
  # Provide the number of events you want the workflow to simulate
  events: 2
  # Provide the number events you want assigned to each job
  eventsPerJob: 1
```

You'll have to find the balance that works for your case, the next episode will provide the time and storage benchmarks of the workflow to help you understand how long it'll take and how much storage you'll need.

### 3- EOS 

The final root files, plots, metrics, etc. will all be stored in the `EOS` directory you specify. Assuming you want to store in your own personal `EOS` directory, the format will be `/eos/user/first_letter_of_first_name/cern_username/project_name`. 

For example assuming the user "John Doe" wants to store the results in his project directory named "my_project", just change the `eos_outdir` field name in the `reana.yaml`:
```
  # Provide the eos_outdir you want the results to be stored in
  eos_dir: "/eos/user/j/johndoe/my_project"
```