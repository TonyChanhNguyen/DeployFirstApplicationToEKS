---
title : "Deploy application to EKS Cluster Fargate"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 6.3 </b> "
---


### Deploy application
1. At Cloud9 Terminal, create the directories **01.fargate-profile** and **02.application**.
```
mkdir 01.fargate-profile 02.application
ls
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.1.fargateprofile.png?pc=90pt)

2. Move 2 manifest files to directory **02.application**.
```
mv 01.mybasicapp-deployment.yaml 02.application/
mv 02.mybasicapp-service.yaml 02.application/
ls 02.application/
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.2.fargateprofile.png?pc=90pt)
3. Now, let list all files and directories on **kube-manifest**.
```
ls
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.3.fargateprofile.png?pc=90pt)
It includes 2 directories **01.fargate-profile** and **02.application**. Two manifest files **01.mybasicapp-deployment.yaml** and **02.mybasicapp-service.yaml** are inside **02.application**.

4. Create the files named **fargate-profiles.yaml** on **01.fargate-profile**.
```
touch 01.fargate-profile/fargate-profiles.yaml
ls 01.fargate-profile
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.4.fargateprofile.png?pc=90pt)

5. Created the files named **00.namespace.yaml** on **02.application**.
```
touch 02.application/00.namespace.yaml
ls 02.application
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.5.fargateprofile.png?pc=90pt)

6. Open **fargate-profiles.yaml** and paste the code below. Then save it.
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: my-fcj-cluster  # Name of the EKS Cluster
  region: ap-southeast-1
fargateProfiles:
  - name: fp-fcj
    selectors:
      # All workloads in the "ns-fcj" Kubernetes namespace will be
      # scheduled onto Fargate:      
      - namespace: ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.6.fargateprofile.png?pc=90pt)

7. Open **00.namespace.yaml** and paste the code below. Then save it.
```
apiVersion: v1
kind: Namespace
metadata: 
  name: ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.9.fargateprofile.png?pc=90pt)

Now, we need to add the **Namespace** parameter to **Deployment** and **Service** manifest files.

8. Open **01.mybasicapp-deployment.yaml** and add ```namespace: ns-fcj``` inside **metadata** and same level with **name** and **labels**. Then save it.
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.7.fargateprofile.png?pc=90pt)

9. Open **02.mybasicapp-service.yaml**, add ```namespace: ns-fcj``` inside **metadata** - same level with **name** and **labels** and replace **Type** from **LoadBalancer** to **NodePort**. Then save it.
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.8.fargateprofile.png?pc=90pt)

10. At **kube-manifest** directory, execute those command to create Fargate Profile.
```
eksctl create fargateprofile -f 01.fargate-profile/fargate-profiles.yaml
``` 
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.10.fargateprofile.png?pc=90pt)

11. List Fargate Profiles.
```
eksctl get fargateprofile --cluster my-fcj-cluster
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.11.fargateprofile.png?pc=90pt)

12. At **kube-manifest** directory, execute those command to deploy application to EKS Cluster.
```
kubectl apply -Rf 02.application
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.12.fargateprofile.png?pc=90pt)
13. List all resources
```
kubectl get all -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.13.fargateprofile.png?pc=90pt)

14. List the nodes and see the result.
```
kubectl get nodes -o wide
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.14.fargateprofile.png?pc=90pt)

There is a fargate instance appeared, but it do not have the **EXTERNAL-IP**. Since fargate instance is allocated in Private Subnet, so we can not access to application publicly. Therefore if you want to access to application deployed on fargate instance, let create an Ephemeral Pod with Curl image to test the application.

15. We need to get the Private IP Address of application Pod at the IP field.
```
kubectl describe pod <Pod-NAME> -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.15.fargateprofile.png?pc=90pt)

In this case, the Private IP Address of application Pod is **192.168.78.227**.

16. Run the below command to deploy a Curl Ephemeral Pod.
```
kubectl run mycurlpod -n ns-fcj --image=curlimages/curl -i --tty -- sh
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.16.fargateprofile.png?pc=90pt)
17. Using Curl command to access to your application. Replace with the Private IP Address of your Pod.
```
curl http://<REPLACE-WITH-PRIVATE-IP>:8080
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.17.fargateprofile.png?pc=90pt)

The Curl Ephemeral Pod got content of your application.

18. Command ```exit``` to quit.
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.18.fargateprofile.png?pc=90pt)

19. List all created Pod.
```
kubectl get pod -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.19.fargateprofile.png?pc=90pt)

20. Delete the Ephemeral Pod.
```
kubectl delete pod mycurlpod -n ns-fcj
kubectl get pod -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.20.fargateprofile.png?pc=90pt)

The Curl Ephemeral Pod was deleted.

### Clean up
1. Delete all created resources.
```
kubectl delete -Rf 02.application
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.21.fargateprofile.png?pc=90pt)

2. List all resource.
```
kubectl get all -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.22.fargateprofile.png?pc=90pt)

3. Delete the Fargate Profile.
```
eksctl delete fargateprofile --cluster my-fcj-cluster --name fp-fcj --region ap-southeast-1 --wait
```
![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.23.fargateprofile.png?pc=90pt)

4. It will take you about 5 minutes to delete Fargate Profile successfully.

![Amazon EKS Cluster Fargate Profile](../../images/6.deployapptoeks/6.3.fargateprofile/6.3.24.fargateprofile.png?pc=90pt)