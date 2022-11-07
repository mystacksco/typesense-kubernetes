# typesense-kubernetes


This repo hosts kustomize files for deploying typesense in a kubernetes cluster.


## Quickstart

> kubectl apply -f https://raw.githubusercontent.com/typesense/typesense-kubernetes/master/base/install.yaml
## Detailed setup:

1. Clone the repo

> git clone https://github.com/typesense/typesense-kubernetes


2. modify the overlays/dev/kustomization.yaml file according to your needs



Run below command:

To install

> kustomize build overlays/dev | kubectl apply -f - 

Clean up

> kustomize build overlays/dev | kubectl delete -f - 

## TROUBLESHOOTING

1. After `kubectl apply`, cluster will not respond to requests.  Logs show something like 

```
│ W20221107 17:03:45.009104  139 node.cpp:1494] node default_group:192.168.96.24:8107:8108 can’t do pre_vote as it is not in 192.168.117.33:8107:8108    │               │
│ I20221107 17:03:47.479279  131 raft_server.cpp:565] Term: 9, last_index index: 681522, committed_index: 0, known_applied_index: 681517, applying_index: 0 │               │
│ W20221107 17:03:47.479300  131 raft_server.cpp:593] Multi-node with no leader: refusing to reset peers.
```

Solution: Scale # replicas down to 1 in overlays/dev/kustomization.yaml and apply the configuration.  The new single node should be responsive.  After, you should be able to scale back up to 3 nodes.




