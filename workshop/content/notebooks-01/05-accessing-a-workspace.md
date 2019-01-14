---
Title: Accessing a Workspace
PrevPage: 04-creating-a-workspace
NextPage: 06-enabling-jupyterlab
---

Once the deployment has completed, you can see details of the public route created, including what public hostname the Jupyter Notebook instance was given, by running:

```execute
oc get route workspace
```

You can query just the public hostname, by running:

```execute
oc get route workspace -o template --template '{{.spec.host}}{{"\n"}}'
```

The argument to `oc get route` is the name passed in the `APPLICATION_NAME` template parameter. In this case it was `workspace`.

Open the hostname from a new browser window, or click on:

https://workspace-%project_namespace%.%cluster_subdomain%/

You should be presented with a form to enter a password. Use the same password as you used when you created the deployment.

![Password Entry](jupyternotebooklogin.png)

Having logged in, you will then be presented with the Jupyter Notebook file browser, and can start using the workspace.

![File Browser](jupyternotebookbrowser.png)
