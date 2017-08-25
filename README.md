# Openshift Debugging tools

I found myself installing these in containers several times.

A minimal Alpine image, with:

- `curl`
- `oc`, the OpenShift client
- `kubectl`, the Kubernetes client
- `dig` to investigate DNS entries


## Supported versions
- 3.6

## Usage

```
oc run --rm --restart=Never --ti debug --image moretea/openshift-debug-tools:$VERSION
```
