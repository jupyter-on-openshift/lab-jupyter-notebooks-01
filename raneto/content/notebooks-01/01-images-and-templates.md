---
Title: Images and Templates
PrevPage: ../index
NextPage: 02-creating-a-workspace
---

Development of Jupyter Notebooks is done under the banner of [Project Jupyter](https://jupyter.org/). Ready to go container images and templates, for running Jupyter Notebooks on OpenShift, are provided as part of the [Jupyter on OpenShift](https://github.com/jupyter-on-openshift) project. The images and templates from the Jupyter on OpenShift project are designed to make it easy to deploy Jupyter Notebooks to OpenShift.

To show you how quick it is to get a Jupyter Notebook running in OpenShift, the first exercise you are going to do is to create a workspace in OpenShift, running a Jupyter Notebook, where you can upload and/or create notebook files, and work on them. The workspace will use a persistent volume so that anything you create, or additional Python packages you install, will not be lost when the Jupyter Notebook instance is restarted.

This workspace can provide you an ongoing place where you can do any work you want to with Jupyter Notebooks, without needing to install any Jupyter software, or Python, on your own local computer. Instead, everything will be in the cloud, hosted in your OpenShift cluster.

## Loading the images

Before you can create the Jupyter Notebook workspace, you first need to load the images and templates you will be using into your project in OpenShift. You only need to load these once in a project. You can then use them to create as many different Jupyter Notebook deployments as you need.

To create the image stream definition for a minimal Jupyter Notebook, run the command:

```execute
oc create -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/image-streams/s2i-minimal-notebook.json
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

## Loading the templates

The minimal Jupyter Notebook image you loaded above can be deployed as is, but to make it easier to secure access properly, add persistent storage, and define resources, as well as use it as a Source-to-Image (S2I) builder to create custom Jupyter Notebook images, a set of templates also exist.

To load the templates, run the commands:

```execute
oc create -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-deployer.json
oc create -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-builder.json
oc create -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-quickstart.json
oc create -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-workspace.json
```

This will load the following templates:

* `notebook-deployer` - Template for deploying a Jupyter Notebook image.

* `notebook-builder` - Template for building a custom Jupyter Notebook image using Source-to-Image (S2I) against a hosted Git repository. Python packages listed in the `requirements.txt` file of the Git repository will be installed and any files, including notebook images, will be copied into the image. The image can then be deployed using the `notebook-deployer` template.

* `notebook-quickstart` - Template for building and deploying a custom Jupyter Notebook image. This combines the functionality of the `notebook-builder` and `notebook-deployer` templates.

* `notebook-workspace` - Template for deploying a Jupyter Notebook instance which also attaches a persistent volume, and copies any Python packages and notebooks included in the image, into the persistent volume. Any work done on the notebooks, or to install additional Python packages, will survive a restart of the Jupyter Notebook environment. A webdav interface is also enabled to allow remote mounting of the persistent volume to a local computer.

You can see the list of templates loaded by running:

```execute
oc get templates
```

In the initial exercise you will be using the `notebook-workspace` template.

To see details about this template and what parameters can be provided when using the template, run the command:

```execute
oc describe template notebook-workspace
```
