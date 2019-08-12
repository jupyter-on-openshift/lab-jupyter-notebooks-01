The minimal Jupyter Notebook image you loaded can be deployed as is, but to make it easier to secure access properly, add persistent storage, and define resources, as well as use it as a Source-to-Image (S2I) builder to create custom Jupyter Notebook images, a set of templates also exist.

To load the templates, run the commands:

```execute
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-deployer.json
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-builder.json
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-quickstart.json
oc apply -f https://raw.githubusercontent.com/jupyter-on-openshift/jupyter-notebooks/master/templates/notebook-workspace.json
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

In this workshop you will be using the `notebook-workspace` template.

To see details about this template and what parameters can be provided when using the template, run the command:

```execute
oc describe template notebook-workspace
```
