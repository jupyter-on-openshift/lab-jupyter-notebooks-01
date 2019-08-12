Neither Kubernetes or OpenShift provide a method for mounting of a persistent volume used by an application in a cluster, to a separate host outside of the cluster.

One way around this, is to host within OpenShift a WebDAV server, which exports access to the persistent volume, over the HTTP protocol.

WebDAV is an extension of HTTP that allows clients to create, change, and move documents on a remote server. Although it relies on HTTP as the transport mechanism for communicating with a server, major operating systems support the protocol as a backend for mounted filesystems. This means that one can connect to a WebDAV server and then work directly with files hosted by the server as if they were present in your local file system.

For details on how to mount a WebDAV filesystem, check the documentation for your operating system. Instead of mounting the remote persistent volume as a local filesystem, various tools are also available that allow access to a WebDAV filesystem without needing to mount it as a local file system. One popular example of such a tool is [CyberDuck](https://cyberduck.io/), for Windows and macOS. There is also the [cadaver](http://www.webdav.org/cadaver/) command line client, which acts similar to `ftp` or `smbclient` tools, but which works against a WebDAV server instead.

To support access using the WevDAV protocol, when the `notebook-workspace` template is used to create the Jupyter Notebook workspace, in addition to running the Jupyter Notebook application, it runs a WebDAV server. The integrated WebDAV server is accessible by using the `/wevdav/` path with the existing URL route created for the Jupyter Notebook workspace.

To browse the content of the workspace exposed by the WebDAV server through your web browser, you can visit the URL:

https://workspace-%project_namespace%.%cluster_subdomain%/webdav/

When connecting to the WebDAV server, the login name will be `jupyter` and the password will be the same password you used to secure access to the Jupyter Notebook workspace through the browser.

When using a web browser to access the WebDAV server, it is read only. You can download files, but cannot upload them.

If you have the `cadaver` command line client installed it can be used like the `ftp` or `smbclient` command line clients. For example, run:

```execute
cadaver https://workspace-%project_namespace%.%cluster_subdomain%/webdav/
```

and enter the same user name and password as above.

To see the list of files in the workspace, run at the `cadaver` prompt:

```execute
ls
```

You can then used `edit` to remotely edit text files. Use `put` or `mput` to upload files, or `get` or `mget` to download files.

To exit the client, run at the `cadaver` prompt:

```execute
quit
```

When copying notebook files to and from the Jupyter Notebook workspace over WebDAV, ensure you do not have the notebook file open in the Jupyter Notebook web interface at the same time. This avoids the risk of updating or copying files that have not be fully written to the persistent volume.
