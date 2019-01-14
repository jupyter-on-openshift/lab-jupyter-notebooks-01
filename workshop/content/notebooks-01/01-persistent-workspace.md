---
Title: Persistent Workspace
PrevPage: ../index
NextPage: 02-loading-the-images
---

Development of Jupyter Notebooks is done under the banner of [Project Jupyter](https://jupyter.org/). Ready to go container images and templates, for running Jupyter Notebooks on OpenShift, are provided as part of the [Jupyter on OpenShift](https://github.com/jupyter-on-openshift) project. The images and templates from the Jupyter on OpenShift project are designed to make it easy to deploy Jupyter Notebooks to OpenShift.

To show you how quick it is to get a Jupyter Notebook running in OpenShift, the first exercise you are going to do is to create a workspace in OpenShift, running a Jupyter Notebook, where you can upload and/or create notebook files, and work on them. The workspace will use a persistent volume so that anything you create, or additional Python packages you install, will not be lost when the Jupyter Notebook instance is restarted.

This workspace can provide you an ongoing place where you can do any work you want to with Jupyter Notebooks, without needing to install any Jupyter software, or Python, on your own local computer. Instead, everything will be in the cloud, hosted in your OpenShift cluster.
