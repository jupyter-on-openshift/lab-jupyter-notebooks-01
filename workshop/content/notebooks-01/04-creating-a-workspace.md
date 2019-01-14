---
Title: Creating a Workspace
PrevPage: 03-loading-the-templates
NextPage: 05-accessing-a-workspace
---

Now that you have the images and templates for deploying a Jupyter Notebook loaded, you can create the Jupyter Notebook workspace by running the command:

```execute
read -p "Enter Password: " NOTEBOOK_PASSWORD && oc new-app --template notebook-workspace --param APPLICATION_NAME=workspace --param NOTEBOOK_PASSWORD=$NOTEBOOK_PASSWORD
```

This command will prompt you for a password to secure access to the Jupyter Notebook workspace. Enter the password you would like to use.

Once the template has been processed and the deployment created, you should see output similar to:

```
--> Deploying template "workshop/notebook-workspace" to project workshop

     Jupyter Notebook Workspace
     ---------
     Template for deploying Jupyter Notebook images with persistent storage and webdav filesystem access.

     * With parameters:
        * APPLICATION_NAME=workspace
        * NOTEBOOK_IMAGE=s2i-minimal-notebook:3.6
        * NOTEBOOK_PASSWORD=grumpy
        * NOTEBOOK_MEMORY=512Mi
        * VOLUME_SIZE=1Gi

--> Creating resources ...
    deploymentconfig.apps.openshift.io "workspace" created
    persistentvolumeclaim "workspace-data" created
    service "workspace" created
    route.route.openshift.io "workspace" created
    route.route.openshift.io "workspace-webdav" created
--> Success
    Access your application via route 'workspace-workshop.apps.grumpy-xyz.openshiftworkshop.com'
    Access your application via route 'workspace-webdav-workshop.apps.grumpy-xyz.openshiftworkshop.com'
    Run 'oc status' to view your app.
```

The template creates a set of resources for the deployment. These include a persistent volume for storing data for your Jupyter Notebook workspace, and a route, which exposes the Jupyter Notebook workspace via a URL so you can access it. When you connect to the Jupyter Notebook workspace, a secure connection will be used and you will need to login using the password you supplied.

For this workspace, the name `workspace` was passed to the `APPLICATION_NAME` template parameter. If you do not supply this template parameter, it will default to using the name `custom-notebook`. This name is used in the resources created, and the URL you use to access the Jupyter Notebook workspace.

If you were to create multiple Jupyter Notebook workspaces in the one project, you should give them unique names using the `APPLICATION_NAME` template parameter.

To monitor progress of the deployment, run the command:

```execute
oc rollout status deploymentconfig workspace
```

The initial deployment when using the `notebook-workspace` template can take some time. This is because the persistent volume will need to be populated, by copying the contents of the workspace from the image to the persistent volume. Depending on the class of persistent storage used by the cluster, how long this will take can vary. A subsequent restart of the Jupyter Notebook instance will be quicker, as the copying of contents only needs to be done once.

Once the deployment has completed, the `oc rollout status` command will exit, and the Jupyter Notebook workspace will be ready to use.
