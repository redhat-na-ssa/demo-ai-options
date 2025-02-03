# demo-ai-options

Various Configurations for using OCP as an AI platform

```bash
oc login to cluster

# if ssh in and cloned
until oc apply -k demos/default ; do : ; done

# if not cloned
until oc apply -k https://github.com/redhat-na-ssa/demo-ai-options.git ; do : ; done
```