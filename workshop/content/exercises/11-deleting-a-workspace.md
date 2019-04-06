---
Title: Deleting a Workspace
PrevPage: 10-mounting-via-webdav
NextPage: ../finish
---

The Jupyter Notebook workspace deployed using the `notebook-workspace` template is intended to serve as a long lived place where you can work on Jupyter notebooks. The use of attached persistent storage ensures that you will not loose your work even if the Jupyter Notebook application is restarted.

If you have finished with a particular Jupyter Notebook workspace, you can delete it, by deleting the resources created by the deployment.

To see a list of all the resources created, run:

```execute
oc get all,pvc --selector app=workspace -o name
```

This will display output similar to:

```
pod/workspace-3-62692
replicationcontroller/workspace-1
replicationcontroller/workspace-2
replicationcontroller/workspace-3
service/workspace
deploymentconfig.apps.openshift.io/workspace
route.route.openshift.io/workspace
route.route.openshift.io/workspace-webdav
persistentvolumeclaim/workspace-data
```

To then delete the Jupyter Notebook workspace, run:

```execute
oc delete all,pvc --selector app=workspace
```

Note that this command will delete the deployed application, as well as the persistent volume. If you wanted to retain the persistent volume in order to copy files out of it at a later time, do not include `pvc` in the list of resources to delete.
