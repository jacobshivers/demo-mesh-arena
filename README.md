# demo-mesh-arena

## Slides

This demo was presented at [DevopsDday](http://2018.devops-dday.com/) in the Velodrome, Marseilles' famous stadium.
[Here are the slides](https://docs.google.com/presentation/d/1PzRD3BquEI3Al6y2_vSrZqUY0AlJF54_uuWYhr81t5g), in French. Or a similar [English version](https://docs.google.com/presentation/d/1WZDmIcfzKC9GMqz8Cvcb0_mJK_hIH-JxEDROZLnEnng).

## Step-by-step

For a step-by-step walk-through, [read this](./STEP-BY-STEP.md).

## Pre-requisite

- Kubernetes or OpenShift cluster running (ex: minikube 0.27+ / minishift)
- Istio with Kiali installed
- Repo cloned locally (actually, only YML files are necessary)
- `yq` is needed, grab it from there: https://github.com/mikefarah/yq/releases (Last version known to work here: 3.1.1)

## Deploy all

Quick start, using latest version:

```bash
make deploy-latest
```

This deployment method includes runtime metrics.

More options are available in Makefile. E.g:

```bash
NAMESPACE=mesh-arena TAG=1.1.8 REMOTE=true GENTPL_OPTS="--tracing --metrics" make deploy
```

This will deploy images tagged 1.1.8 with both runtime metrics and tracing to namespace mesh-arena.

### Expose route

```bash
make expose
```

### Clean up everything

```bash
make undeploy
```

## Build the demo

For the first build, it is necessary to get the JS dependencies on your filesystem:

```bash
make prepare
```

Then build everything, with images tagged for local usage with Minikube, and deploy:

```bash
make build images deploy
```

More options are possible. E.g. to build and push to quay.io, with a specific user and tag:

```bash
OCI_USER=myself TAG=1.2.3 REMOTE=true make build images
```
