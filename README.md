LAB - Jupyter Notebooks 01
==========================

This repository contains the first instalment in a series of workshops for learning how to deploy Jupyter Notebooks, and related applications in the Jupyter ecosystem, to OpenShift.

To deploy this workshop standalone in an existing OpenShift project, run:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param TERMINAL_IMAGE="quay.io/jupyteronopenshift/lab-jupyter-notebooks-01:master" \
  --param APPLICATION_NAME=lab-jupyter-notebooks-01
```

This will deploy an instance of the user environment as a standalone deployment. The name of the deployment will by default be `lab-jupyter-notebooks-01`.

To determine the hostname assigned to the route which you need to use in the URL to access the workshop, run:

```
oc get route/lab-jupyter-notebooks-01
```

When you access the URL for the workshop, you will if necessary be redirected to the login page for the OpenShift cluster the workshop is deployed to. You should enter your login and password for the OpenShift cluster.

After you have supplied your credentials, you will be granted access to the workshop.

Note that you will only be granted access to the workshop if your are listed as a project admin for the project the workshop is deployed to. Users of the OpenShift cluster who are members of your project but who only have edit or view access, or users who are not a collaborator of your project, will not be granted access to the workshop.

To delete the workshop when done, run:

```
oc delete all,serviceaccount,rolebinding,configmap -l app=lab-jupyter-notebooks-01
```

This assumes you completed the workshop and followed any steps it describes to remove deployments created by following the steps described in the workshop.
