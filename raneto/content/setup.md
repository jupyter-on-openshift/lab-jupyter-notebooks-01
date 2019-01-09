---
Sort: 3
Title: Setup Environment
PrevPage: index
NextPage: notebooks-01/01-images-and-templates
ExitSign: Start Workshop
---

This workshop environment provides you with an interactive terminal in your browser. The user shell has access to all the command line tools you require. You do not need to install anything on your local computer.

Before starting, we need to check that the environment you are using is setup correctly for the workshop and that you have access to a project you can use.

To check that you are currently logged in from the command line, in the interactive terminal in your browser run the command:

```execute
oc auth can-i create pods
```

Did you type the command in yourself? If you did, click on the command instead and you will find that it is executed for you. You can click on any command which has the <span class="glyphicon glyphicon-play-circle"></span> icon shown to the right of it, and it will be copied to the interactive terminal and run.

If the output from the `oc auth can-i` command is `yes`, you are all good to go, and you can scroll to the bottom of the page and click on "Start Workshop".

If instead of the output `yes`, you see:

```
no - no RBAC policy matched
```

or any other errors, it is likely that you need to login to the OpenShift cluster. This will be the case if you are doing the workshop as part of a supervised training session in a hosted workshop environment.

If you need to login, run the command:

```execute
oc login
```

and when prompted, enter in the same username and password you logged into the OpenShift web console, that was supplied to you by the workshop organizer.

Run a second time the command:

```execute
oc auth can-i create pods
```

If the output is `yes`, this time you are all ready to go.

If you still get an error, try creating a new project to do the workshop in by running:

``` execute
read -p "Project Name: " PROJECT_NAMESPACE && \
  oc new-project $PROJECT_NAMESPACE
```

At the prompt for your project name, enter in your username.

If this gives an error and fails to create a project, and you are in a supervised training session, ask the workshop organizer for help.
