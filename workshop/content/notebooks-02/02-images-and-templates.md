---
Title: Images and Templates
PrevPage: 01-distributing-notebooks
NextPage: ../finish
ExitSign: Finish Workshop
---

Before we get started, ensure that you have deleted the Jupyter Notebook workspace you already created, by running:

```execute
oc delete all,pvc --selector app=workspace
```

Next ensure that the image streams and templates loaded in the first exercises are still loaded. These will need to be loaded if you have skipped the first set of exercises.

To load the image streams, run:

```execute
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/image-streams/s2i-minimal-notebook.json
```

This command is safe to run, even if you had run it before and they were already loaded.

To load the templates, run:

```execute
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-deployer.json
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-builder.json
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-quickstart.json
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-workspace.json
```

Again, these commands are safe to run if you have already run them.
