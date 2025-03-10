---
layout: post
section-type: post
title: Getting started with consul
category: tech
tags: [ 'consul']
---

This is going to be a kata based learning,  you may just follow the simple
steps one after the other. 

As a part of this tutorial,  we will be
using homebrew, kind, kubernetes, consul

Step 1: Install homebrew

Step 2: Install kind with homebrew

```shell
brew install kind
```

Step 3: Create a kubernetes(k8s) cluster with kind

```shell
kind create cluster
```

Step 4: Install consul-k8s cli with brew
```shell
brew tap hashicorp/tap # adding hasicorp repo
brew install hashicorp/tap/consul-k8s
```

Step 5: create a values.yaml file with below configuration

```yaml
# Contains values that affect multiple components of the chart.
global:
# The main enabled/disabled setting.
# If true, servers, clients, Consul DNS and the Consul UI will be enabled.
enabled: true
# The prefix used for all resources created in the Helm chart.
name: consul
# The consul image version.
image: hashicorp/consul:1.16.0
# The name of the datacenter that the agents should register as.
datacenter: dc1
# Enables TLS across the cluster to verify authenticity of the Consul servers and
clients.
tls:
enabled: true
# Enables ACLs across the cluster to secure access to data and APIs.
acls:
# If true, automatically manage ACL tokens and policies for all Consul
components.
manageSystemACLs: true
# Exposes Prometheus metrics for the Consul service mesh and sidecars.
metrics:
enabled: true
# Enables Consul servers and clients metrics.
enableAgentMetrics: true
# Configures the retention time for metrics in Consul servers and clients.
agentMetricsRetentionTime: &quot;1m&quot;
# Configures values that configure the Consul server cluster.
server:
enabled: true
# The number of server agents to run. This determines the fault tolerance of the
cluster.
replicas: 1
# Contains values that configure the Consul UI.
ui:
enabled: true
# Defines the type of service created for the Consul UI (e.g. LoadBalancer,
ClusterIP, NodePort).
# NodePort is primarily used for local deployments.
service:
type: NodePort
# Enables displaying metrics in the Consul UI.
metrics:
enabled: true
# The metrics provider specification.
provider: &quot;prometheus&quot;
# The URL of the prometheus metrics server.
baseURL: http://prometheus-server.default.svc.cluster.local
# Configures and installs the automatic Consul Connect sidecar injector.
connectInject:
enabled: true
# Enables metrics for Consul Connect sidecars.
metrics:
defaultEnabled: true
```

Step 6: Install consul and proceed installation with y (ie., yes)

```shell
consul-k8s install -f values.yaml
```

Step 7: list all the pods in consul namespace

```shell
kubectl get pods -n consul
```

Step 8: list all the service in consul namespace

```shell
kubectl get svc -n consul
```

Step 9: Port forward the consul-ui service to access consul ui

```shell
kubectl port-forward svc/consul-ui 8501:443 -n consul
```

Step 10: Access consul UI with URL
https://localhost:8501/ui/
Step 11: Install consul agent CLI


```shell
brew tap hashicorp/tap
brew install hashicorp/tap/consul
```

Step 12: Export Tokens

```shell
export CONSUL_HTTP_TOKEN=$(kubectl get --namespace consul secrets/consul-bootstrap-
acl-token --template={{.data.token}} | base64 -d)
export CONSUL_HTTP_ADDR=https://127.0.0.1:8501
export CONSUL_HTTP_SSL_VERIFY=false
```

Step 13: Execute consul agent commands

```shell
consul catalog datacenters
consul catalog nodes
consul catalog services
```


Now that you have access to the UI and Command line to access consul, let
us deal with ***what is consul***?

Consul is an application which help in service discovery and service
configuration. It helps in automated networking between services &
applications and helps in securing the network.

We have seen how to perform a simple installation of consul in this tutorial
and seen what is consul.

At this point, I like to leave you to explore more about consul by yourself.

Happy Learning.