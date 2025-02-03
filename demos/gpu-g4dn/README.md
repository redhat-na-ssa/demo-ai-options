# How to change the GPU instance type

Build the rhoai-ready pipe to less
`kustomize build "https://github.com/redhat-na-ssa/demo-ai-gitops-catalog/demos/rhoai-workshop-ready?ref=v0.11" | less`

Search for the instance type env variable
`search for INSTANCE_TYPE`

copy the Job job-aws-gpu-machineset definition
```sh
apiVersion: batch/v1
kind: Job
metadata:
  annotations:
    argocd.argoproj.io/hook: PreSync
  generateName: job-aws-gpu-machineset-
  name: job-aws-gpu-machineset
  namespace: nvidia-gpu-operator
spec:
  template:
    metadata:
      annotations:
        argocd.argoproj.io/hook: PreSync
    spec:
      containers:
      - command:
        - /bin/bash
        - -c
        - /scripts/job.sh
        env:
        - name: INSTANCE_TYPE
```

Edit the following rows for this yaml definition to change from 4xlarge to 12xlarge
```sh
apiVersion: batch/v1
kind: Job
metadata:
  name: job-aws-gpu-machineset
  namespace: nvidia-gpu-operator
spec:
  template:
    spec:
      containers:
      - env:
        - name: INSTANCE_TYPE
          value: g4dn.12xlarge
```

Other types:
- single gpu: g4dn.{2,4,8,16}xlarge
- multi gpu:  g4dn.12xlarge
- practical:  g4ad.4xlarge
- a100 (MIG): p4d.24xlarge
- h100 (MIG): p5.48xlarge