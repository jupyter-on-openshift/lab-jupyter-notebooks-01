---
Title: Mounting via WebDAV
PrevPage: 06-uploading-notebooks
NextPage: 08-deleting-a-workspace
---

Neither Kubernetes or OpenShift provide a method for mounting of a persistent volume used by an application in a cluster, to a separate host outside of the cluster.

One way around this, is to host within OpenShift a WebDAV server, which exports access to the persistent volume, over the HTTP protocol.

WebDAV is an extension of HTTP that allows clients to create, change, and move documents on a remote server. Although it relies on HTTP as the transport mechanism for communicating with a server, major operating systems support the protocol as a backend for mounted filesystems. This means that one can connect to a WebDAV server and then work directly with files hosted by the server as if they were present in your local file system.

For details on how to mount a WebDAV filesystem, check the documentation for your operating system. Instead of mounting the remote persistent volume as a local filesystem, various tools are also available that allow access to a WebDAV filesystem without needing to mount it as a local file system. One popular example of such a tool is [CyberDuck](https://cyberduck.io/), for Windows and macOS.

To support access using the WevDAV protocol, when the `notebook-workspace` template is used to create the Jupyter Notebook workspace, in addition to running the Jupyter Notebook application, it runs a WebDAV server. This WebDAV server is accessible via its own URL and provides access to the `/opt/app-root/src` directory.

To see the hostname allocated to the URL for the WebDAV server, run:

```execute
oc get route experiments-webdav
```

The URL for access to the WebDAV server for the instance of the Jupyter Notebook workspace you created is:

```copy
https://experiments-webdav-%project_namespace%.%cluster_subdomain%/webdav/
```

When connecting to the WebDAV server, the login name will be `jupyter` and the password will be the same password you used to secure access to the Jupyter Notebook web space through the browser. You must use the `/webdav/` path in the URL or setup of the WebDAV connection.

When copying notebook files to and from the Jupyter Notebook workspace over WebDAV, ensure you do not have the notebook file open in the Jupyter Notebook web interface at the same time. This avoids the risk of updating or copying files that have not be fully written to the persistent volume.
