# Kubernetes Infrastructure for Jenkins Pipeline

This repository provides a Kubernetes script that allows you to create a Kubernetes infrastructure tailored for running a Jenkins pipeline. The script deploys a Jenkins master instance within a Kubernetes namespace, along with necessary service accounts and role bindings.

## Usage

To create the Kubernetes infrastructure for the Jenkins pipeline, follow these steps:

1. Apply the script by executing the following command:

   ```shell
   kubectl apply -f kubernetes-script.yaml
   ```

   This will create the Jenkins namespace, service account, cluster role binding, deployment, and service.

2. Once the infrastructure is deployed, access the Jenkins instance by connecting to the Jenkins service's external IP or by using port forwarding. Use the following command for port forwarding:

   ```shell
   kubectl port-forward -n jenkins svc/jenkins-service 8080:80
   ```

   This will forward local port 8080 to the Jenkins service running on port 80.

3. Open a web browser and visit `http://localhost:8080` to access the Jenkins web interface.

4. Follow the on-screen instructions to set up Jenkins and configure the required plugins.

5. With Jenkins up and running, you can define your pipeline jobs using Jenkinsfile and configure them as needed to automate your CI/CD processes.

## Example Kubernetes Script

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: jenkins

---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: jenkins
  namespace: jenkins

---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: jenkins
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: jenkins
  namespace: jenkins

---
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: jenkins-deployment
  namespace: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins-master
  template:
    metadata:
      labels:
        app: jenkins-master
    spec:
      serviceAccountName: jenkins
      containers:
      - name: jenkins-master
        image: jenkins/jenkins:lts-jdk11
        ports:
        - containerPort: 8080

---
apiVersion: v1
kind: Service
metadata:
  name: jenkins-service
  namespace: jenkins
spec:
  selector:
    app: jenkins-master
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

This Kubernetes script defines the necessary resources for deploying a Jenkins master instance on Kubernetes. It creates a dedicated namespace, service account, cluster role binding, deployment, and service.

## Resources

For more information on setting up a CI/CD pipeline with Kubernetes and Jenkins, refer to the following resources:

- [Create A CI/CD Pipeline With Kubernetes and Jenkins](https://www.weave.works/blog/create-a-cicd-pipeline-with-kubernetes-and-jenkins)
- [Continuous Integration with Jenkins on Kubernetes](https://piotrminkowski.com/2020/11/10/continuous-integration-with-jenkins-on-kubernetes)
- [CI/CD Pipeline with Jenkins and Kubernetes | Medium](https://narsimhulu-464.medium.com/ci-cd-pipeline-with-jenkins-and-k8s-part-1-10c4d603c4c5)

Feel free to explore and adapt this Kubernetes infrastructure script to fit your specific