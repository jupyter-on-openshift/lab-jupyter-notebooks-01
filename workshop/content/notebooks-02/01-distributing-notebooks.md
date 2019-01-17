---
Title: Distributing Notebooks
PrevPage: ../notebooks-01/11-deleting-a-workspace
NextPage: 02-images-and-templates
---

In the first set of exercises you deployed a Jupyter Notebook workspace. This included a persistent volume so that any work done in the workspace was retained, even if the Jupyter notebook instance was restarted.

A persistent Jupyter notebook workspace is useful where you want an environment in which to try out ideas, and create, or work on your own Jupyter notebooks.

If instead of working on your own Jupyter notebooks you wanted to use a set of Jupyter notebooks created by someone else, you would need to manually upload the Jupyter notebook files into the workspace, as well as install any additional Python packages required.

In order to distribute a set of Jupyter notebook files and everything they require, there are two approaches you can use.

The first option is to host the Jupyter notebook files in a hosted Git repository where others can find them. Because this is only the Jupyter notebook files and is not a complete runtime environment, you would also need to add a `requirements.txt` file listing the set of Python packages required. This would allow another person to replicate the runtime environment by installing the listed packages.

This option provides maximum portability, as the environment could potentially be replicated on different operating systems, different Python distributions, or different Python versions. This however is not guaranteed, as the operating system could be lacking a required system package, the Python runtime used may not be fully compatible, the author may not have listed all the Python packages required, or they didn't pin versions for all Python packages and so there is no certainty as to what versions they were actually using.

A second option which provides more of a guarantee that another person would have the same runtime environment is to use a container image to package up the Jupyter notebook files, along with the Python and Jupyter Notebook runtime environment, and any Python or system packages required, all pre-installed.

Using a container image as the packaging format, anyone wanting to use the Jupyter notebook files need only then have access to a container runtime to run it. The container runtime could be locally hosted, or a cloud platform such as Kubernetes or OpenShift could be used.

In this next set of exercises, you will learn how to deploy a container image which includes a set of existing Jupyter notebook files, and how to build your own container image that you could distribute.
