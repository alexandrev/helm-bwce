# bwce

This chart allows you to create/configure/manage TIBCO BusinessWorks Container Edition application atop Kubernetes. This chart includes multiple components and is suitable for a variety of use-cases.



## TL;DR;

```console
$ helm install ./stable/bwce --generate-name
```

## Introduction

This chart bootstraps a TIBCO BusinessWorks Container Edition application deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.  The chart can be installed multiple times to create separate application .

## Prerequisites
  - Kubernetes 1.10+ with Beta APIs
  - Helm 2.12+ 

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install my-release ./stable/bwce
```

The command deploys the application on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.



## Configuration

The following tables list the configurable parameters of the bwce chart and their default values.

### General
| Parameter | Description | Default |
| ----- | ----------- | ------ |
| replicaCount                      | Number of replicas of the current deployment                 | 1                                                            |
| image.repository                  | Docker image location inside the Docker Repository of use    | 552846087011.dkr.ecr.eu-west-2.amazonaws.com/tibco/bwce      |
| image.tag                         | Docker image tag                                             | 2.5.3                                                        |
| image.pullPolicy                  | Docker image pull policy                                     | Always                                                       |
| image.imagePullSecrets            | Secret name to use for the pull process                      | regcred                                                      |
| env                               | Environment variables to be added to the deployment          |                                                              |
| istio.enable                      | Flag to enable the use of istio as part of the deployment    | true                                                         |
| service.name                      | Name of the service to be created as part of the deployment  | bwce                                                         |
| service.type                      | Service Type to be created as part of the deployment         | ClusterIP                                                    |
| service.externalPort              | External port to be configured as part of the deployment     | 8080                                                         |
| service.internalPort              | Internal port to be configured as part of the deployment     | 8080                                                         |
| service.annotations               | Additional annotation to be added at the service level       |                                                              |
| resources.limits.cpu              | CPU limit for the deployment                                 | 500m                                                         |
| resources.limits.memory           | Memory limit for the deployment                              | 512Mi                                                        |
| resources.requests.cpu            | CPU request for the deployment                               | 400m                                                         |
| resources.requests.memory         | Memory request for the deployment                            | 512Mi                                                        |
| probePath.httpGet                 | Probe Path endpoint URI                                      | /_ping                                                       |
| probePath.port                    | Probe Path port                                              | 7777                                                         |
| livenessProbe.initialDelaySeconds | Initial delay of seconds to take in account when configure the livenessProbe | 60                                                           |
| livenessProbe.periodSeconds       | Period of seconds to check the livenessProbe                 | 30                                                           |
| livenessProbe.successThreshold    | Minimum consecutive successes for the probe to be considered successful after having failed. | 1                                                            |
| livenessProbe.timeoutSeconds      | Number of seconds after which the probe times out            | 1                                                            |
| readinessProbe.periodSeconds       | Period of seconds to check the readinessProbe                 | 30                                                           |
| readinessProbe.successThreshold    | Minimum consecutive successes for the probe to be considered successful after having failed. | 1                                                            |
| readinessProbe.timeoutSeconds      | Number of seconds after which the probe times out            | 1                                                            |
| bwce.configmap.enable             | Flag to enable the configuration using config map            | true                                                         |
| bwce.configmap.name               | Default name of the config map to configure the application  | bwce-configmap                                               |
| bwce.loglevel                     | ** This configuration is only used if configmap is disabled ** | ERROR                                                        |
| bwce.javaopts                     | ** This configuration is only used if configmap is disabled ** |                                                              |
| bwce.javagcopts                     | ** This configuration is only used if configmap is disabled ** |                                                              |
| bwce.bwprofile                    | BusinessWorks profile to be used during the startup of the application | default                                                      |
| bwce.configprofile                | BusinessWorks Config profile to be used during the startup of the application | docker                                                       |
| bwce.monitoring.enable            | Enable Prometheus monitoring support                         | true                                                         |
| bwce.opentracing.enable           | Enable Opentracing integration using Jaeger                  | true                                                         |
| bwce.opentracing.javaopts         | Additional JVM options needed for Opentracing purposes       | -Dbw.monitor.batchsize=1 -Dbw.monitor.publishtimer=1500 -Dbw.engine.opentracing.enable=true |

