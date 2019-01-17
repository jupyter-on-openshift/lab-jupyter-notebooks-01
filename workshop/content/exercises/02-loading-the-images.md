---
Title: Loading the Images
PrevPage: 01-persistent-workspace
NextPage: 03-loading-the-templates
---

Before you can create the Jupyter Notebook workspace, you first need to load an image for the Jupyter Notebook application into your project in OpenShift. You only need to load this once in a project. You can then use it in creating as many different Jupyter Notebook deployments as you need.

To create the image stream definition for a minimal Jupyter Notebook, run the command:

```execute
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/image-streams/s2i-minimal-notebook.json
```

Once created, run the command:

```execute
oc get imagestreams -o name
```

and you should now see that the `s2i-minimal-notebook` image stream has been added.

Inspect the image stream by running:

```execute
oc describe imagestream s2i-minimal-notebook
```

and you will see that the image stream includes tags for `3.5` and `3.6`. These correspond to versions of the image for Python 3.5 and Python 3.6.
