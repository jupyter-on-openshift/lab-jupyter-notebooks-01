---
Title: Increasing Resources
PrevPage: 04-jupyterlab-web-design
NextPage: ../finish
ExitSign: Finish Workshop
---

When deploying the Jupyter Notebook workspace using the template, by default, 512Mi will be allocated for memory to the pod created.

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

Alternatively, to get just the value of the limit, run:

```execute
oc get deploymentconfig experiments -o template --template '{{(index .spec.template.spec.containers 0).resources.limits.memory}}{{"\n"}}'
```

To increase the memory allocated, you can use the `oc set resources` command. To increase the memory limit to 768Mi, run:

```execute
oc set resources deploymentconfig experiments --limits memory=768Mi
```

To verify the change, run again the command:

```execute
oc get deploymentconfig experiments -o template --template '{{(index .spec.template.spec.containers 0).resources.limits.memory}}{{"\n"}}'
```

Note that if your project is subject to resource limit ranges and/or resource quotas, you will only be able to increase the amount of memory allocated up to maximum allowed under the limit range. Although the limit range may allow you set a value, you still also need to have an adequate memory allowance remaining, not in use, under any resource quota. If you have insufficient memory remaining under your resource quota, the deployment will not succeed.

You can view what the resource limit ranges are, if set for a project, by running:

```execute
oc describe limitranges
```

You can view what resource quota you are subject to, by running:

```execute
oc describe resourcequotas
```
