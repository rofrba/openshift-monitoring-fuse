- Monitor

oc process -f {$templates-base-url}/fuse-servicemonitor.yml -p NAMESPACE=<YOUR NAMESPACE> FUSE_SERVICE_NAME=<YOUR FUSE SERVICE> | oc apply -f -