---
Title: Creating a Workspace
PrevPage: 01-images-and-templates
NextPage: 03-accessing-a-workspace
---

Now that you have the images and templates for deploying a Jupyter Notebook loaded, you can create the Jupyter Notebook workspace by running the command:

```execute
read -p "Enter Password: " NOTEBOOK_PASSWORD && \
  oc new-app --template notebook-workspace \
  --param APPLICATION_NAME=experiments \
  --param NOTEBOOK_PASSWORD=$NOTEBOOK_PASSWORD
```

This command is setup to prompt you for a password to secure access to the Jupyter Notebook workspace. Enter the password you would like to use.

Once the template has been processed and the deployment created, you should see output similar to:

```
--> Deploying template "workshop/notebook-workspace" to project workshop

     Jupyter Notebook Workspace
     ---------
     Template for deploying Jupyter Notebook images with persistent storage and webdav filesystem access.

     * With parameters:
        * APPLICATION_NAME=experiments
        * NOTEBOOK_IMAGE=s2i-minimal-notebook:3.6
        * NOTEBOOK_PASSWORD=grumpy
        * NOTEBOOK_MEMORY=512Mi
        * VOLUME_SIZE=1Gi

--> Creating resources ...
    deploymentconfig.apps.openshift.io "experiments" created
    persistentvolumeclaim "experiments-data" created
    service "experiments" created
    route.route.openshift.io "experiments" created
    route.route.openshift.io "experiments-webdav" created
--> Success
    Access your application via route 'experiments-workshop.apps.grumpy-xyz.openshiftworkshop.com'
    Access your application via route 'experiments-webdav-workshop.apps.grumpy-xyz.openshiftworkshop.com'
    Run 'oc status' to view your app.
```

The template creates a set of resources for the deployment.

These include a persistent volume for storing data for your Jupyter Notebook workspace, and a route, which exposes the Jupyter Notebook workspace via a URL so you can access it. When you connect to the Jupyter Notebook workspace, a secure connection will be used and you will need to login using the password you supplied.

For this workspace, the name `experiments` was passed to the `APPLICATION_NAME` template parameter. If you do not supply this template parameter, it will default to using the name `custom-notebook`. This name is used in the resources created, and the URL you use to access the Jupyter Notebook workspace.

If you were to create multiple Jupyter Notebook workspaces in the one project, you should give them unique names using the `APPLICATION_NAME` template parameter.

To monitor progress of the deployment, run the command:

```execute
oc rollout status deploymentconfig experiments
```

The command will exit once the deployment has completed and the Jupyter Notebook workspace is ready to use.

Note that if it is the first deployment of a Jupyter Notebook to an OpenShift cluster, startup may be delayed. This is due to the Jupyter Notebook image needing to be pulled down to the cluster.
