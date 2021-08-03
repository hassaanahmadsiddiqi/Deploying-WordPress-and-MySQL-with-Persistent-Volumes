# Deploying-WordPress-and-MySQL-with-Persistent-Volumes
This tutorial shows you how to deploy a WordPress site and a MySQL database using Minikube or Kubectl. Both applications use PersistentVolumes and PersistentVolumeClaims to store data.

=>Before you begin:
You need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster.
At least two nodes that are not acting as control plane hosts.

=>Download the following configuration files:
mysql-deployment.yaml
wordpress-deployment.yaml

=>Create a kustomization.yaml:

```
cat <<EOF >./kustomization.yaml
secretGenerator:
- name: mysql-pass
  literals:
  - password=password
EOF
```


=>Add other YAML file to kustomization.yaml file.
```
cat <<EOF >>./kustomization.yaml
resources:
  - mysql-deployment.yaml
  - wordpress-deployment.yaml
EOF
```

  
=>Apply and Verify
```
kubectl apply -k ./
kubectl get secrets
kubectl get pvc
kubectl get pods
kubectl get services wordpress
```

=>Yes..All done..!
Copy the IP address of worker and port of ClusterIP , and load the page in your browser to view your site. ie. WorkerNodeIp:ClusterIPPort
You should see the WordPress set up page on your browser.
  
