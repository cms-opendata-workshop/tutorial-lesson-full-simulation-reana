+++
title = "Running the workflow"
weight = 20
teaching = 15
exercises = 10
questions = ["What are the steps to running the workflow?"]
objectives = ["Learn to simulate the dataset you need."]
keypoints = ["Challenge blocks should be easy to read in source form and easy to scan on the page.", "Hints and solutions should stay collapsible but also support bulk expansion in the all-in-one page."]
+++

## Setting your parameters

### 1- Record ID 

To get started you'll need to specify the `record ID` of the dataset you want to simulate. Assuming the source of the dataset is from [opendata.cern.ch](https://opendata.cern.ch) the `record ID` is the 5 digit number in the URL at the top of the page of the dataset, e.g. `opendata.cern.ch/record/12345`.

![URL with Record ID](fig/showing_record_id.png)

Copy the `record ID` and place it in the `reana.yaml` file under the `parameters` section:
```
  parameters:
    # Provide the record ID of the dataset you want to simulate
    record_id: 12345
```