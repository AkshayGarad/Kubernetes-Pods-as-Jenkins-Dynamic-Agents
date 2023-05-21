# Kubernetes Infrastructure for Jenkins Pipeline

This repository provides an example Kubernetes script that sets up a Kubernetes infrastructure specifically designed for running a Jenkins pipeline.

## What is Kubernetes?

[Kubernetes](https://kubernetes.io/) is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It provides a reliable and scalable infrastructure for running applications in a distributed environment.

## About the Kubernetes Script

The provided Kubernetes script defines the necessary resources to create a Kubernetes infrastructure for a Jenkins pipeline. Here's a breakdown of the script:

1. **Namespace**: Creates a Kubernetes namespace called "jenkins" to isolate Jenkins resources.

2. **ServiceAccount**: Defines a service account named "jenkins" within the "jenkins" namespace.

3. **ClusterRoleBinding**: Binds the "jenkins" service account to the "cluster-admin" ClusterRole, granting it extensive permissions across the cluster.

4. **Deployment**: Deploys a Jenkins master instance within the "jenkins" namespace, using the official Jenkins Docker image.

5. **Service**: Exposes the Jenkins instance through a Kubernetes service, making it accessible on port 80.

## Getting Started

To set up the Kubernetes infrastructure for your Jenkins pipeline:

1. Apply the provided Kubernetes script to your Kubernetes cluster using the appropriate deployment mechanism (`kubectl apply -f <filename>`).

2. Verify that the Jenkins master pod is running successfully within the "jenkins" namespace.

3. Access the Jenkins UI by navigating to the exposed service endpoint on port 80.

## Resources

To learn more about running a Jenkins pipeline with Kubernetes, refer to the following resources:

- [Create A CI/CD Pipeline With Kubernetes and Jenkins](https://www.weave.works/blog/create-a-cicd-pipeline-with-kubernetes-and-jenkins)
- [Continuous Integration with Jenkins on Kubernetes](https://piotrminkowski.com/2020/11/10/continuous-integration-with-jenkins-on-kubernetes/)
- [CI/CD Pipeline with Jenkins and Kubernetes | Medium](https://narsimhulu-464.medium.com/ci-cd-pipeline-with-jenkins-and-k8s-part-1-10c4d603c4c5)

Feel free to explore and adapt the Kubernetes infrastructure to suit your specific requirements for running a Jenkins pipeline.