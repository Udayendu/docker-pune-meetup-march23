# Changelog
- Kubernetes Cluster deployment using Ansible, Docker & Jenkins
- This deployment will setup a Kubernetes Cluster of:
  - Master Node: 1
  - Worker Nodes: 3

![k8d-deployment-diagram](https://user-images.githubusercontent.com/1809177/221905263-ed62dbde-7983-46f8-ad0d-fb490dc168eb.png)


## [v1.0] - 01-03-2022 (dd-mm-yyyy)

### Added
  - Ansible Roles for:
    - VM Management:
      - vmdeploy
      - gocustom
      - vmdelete
    - VM Snapshot Management:
      - vmsnapshot
      - vmsnapshotrevert
      - vmsnapshotremove
    - Kubernetes Cluster Management:
      - mastersetup
      - nodesetup
      - nodelabel

### Software support
  - alpine: 3.17
  - ansible: 7.1.0
  - ansible-core: 2.14.1
  - pyvmomi: 7.0.3
  - vSphere-Automation-SDK: 1.71.0

### Kubernetes Packages:
  - cri-o:   1.24.4
  - kubelet: 1.26.1
  - kubeadm: 1.26.1
  - kubectl: 1.26.1

### Jenkins file name
  - Jenkinsfile

### Dockerfile
  - alpinedevops.dockerfile

## Docker image build process
- To build the docker image, use the below command:
  
  > $ docker build --no-cache=true -f <file_name>.dockerfile -t <docker_registry>/alpinedevops:latest

- To login to the hub.docker.com, use the below command:

  > $ docker login

- To push the docker image, use the below command:

  > $ docker push <docker_registry>/alpinedevops:latest

## Deployment Guide:

### VM Management
- To deploy the linux server, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "deploy"

- To do the guest os customization, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "oscustom"

- To delete the linux server use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "delete"

### VM Snapshot Management
- To take the vm snapshots, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "vmsnapshot"

- To revert the vm snapshot, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "vmsnapshotrevert"

- To remove the vm snapshot, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "vmsnapshotremove"

### Kubernetes Cluster Management
- To deploy & configure the kubernetes master, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "mastersetup"

- To deploy & configure the kubernetes worker nodes, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "nodesetup"

- To label the kubernetes worker nodes, use the below command:

  > ansible-playbook -i inventory containerlab.yaml --tags "nodelabel"
