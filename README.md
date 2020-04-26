# k3s-Logging with Elasticsearch-Metribeat-Kibana
K3S logs have to be stored in centralized location

ElasticSearch was selected as such centralized location, Kibana is used for data visualisation

Metricbeat is used as a DaemonSet to ensure we get a running metricbeat daemon on each node of the cluster.

Everything is deployed under infra namespace, you can change that by updating YAML manifests under this folder.

# Assumptions

You have a K3S environment

You have namespace created with name infra or you can make the changes in yaml files as per your namespace requirement

# Environment Setup

#### 1. Setup Elasticsearch on your k3s setup

The first node of the cluster we’re going to set up is the master which is responsible for controlling the cluster.

###### Command

$ kubectl apply -f es-master-cm.yaml -f es-master-svc.yaml -f es-master-dep.yaml

The second node of the cluster we’re going to set up is the data node that is responsible for hosting the data and executing the queries (CRUD, search, aggregation).

###### Command

$ kubectl apply -f es-data-cm.yaml -f es-data-svc.yaml -f es-data-dep.yaml

The third node client is responsible for exposing an HTTP interface and pass queries to the data node.

###### Command

$ kubectl apply -f es-client-cm.yaml -f es-client-svc.yaml -f es-client-dep.yaml
