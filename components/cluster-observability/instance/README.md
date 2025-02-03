# Deploying a sample service for Cluster Observability Operator

You can monitor metrics for a service by configuring monitoring stacks managed by the Cluster Observability Operator (COO). To test monitoring a service, follow these steps:

1. Deploy a sample service that defines a service endpoint.
1. Create a ServiceMonitor object that specifies how the service is to be monitored by the COO.
1. Create a MonitoringStack object to discover the ServiceMonitor object.

```sh
# Create a YAML file named example-coo-app-service-monitor.yaml that contains the following ServiceMonitor object configuration details:

apiVersion: monitoring.rhobs/v1
kind: ServiceMonitor
metadata:
  labels:
    k8s-app: prometheus-coo-triton-server-monitor
  name: prometheus-coo-triton-server-monitor
  namespace: demo-triton
spec:
  endpoints:
  - interval: 30s
    port: 8000
    scheme: http
  selector:
    matchLabels:
      app: triton-server

# This configuration defines a ServiceMonitor object that the MonitoringStack object will reference to scrape the metrics data exposed by the prometheus-coo-example-app sample service.

# Apply the configuration to the cluster by running the following command:
oc apply -f demo-triton-service-monitor.yaml

# Verify that the ServiceMonitor resource is created by running the following command and observing the output:
oc -n ns1-coo get servicemonitors.monitoring.rhobs
```