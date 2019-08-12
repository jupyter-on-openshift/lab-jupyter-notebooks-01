Using the Jupyter Notebook web interface isn't particularly convenient when you need to upload many notebooks files as they will need to be uploaded one at a time. An alternative if using the web interface is to package them up into a single archive file and extract them once uploaded, from a terminal created from the Jupyter Notebook web interface.

The `oc rsync` command provides an easier way to copy up a directory of files in one operation, but either way, you need to have the files on your local computer first. Often, sets of Jupyter notebooks are distributed by publishing them on a hosted Git repository. In this case, the Git repository can be checked out directly into the Jupyter Notebook workspace.

A hosted Git repository can be used as a distribution mechanism where someone wants others to be able to use their notebooks. You can also use it to manage your own set of notebooks, including being able to version them to track changes. It also makes it easy for you to then share them later with others as well.

To checkout a hosted Git repository into the Jupyter Notebook workspace, you can use a terminal created from the Jupyter Notebook web interface, or you can access the pod for your instance using `oc rsh` and execute a `git clone` command.

To capture the current name of the pod in an environment variable which can then be used in subsequent commands, run:

```execute
POD=`oc get pods --selector app=workspace -o jsonpath='{.items[?(@.status.phase=="Running")].metadata.name}'`; echo $POD
```

Then checkout a copy of the hosted Git repository to the workspace by running:

```execute
oc rsh $POD bash -c "git clone https://github.com/amueller/scipy-2018-sklearn.git"
```

This particular Git [repository](https://github.com/amueller/scipy-2018-sklearn.git) contains a tutorial by Guillaume Lemaitre and Andreas Mueller, presented at the SciPy 2018 conference, on `scikit-learn`, a package for machine learning in Python.

Once the package is checked out, it will be able to be found in the `scipy-2018-sklearn` subdirectory from the Jupyter Notebook file browser.

Before you can start using any of the notebook files, you first need to install any Python packages required.

The set of Python packages required in this case can be found listed in the `requirements.txt` file from the Git repository. To install the packages, run:

```execute
oc rsh $POD bash -c "pip install -r scipy-2018-sklearn/requirements.txt"
```

You are now ready to start browsing the notebooks provided by the Git repository and executing them to try them out.
