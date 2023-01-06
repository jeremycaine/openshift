# OpenShift Local (formerly Code Ready Containers)
On Apple MacPro Silicon M1 `aarch64` chip architecture

## Install
- Download installer and pull secret from [Dowload page](https://console.redhat.com/openshift/create/local)
- Run installer
- Applications | Red Hat OpenShift Local > double-click, launches an installer
- select a full OpenShift cluster or Podman
- paste in the pull secret text
- decide on whether to sent telemetry data to Red Hat
- Run Setup


## Start
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

## Access 
Access the web console
```
crc console
```

Log in as the developer user with the password printed in the output of the crc start command. You can also view the password for the developer and kubeadmin users by running the following command: 
```
crc console --credentials
```

## OpenShift CLI
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

## Configure Registry Access in OpenShift Local
Go to the console as kubeadmin and configure the OpenShift Local cluster to accept images from external registries.

Go to Overview | Details | View Settings | Configuration | edit `Image' YAML
```
spec:
  additionalTrustedCA:
    name: registry-certs
  allowedRegistriesForImport:
    - domainName: quay.io
      insecure: false
  registrySources:
    allowedRegistries:
      - quay.io
      - registry.redhat.io
      - 'image-registry.openshift-image-registry.svc:5000'
status:
  externalRegistryHostnames:
    - default-route-openshift-image-registry.apps-crc.testing
  internalRegistryHostname: 'image-registry.openshift-image-registry.svc:5000'
```