+++
title = "Setup"
weight = 10
+++

## Terminal Setup

To get started, assuming you have a CERN account, the `lxplus` environment is accessed through `ssh`
```
# replace johndoe with your CERN username
ssh johndoe@lxplus.cern.ch
```
When prompted enter your `lxplus` password, the terminal won't show the password for security reasons.
## REANA

This workflow utilizes the REANA computing clusters, to run a workflow using them, a REANA access token and the activation of `reana-client` is needed. Follow **only** the `First Example` to get setup and verify that it's working, then return to this tutorial. 

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
## Kerberos

For the workflow to access and write files to EOS, `Kerberos` authentication is required. [As instructed in the REANA docs](https://docs.reana.io/advanced-usage/access-control/kerberos/), we'll start with generating the `keytab` file.

### Generate keytab file
```
# replace johndoe with your CERN username
cern-get-keytab --keytab ~/.keytab --user --login johndoe
```

### Uploading secrets

After getting the working `keytab` file, upload your CERN username and `keytab` secrets to REANA with:
```
reana-client secrets-add --env CERN_USER=johndoe \
                           --env CERN_KEYTAB=.keytab \
                           --file ~/.keytab
```

## Next step 

Once a working evnironment has been setup, continue to [Introduction]({{< relref "/episodes/01-introduction" >}})