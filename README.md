# Ansible CI/CD with Tekton


## Download and install Tetkon and oc client

[Tekton](https://tekton.dev/docs/cli/)

or all via question mark item in the OpenShift Webconsole -> Command line tools



## Create the pipeline

First create a namespace


```sh
oc new-project my-pipeline
```

### Install all tasks

```sh
oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/task-controller-job.yaml

oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/task-ansible-lint.yaml 

oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/task-git-merge.yaml  

oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/task-pull-request.yaml
```

### Create the pipeline with the defined tasks above

```sh
oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/pipeline-ansible-pipeline.yaml  
```

### Create Triggers and EventListener

```sh
oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/triggerbinding-ansible-pipeline-triggerbinding.yaml

oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/triggertemplate-ansible-pipeline.yaml     

oc create -f https://raw.githubusercontent.com/pmumenthaler/ansible-tekton-cicd/main/eventlistener-ansible-pipeline.yaml  

```

### expose service
```sh
oc expose svc/el-ansible-pipeline
```
