+++
title = "Computing Resources"
weight = 30
teaching = 15
exercises = 5
questions = ["How much time and space will the simulation take?"]
objectives = ["Understand the time and space requirements of the workflow and how they scale."]
keypoints = ["The workflow scale requirements scale linearly with enough jobs available."]
[tabs]
  sync = false
+++

## Time & Storage

As mentioned in the first run [episode]({{< relref "/episodes/02-first-run/index.md" >}}), the simulation time will depend on the **total number of events** as well as the **number of events per job**. 

For the storage requirements of the workflow, cleanup rules were implemented along the workflow to delete the intermediary root files of a rule after they have been successfully used by the subsequent rule, to save on the total storage needed. Therefore the peak storage used is just where the intermediary root files are the largest, which is during the `DIGI2RAW` and `HLT` steps.

## Benchmarks 

These metrics were measured mid-August 2026, with the workflow utilizing the REANA Kubernetes Clusters (HTCondor has not tested yet as a compute backend). 

### 10,000 Events

#### 800 Events Per Job

|   Step   |   Total Size (GBs) |   File Count |   Peak Storage (GBs) |   Avg Time (h) |
|----------|--------------------|--------------|----------------------|----------------|
| GEN      |         0.0874085  |           12 |            0.0874085 |      0.300821  |
| SIM      |         0.482737   |           12 |            0.570146  |      2.00771   |
| DIGI2RAW |         1.23497    |           12 |            1.71771   |      0.33752   |
| HLT      |         1.1197     |           12 |            2.35467   |      0.318887  |
| PAT      |         0.0418785  |           12 |            1.16158   |      0.0819273 |
| RECO     |         0.251813   |           12 |            0.293692  |      0.48665   |
| NANO     |         0.00396742 |           12 |            0.255781  |      0.0320535 |

`Total time` ~ 3.8 hours

`Peak Storage Usage` ~ 2.35 GBs

`Final Storage Usage` ~ 0.25 GBs

#### 1600 Events Per Job

| Step     | Total Size (GBs) | File Count | Peak Storage (GBs) | Avg Time (h) |
| -------- | ---------------- | ---------- | ------------------ | ------------ |
| GEN      | 0.0868944        | 6          | 0.0868944          | 0.624415     |
| SIM      | 0.481152         | 6          | 0.568047           | 3.88914      |
| DIGI2RAW | 1.23275          | 6          | 1.7139             | 0.646297     |
| HLT      | 1.11714          | 6          | 2.34989            | 0.648159     |
| PAT      | 0.036318         | 6          | 1.15346            | 0.143605     |
| RECO     | 0.249646         | 6          | 0.285964           | 0.8936       |
| NANO     | 0.00265868       | 6          | 0.252305           | 0.0436264    |

`Total time` ~ 7 hours

`Peak Storage Usage` ~ 2.35 GBs

`Final Storage Usage` ~ 0.25 GBs

### 20,000 Events 

#### 800 Events Per Job

| Step     | Total Size (GBs) | File Count | Peak Storage (GBs) | Avg Time (h) |
| -------- | ---------------- | ---------- | ------------------ | ------------ |
| GEN      | 0.181265         | 25         | 0.181265           | 0.312674     |
| SIM      | 1.00096          | 25         | 1.18223            | 2.02227      |
| DIGI2RAW | 2.56267          | 25         | 3.56363            | 0.329211     |
| HLT      | 2.32382          | 25         | 4.88649            | 0.330139     |
| PAT      | 0.0870847        | 25         | 2.4109             | 0.0836789    |
| RECO     | 0.522663         | 25         | 0.609748           | 0.487232     |
| NANO     | 0.00826678       | 25         | 0.53093            | 0.0321643    |

`Total time` ~ 3.6 hours

`Peak Storage Usage` ~ 2.35 GBs

`Final Storage Usage` ~ 0.25 GBs

#### 1600 Events Per Job

| Step     | Total Size (GBs) | File Count | Peak Storage (GBs) | Avg Time (h) |
| -------- | ---------------- | ---------- | ------------------ | ------------ |
| GEN      | 0.173424         | 12         | 0.173424           | 0.62212      |
| SIM      | 0.960361         | 12         | 1.13378            | 4.09312      |
| DIGI2RAW | 2.46316          | 12         | 3.42352            | 0.643861     |
| HLT      | 2.2326           | 12         | 4.69576            | 0.649142     |
| PAT      | 0.0726798        | 12         | 2.30528            | 0.144928     |
| RECO     | 0.499602         | 12         | 0.572282           | 0.960837     |
| NANO     | 0.00531898       | 12         | 0.504921           | 0.0456583    |

`Total time` ~ 7.16 hours

`Peak Storage Usage` ~ 4.69 GBs

`Final Storage Usage` ~ 0.5 GBs

## Variations

Of course, these times can change for many reasons. If you end up with a worfklow run where the number of jobs 
per step exceeds the number of available cluster nodes, that'll result in increased times as each step can't be fully parallelized at once. 

There have been anomalies while testing the workflow, where a step and its subsequent steps take much longer than usual to run, however it has been quite rare.