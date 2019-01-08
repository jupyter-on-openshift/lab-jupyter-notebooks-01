---
Title: JupyterLab Web Design
PrevPage: 03-accessing-a-workspace
NextPage: 05-increasing-resources
---

The Jupyter Notebook web interface which is used is the so called "classic" design. If you wish to use the new JupyterLab web interface design, you can do so by setting an environment variable in the deployment configuration to enable it. To do this, run the command:

```execute
oc set env deploymentconfig experiments JUPYTER_ENABLE_LAB=true
```

This will trigger a re-deployment of the Jupyter Notebook instance. You can monitor progress of the new deployment by running:

```execute
oc rollout status deploymentconfig experiments
```

Once the new deployment has finished, close the existing window for the Jupyter Notebook workspace and open the URL for the instance again.

https://experiments-%project_namespace%.%cluster_subdomain%/

Enter your password, and you should see the JupyterLab web interface design.

![JupyterLab Interface](jupyterlabwebdesign.png)

It is necessary use a new browser window with the original URL, because even when the JupyterLab web interface is enabled, the classic web interface is still supported at the original sub URL the browser would have been on. It is thus necessary to start over, so you are redirected to the sub URL for the JupyterLab web interface.

If you prefer to always have the JupyterLab web interface design, instead of overriding the environment variable in the deployment configuration each time, you can instead edit and change the templates to make it the default. This way it will always be used when creating new Jupyter Notebook workspaces.
