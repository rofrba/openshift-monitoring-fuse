# Fuse applications monitoring 

You can use **Prometheus** to monitor and store **Fuse on OpenShift** data by exposing endpoints with your Fuse application’s data to Prometheus format. Prometheus stores the data so that you can use a graphical tool, such as Grafana, to visualize and run queries on the data.

You can use Prometheus to monitor Fuse applications that are running on an on-premise OpenShift cluster or on a single-node cluster, such as Minishift or the Red Hat Container Development Kit.


## Setting up Prometheus

To set up Prometheus, install the Prometheus operator custom resource definition on the cluster and then add Prometheus to an OpenShift project that includes a Fuse application.


### Procedure

 1. Login to OpenShift with administrator permissions:
    ` $ oc login -u system:admin `
    
 2. Install the Prometheus operator to your namespace by using the following command syntax:
    ` $ oc process -f https://github.com/rofrba/openshift-monitoring-fuse/blob/master/templates/fuse-prometheus-operator.yml -p NAMESPACE=<YOUR NAMESPACE> | oc create -f - `

 3. Instruct the Prometheus operator to monitor the Fuse application in the project by using the following command syntax:
     ` $ oc process -f https://github.com/rofrba/openshift-monitoring-fuse/blob/master/templates/fuse-servicemonitor.yml -p NAMESPACE=<YOUR NAMESPACE> FUSE_SERVICE_NAME=<YOUR FUSE SERVICE> | oc apply -f - `
