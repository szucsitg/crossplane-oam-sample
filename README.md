This repo is now deprecated, as you can install from [OAM Kubernetes Runtime](https://github.com/crossplane/oam-kubernetes-runtime#install-oam-runtime).

# Crossplane OAM Sample

This repo is for quick and simple demo to show how OAM works on version v1alpha2,
it will finally move to [Crossplane Org](https://github.com/crossplane/) after
everything is prepared.

## Install Crossplane and OAM

Crossplane can be easily installed into any existing Kubernetes cluster using
the regularly published Helm chart. The Helm chart contains all the custom
resources and controllers needed to deploy and configure Crossplane.

Crossplane and OAM all in one.

## Pre-requisites

* [Kubernetes cluster](https://kubernetes.io/docs/setup/)
  * For example
    [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/),
    minimum version `v0.28+`
* [Helm 3](https://helm.sh/docs/intro/), minimum version `v3.0.0+`.


## Installation

```console
helm repo add oam https://oam-dev.github.io/crossplane-oam-sample/archives/
kubectl create namespace oam-system
helm install crossplane --namespace oam-system oam/crossplane-oam
```

## Try Sample OAM AppConfig

```
$ kubectl apply -f samples/sample_application_config.yaml
component.core.oam.dev/example-component created
applicationconfiguration.core.oam.dev/example-appconfig created
```

You will get containerized workload and manual scaler trait.

```
$ kubectl get manualscalertraits.core.oam.dev
NAME                      AGE
example-appconfig-trait   4s
```

```
$ kubectl get containerizedworkloads.core.oam.dev
NAME                         AGE
example-appconfig-workload   58s
```

And you will get a K8s deployment as real running resource.

```
$ kubectl get deploy
NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
example-appconfig-workload-deployment   3/3     3            3           114s
```
