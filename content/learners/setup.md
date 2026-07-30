+++
title = "Setup"
weight = 10
+++

## Terminal Setup

To get started, assuming a CERN account, the `lxplus` environment is accessed through `ssh`

```
# replace johndoe with your account username
ssh johndoe@lxplus.cern.ch
```

When prompted enter your `lxplus` password, the terminal won't show the password for security reasons.

## REANA

This workflow utilizes the REANA computing clusters, to run a workflow using them, a REANA access token and the activation of `reana-client` is needed. Follow **only** the `First Example` to get setup and verify that it's working, then return to continue the workflow setup. 

[Setup REANA](https://docs.reana.io/getting-started/first-example/)

After finishing the `First Example` tutorial, return to the home directory through

```
cd ~
```

To avoid going through all the steps of activating the `reana-client` everytime you access lxplus, a small script can be used, **be sure to replace `xxxxxxxxxxxxxxxxxxx` with your own `REANA Access Token`** and copy the following into your terminal:

```
cat << 'EOF' > ~/private/reana-env-prod.sh
#!/bin/bash
source /afs/cern.ch/user/r/reana/public/reana-qa/bin/activate
export REANA_SERVER_URL=https://reana-qa.cern.ch
export REANA_ACCESS_TOKEN=xxxxxxxxxxxxxxxxxxx
EOF
```

Now to activate the `reana-client` environment whenever needed, simply run:

```
source ~/private/reana-env-prod.sh
```