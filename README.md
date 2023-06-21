# GitOps

## Reference

- https://about.gitlab.com/topics/gitops/
- https://www.gitops.tech/tutorial.html
- https://www.bmc.com/blogs/gitops-cloud-native-app-delivery/
- https://docs.gitlab.com/ee/user/clusters/agent/gitops.html
- https://about.gitlab.com/blog/2022/04/07/the-ultimate-guide-to-gitops-with-gitlab/
- https://youtu.be/f5EpcWp0THw

### Introduction

- GitOps is an operational framework that takes DevOps best practices used for application development such as version control, collaboration, compliance, and CI/CD, and applies them to infrastructure automation.

### What is GitOps?

- GitOps is a IAC, Version Control, Pull Merge Request, CI/CD Pipeline.

- While much of the software development lifecycle has been automated, infrastructure has remained a largely manual process that requires specialized teams. With the demands made on today’s infrastructure, it has become increasingly crucial to implement infrastructure automation. Modern infrastructure needs to be elastic so that it can effectively manage cloud resources that are needed for continuous deployments.

- Modern and cloud native applications are developed with speed and scale in mind. Organizations with a mature DevOps culture can deploy code to production hundreds of times per day. DevOps teams can accomplish this through development best practices such as version control, code review, and CI/CD pipelines that automate testing and deployments.

- GitOps is used to automate the process of provisioning infrastructure, especially modern cloud infrastructure. Similar to how teams use application source code, operations teams that adopt GitOps use configuration files stored as code (infrastructure as code). GitOps configuration files generate the same infrastructure environment every time it’s deployed, just as application source code generates the same application binaries every time it’s built.

- it is like X as Code instead of IAAC
  - Includes:
    - IAAC
    - Network as a Code
    - Policy as a Code
    - Configuration as a Code
    - Security as a Code

### Using IAAC Wrong way

- Writing code in a local machine
- pushing code directly to the master branch with test
- No Review/Approval process
- No Code reviews
- No Collaboration
- No Automated tests

- Invalid YAML Files
- typos
- breaking Infra
- breaking app environment

### How Does GitOps Work

- IAC Hosted on Git repository
  - Version Controlled
  - Team Collaboration

- Gitops Flow
  - Create a pull request
    - do changes in the code
  - Run CI Pipeline
    - Validate Configuration files
    - run automated tested
  - Approve changes
    - tested and well reviewed
    - Code is merged in the main branch
  - After Merge run CD Pipeline
    - deployment is done

- This flow gives Automated Process, Quality Code, and More transparency.

### Types of Deployment

- Push Deployment
  - Basically out Code is push to the Production Environment to apply the changes.

- Pull Deployment
  - there is a agent which is installed in Environment like K8s Cluster, that activly pulls the changes from Git Repository itself.
  - Monitors and compares the Desired State with the Actual state.
    - if any changes, then it will pull the changes nad apply the changes to come in a desired state.
    - two example that works with this kind of CD
      - Flux CD
      - Argo CD

### Easy RollBack

- If you are pulling the code and after deployment something goes wrong then you can easliy roll back to previous working state.

### Increasing Security

- Only CD needs access to the push/pull the code like flux or argo
- Smaller Group of people only approving the code

- Less Permission to manage.
- More Secure Environment