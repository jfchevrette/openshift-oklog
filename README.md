This is an OpenShift deployment for [oklog](https://github.com/oklog/oklog/).

**This hasn't been tested for production use. Use at your own risk!**

# Quickstart
```
oc new-project oklog
oc create -f oklog-ingest.yaml
oc create -f oklog-store.yaml
```

If you want to expose the Web UI, you can create a route
```
oc create -f oklog-route.yaml
```

# OpenShift logs forwarder
## Logspout
This is a gliderlabs/logspout-based deployment that will ship logs from docker.

A privileged SCC is required for logspout to access the host network and processes

```
oc create -f logspout-scc.yaml
oc create -f logspout-serviceaccount.yaml

oc create -f logspout.yaml
```

# TODO
* Make the `-peer` command-line arguments dynamic somehow. Currently scaling the statefulsets require updating the peer list manually.
* Secure the /ui/ endpoint?
* Ship OpenShift logs (apiserver, controllers) from journald
* Ship OpenShift events?
* Replace logspout with a log forwarder that can
  * add openshift/k8s metadata to logs such as namespace, podname, etc...
  * output all logs as structured logs (json? fluentd?)
