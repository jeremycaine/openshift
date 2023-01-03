# Local OpenShift on macos

Apple MacPro Silicon M1 `aarch64` chip architecture

## OpenShift Local (formerly Code Ready Containers)

### Install
- Download installer and pull secret from [Dowload page](https://console.redhat.com/openshift/create/local)
- Run installer
- Applications | Red Hat OpenShift Local > double-click, launches an installer
- select a full OpenShift cluster or Podman
- paste in the pull secret text
- decide on whether to sent telemetry data to Red Hat
- Run Setup


### Start
Once installed
- go to Terminal and `.crc` directory will be in your macos user folder e.g. `/Users/<username>`
- `crc start` which takes about four minutes to start up the cluster instance
- password will be printed in the output

example tail of start output
```
...
INFO Operators are stable (3/3)...
INFO Adding crc-admin and crc-developer contexts to kubeconfig...
Started the OpenShift cluster.

The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: GfffH-TCw7R-4CQqa-rZ8cR

Log in as user:
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443
```

### Access 
Access the web console
```
crc console
```

Log in as the developer user with the password printed in the output of the crc start command. You can also view the password for the developer and kubeadmin users by running the following command: 
```
crc console --credentials
```

### OpenShift CLI
Log into command line as developer
```
eval $(crc oc-env)
oc login -u developer https://api.crc.testing:6443
```
Output will be:
```
Logged into "https://api.crc.testing:6443" as "developer" using existing credentials.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>
```

