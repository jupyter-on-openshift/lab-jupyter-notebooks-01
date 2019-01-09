---
Title: Uploading Notebooks
PrevPage: 05-increasing-resources
NextPage: 07-mounting-via-webdav
---

The Jupyter Notebook workspace you created using the `notebook-workspace` template is empty. It has only the minimal set of Python packages installed which are necessary to run the Jupyter Notebook software, with no additional files such as notebooks or data files.

To work with a Jupyter notebook file, you can either create them from scratch or upload them to the workspace.

To upload your existing Jupyter notebook files and data files, you can use the Jupyter Notebook web interface, or copy them into the workspace using the OpenShift command line tools.

To upload files to the workspace when using the JupyterLab web interface design, click on the upload button icon above the file browser.

![JupyterLab Upload](jupyterlabupload.png)

When using the classic Jupyter Notebook web interface design, click on the "Upload" button to the right and above the file browser.

![Classic Upload](jupyterclassicupload.png)

To upload files using the OpenShift command line tools you first need to identify the name of the Kubernetes pod in which the instance of the Jupyter Notebook workspace is running. You can get a list of all the pods, for the instance of the Jupyter Notebook application you deployed, by running:

```execute
oc get pods --selector app=experiments
```

This should display output similar to:

```
NAME                  READY     STATUS    RESTARTS   AGE
experiments-3-6648q   1/1       Running   0          15m
```

There would normally only be a single pod shown. If there is more than one, the one you want is that with "Running" status.

To capture just the name of the pod in an environment variable which can then be used in subsequent commands, run:

```execute
POD=`oc get pods --selector app=experiments -o jsonpath='{.items[?(@.status.phase=="Running")].metadata.name}'`; echo $POD
```

In your own OpenShift cluster when copying files, you can skip capturing the name of the pod like this, and instead type the name of the pod in manually when running the command below. An environment variable is used here just to help automate things for these workshop instructions.

To copy all the files in a local directory directory called `notebooks` to the Jupyter Notebook workspace, run:

```execute
oc rsync notebooks/ $POD:/opt/app-root/src/
```

The destination path `/opt/app-root/src` is the home directory for the Jupyter Notebook application. Any directories or files created under this directory will be visible in the Jupyter Notebook file browser. This directory is part of the persistent volume attached to the Jupyter Notebook workspace, so any changes now made to the files copied to that directory will be preserved, even if the Jupyter Notebook instance is restarted.

In addition to being able to use `oc rsync` to copy files into the Jupyter Notebook workspace, it can be used to copy files back from it to a local computer.

For additional information on using `oc rsync` to copy files to and from applications running in OpenShift, see the set of exercises, [Transferring Files in and out of Containers](https://learn.openshift.com/introduction/transferring-files/), hosted on the [OpenShift Interactive Learning Portal](https://learn.openshift.com/).
