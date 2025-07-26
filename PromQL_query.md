In the Opeshift 
Openshift Console > Observe > Metrics - You'll see the promql editor and graph area.
(***note: change the namespace name according to you;***)

Cpu usage per pod  
```
rate(container_cpu_usage_seconds_total{namespace="your-namespace"}[5m])
or 
sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{namespace='pritam-03-dev'}) by (pod)
```

Memory usage  
```
container_memory_usage_bytes{namspace="your-namespace"}
or
sum(container_memory_working_set_bytes{container!="", namespace='pritam-03-dev'}) by (pod)
```

Pod restarts 
```
kube_pod_container_status_restarts_total{namspace="your-namespace"}
```

Network I/O 
```
container_network_receive_bytes_total{namespace="your-namespace"}
```
file system usage
```
topk(25, sort_desc(sum(pod:container_fs_usage_bytes:sum{container="",pod!="",namespace='pritam-03-dev'}) BY (pod, namespace)))
```
Receive bandwidth
```
sum(irate(container_network_receive_bytes_total{namespace='pritam-03-dev'}[2h])) by (pod)
```
Transmit Bandwidth
```
sum(irate(container_network_transmit_bytes_total{namespace='pritam-03-dev'}[2h])) by (pod)
```
Rate of received packets
```
sum(irate(container_network_receive_packets_total{namespace='pritam-03-dev'}[2h])) by (pod)
```
Rate of transmitted packets
```
sum(irate(container_network_transmit_packets_total{namespace='pritam-03-dev'}[2h])) by (pod)
```
Rate of received packets dropped
```
sum(irate(container_network_receive_packets_dropped_total{namespace='pritam-03-dev'}[2h])) by (pod)
```
Rate of transmitted packets dropped
```
sum(irate(container_network_transmit_packets_dropped_total{namespace='pritam-03-dev'}[2h])) by (pod)
```
