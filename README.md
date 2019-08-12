LAB - Jupyter Notebooks 01
==========================

This repository contains the first instalment in a series of workshops for learning how to deploy Jupyter Notebooks, and related applications in the Jupyter ecosystem, to OpenShift.

Deploying the Workshop
----------------------

To deploy the workshop, first clone this Git repository to your own machine.

When you clone the repository, ensure you use the `--recurse-submodules` option with the `git clone` command. Alternatively, after having cloned the repository, within the repository directory, run:

```
git submodule update --init --recursive
```

The option to `git clone`, or the `git submodule update` command, ensure that a copy of a Git submodule which contains scripts to help you deploy the workshop will also be cloned.

Next create a project in OpenShift into which the workshop is to be deployed.

```
oc new-project workshops
```

From within the top level of the Git repository, now run:

```
./.workshop/scripts/deploy-spawner.sh
```

You will need to be a user who is cluster admin when you run this command.

The name of the deployment will be `lab-jupyter-notebooks-01`.

You can determine the hostname for the URL to access the workshop by running:

```
oc get route lab-jupyter-notebooks-01
```

This method for deploying the workshop will provide you with a multi user workshop deployment where each user will get a separate session, and users don't need a login for the OpenShift cluster. This is the recommended method deploying the workshop even if doing it yourself, as you will get a distinct project for your session when working through the workshop, and everything will be cleaned up automatically when you are done.

If you prefer to to run the workshop in single user mode, run instead:

```
./.workshop/scripts/deploy-personal.sh
```

This can be run as a normal user, but that user will need to be a project admin of the project it is deployed to. Only project admins will subsequently be able to login to the workshop.

When deploying it as a personal workshop, it is recommended to use a fresh project so you can delete the whole project when you are done.

Editing the Workshop
--------------------

The deployment created above will use a version of the workshop which has been pre-built into an image and which is hosted on `quay.io`.

To make changes to the workshop content and test them, edit the files in the Git repository and then run:

```
./.workshop/scripts/build-workshop.sh
```

This will replace the existing image used by the active deployment.

If you are running an existing instance of the workshop, from your web browser select "Restart Workshop" from the menu top right of the workshop environment dashboard.

When you are happy with your changes, push them back to the remote Git repository. This will automatically trigger a new build of the image hosted on `quay.io`.

If you need to change the RBAC definitions, or what resources are created when a project is created, change the definitions in the `templates` directory. You can then re-run:

```
./.workshop/scripts/deploy-spawner.sh
```

and it will update the active definitions.

Note that if you do this, you will need to re-run:

```
./.workshop/scripts/build-workshop.sh
```

to have any local content changes be used once again as it will revert back to using the image on ``quay.io``.

If you need to ever update the deployment scripts pulled in via a git submodule to the latest version, run:

```
git submodule update --recursive --remote
```

The update will be staged immediately, so don't forget to commit it.

Deleting the Workshop
---------------------

To delete the spawner and any active sessions, including projects, run:

```
./.workshop/scripts/delete-spawner.sh
```

If you only ran a personal workshop instance, instead run:

```
./.workshop/scripts/delete-personal.sh
```

To delete the build configuration for the workshop image, run:

```
./.workshop/scripts/delete-workshop.sh
```

To delete special global resources which may have been created when using the spawner, run:

```
./.workshop/scripts/delete-resources.sh
```
