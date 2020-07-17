# Fuse applications monitoring 

You can use **Prometheus** to monitor and store **Fuse on OpenShift** data by exposing endpoints with your Fuse application’s data to Prometheus format. Prometheus stores the data so that you can use a graphical tool, such as Grafana, to visualize and run queries on the data.

You can use Prometheus to monitor Fuse applications that are running on an on-premise OpenShift cluster or on a single-node cluster, such as Minishift or the Red Hat Container Development Kit.


## Setting up Prometheus

To set up Prometheus, install the Prometheus operator custom resource definition on the cluster and then add Prometheus to an OpenShift project that includes a Fuse application.


### Procedure

 1. Login to OpenShift with administrator permissions:
    ` $ oc login -u system:admin `
    
 2. Install the Prometheus operator to your namespace by using the following command syntax:
    ` $ oc process -f templates/fuse-prometheus-operator.yml -p NAMESPACE=<YOUR NAMESPACE> | oc create -f - `

 3. Instruct the Prometheus operator to monitor the Fuse application in the project by using the following command syntax:
     ` $ oc process -f templates/fuse-servicemonitor.yml -p NAMESPACE=<YOUR NAMESPACE> FUSE_SERVICE_NAME=<YOUR FUSE SERVICE> | oc apply -f - `

## Install Grafana

 1. Login to OpenShift with administrator permissions:
    ` $ oc login -u system:admin `
 2. Deploy oficial Grafana image
    `$ oc new-app --name grafana grafana/grafana `
 3. Create a Config Map for Grafana
    `$ oc create -f templates/grafana-configmap.yml `
 4. Mount the Config Map into Grafana container
    `$ oc set volume dc/grafana --add -t configmap -m /etc/grafana --name grafana-config --configmap-name grafana-config `

**IMPORTANT:** It's recommended to add a persistent volume mounted on /var/lib/grafana to protect the Grafana data, including users and dashboards.

In the [dashboards directory](./dashboards), there is a simple example of monitoring a Fuse service
