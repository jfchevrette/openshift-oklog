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

