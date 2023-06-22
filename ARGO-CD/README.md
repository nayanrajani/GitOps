# Argo CD

## Reference

- https://youtu.be/MeU5_k9ssrs
- https://www.opsmx.com/what-is-argocd/
- https://argo-cd.readthedocs.io/en/stable/
- https://github.com/argoproj/argo-cd [projects]
- https://developer.redis.com/operate/continuous-integration-continuous-deployment/argocd/ 
- https://medium.com/geekculture/argo-cd-a-tool-for-kubernetes-devops-c46f2881edfe [IMP]
- https://www.digitalocean.com/community/tutorials/how-to-deploy-to-kubernetes-using-argo-cd-and-gitops
- https://redhat-scholars.github.io/argocd-tutorial/argocd-tutorial/index.html [Trusted]


### Best practice

- Separate Git repo for Application Source Code and Application Configuration (K8s Manifest file)
- Even Separate git repos for system configuration

### What is Argo CD

- Argo CD is Continous Delivery Tool.

### CD WorkFlow Without Argo CD

- Let's say we are running Microservices in Kubernetes

- CI
  - When you update the code and push to branch
  - then Jenkins pull the code for CI Pipeline
  - build the code and test the code
  - and push the Docker Image in Docker Hub

- How does it get deployed on K8s Cluster?
  - update K8S Deployment file with new image tag
  - apply file in K8s

- CD
  - Jenkins will update the file
  - using tool it will apply in K8s

- challenges with this approach
  - you need to install tools like kubectl helm etc on jenkins to apply the changes
  - Configure Access to K8s
  - Configure Access to cloud Platform
  - Security Challenges
  - No Visibility after the Deployment of changes.

### How Does ARGO CD make the process mode efficient?

- Reverse Flow
  - ArgoCD is a part of K8s Cluster
  - ArgoCD agent pulls K8s Manifest Changes and Applies them

- K8s manifest can be defined in different ways
  - argo supports
    - Kubernets YAML Files
    - Helm Charts
    - Kustomize

- Spliting CI and CD
  - We have now splitted CI and CD
    - CI is Manged by Developers/DevOps
      - jenkins, repo and all
    - CD is managed by Operations/Devops
      - K8s and ArgoCD

### Benefits of ArgoCD

- Whole K8s Configuration defined as code in GIT repo
- Config Files are nt Applied manually from local laptops
- Same Interface for updating the cluster

- What happens when people updates the cluster manually?
  - ArgoCD Watches the changes in the cluster as well.
  - ArgoCD comapres desired config files in the git repo with the actual state in the K8s Cluster.
  - ArgoCD will detect the diverged
  - ArgoCD will sync the changes, Overwriting the manual change to the desired repo state.

- If there is an Urgent requirement to change the app directly?
  - then you can set the ArgoCD to not sync manual cluster changes automatically.
  - send alert for manual changes.

### Easy Rollback

- Instead of Imperative approach we will follow decalarative approach
- ArgoCD automatically rollback the previous state if something goes wrong

### Cluster Disaster Recovery

- If using EKS Cluster then we can easily roll back to the new region if the current region is down, by just pointing the files repo to new region.

### K8S Access Control with Git & Argo CD

- Without ArgoCD
  - By Allowing only higher authority to merge the code into the main branch
  - rest of the people can create a pull request only
  - Mange cluster access indirectly with Git
  - No need to create CLuster roles or User in Cluster

- With ArgoCD
  - you don't need to give any external access to the user
  - argo will take care of latest change pull
  - no cluster credential required.

### Argo CD as a extension

- Argo CD uses Existing K8s Functionalities
- e.g etcd to store data
- e.g using K8s Controllers for monitoring and comparing actual vs desired state.
- benefit
  - Visibility in the cluster
    - real time update of application state.

### Configure Argo CD

- Deploy ArgoCD into K8s Cluster
  - Extends the K8s API with Custom Resource Definition
- Configure ArgoCD with K8s Yaml File
  - main resources is application
    - which git repo?
    - which k8s cluster
  - logically group application

### Multiple Cluster with ArgoCD

- Configure and Manage just one ArgoCD
- Same ArgoCD Instance is able to Sunc a fleet of K8s Cluster.

- What about different environments?
  - Two Options [Not the best option]
    - Git Multiple Branch of Each Environment.
    - Using Overlays with Kustomize

### Replacement for other CI/CD tools?

- Argo will not replace the jenkins or etc kind of tool
- because we do need CI Pipeline.
- It is only replacement for CD (Continous Delivery) but specifically for K8s.
- there are other alternatives as well of ArgoCD
  - Flux
  - Jenkins X

### Demo Overview

- https://gitlab.com/nanuchi/argocd-app-config

- https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd
- https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli
- https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/