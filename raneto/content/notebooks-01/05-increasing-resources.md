---
Title: Increasing Resources
PrevPage: 04-jupyterlab-web-design
NextPage: 06-uploading-notebooks
---

When deploying the Jupyter Notebook workspace using the template, 512Mi of memory will be allocated to the container created.

If you are working with large data sets, or wish to be able to open many Jupyter notebook files at the same time, you may need to increase the amount of memory allocated.

To determine the current amount of memory allocated, you have a couple of options.

The first is to run:

```execute
oc describe deploymentconfig experiments
```

Look through the output, and for the `notebook` container you should see an entry for the memory limit, similar to:

```
Containers:
  notebook:
   ...
   Limits:
     memory:   512Mi
```

Alternatively, to display just the value of the limit, run:

```execute
oc get deploymentconfig experiments -o template --template '{{(index .spec.template.spec.containers 0).resources.limits.memory}}{{"\n"}}'
```

To increase the memory allocated, you can use the `oc set resources` command. To increase the memory limit to 768Mi, run:

```execute
oc set resources deploymentconfig experiments --containers notebook --limits memory=768Mi
```

To verify the change, run again the command:

```execute
oc get deploymentconfig experiments -o template --template '{{(index .spec.template.spec.containers 0).resources.limits.memory}}{{"\n"}}'
```

If you know in advance of creating a Jupyter Notebook workspace that you will need additional memory, you can set the memory by passing the `NOTEBOOK_MEMORY` template parameter to the `notebook-workspace` template.

A template parameter can also be used to set the size of the persistent storage allocated. The default value for the size is `1Gi`. The name of the template parameter for the size of the volume is `VOLUME_SIZE`. The volume size is a request only. If only larger volume sizes are available, you can be given a persistent volume with larger capacity than requested.

To see how much capacity the persistent volume allocated does have, run:

```execute
oc get pvc experiments-data
```

This will display output similar to:

```
NAME              STATUS  VOLUME  CAPACITY  ACCESS MODES  STORAGECLASS  AGE
experiments-data  Bound   vol121  10Gi      RWO                         15m
```

Note that if your project is subject to resource limit ranges and/or resource quotas, you will only be able to increase the amount of memory allocated up to maximum allowed under the limit range. Although the limit range may allow you set a value, you still also need to have an adequate memory allowance remaining, not in use, under any resource quota. If you have insufficient memory remaining under your resource quota, the deployment will not succeed.

Resource quotas can also exist for persistent storage, including the maximum size persistent volume you can request, as well as the number of persistent volumes and overall capacity.

You can view what the resource limit ranges are, by running:

```execute
oc describe limitranges
```

You can view what resource quota you are subject to, by running:

```execute
oc describe resourcequotas
```

The output from these command will be empty if you are not subject to any resource limit ranges or quotas.
