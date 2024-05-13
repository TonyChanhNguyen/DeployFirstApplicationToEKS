---
title : "Cleanup resources"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---

### Clean up EKS Cluster
1. Execute the command below to delete EKS Cluster
```
eksctl delete cluster --name my-fcj-cluster --region ap-southeast-1
```

![Clean up resources](../images/7.cleanup/7.1.cleanup.png?pc=90pt)

{{% notice info %}}
It will take you about 20 minutes to delete.
{{% /notice %}}


### Delete Cloud9 Workspace
1. Go to [Cloud9](https://ap-southeast-1.console.aws.amazon.com/cloud9control/home?region=ap-southeast-1#/).
2. Select **FCJ-Workspace**.
3. Click on **Delete**.

![Clean up resources](../images/7.cleanup/7.3.cleanup.png?pc=90pt)

4. Input ```Delete``` to confirm.
5. Click on **Delete**.
![Clean up resources](../images/7.cleanup/7.4.cleanup.png?pc=90pt)


### Delete IAM Role.
1. Go to [IAM Role](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles).
2. Search IAM Role named ```eksworkspace-administrator```.
3. Select IAM Role.
4. Click on **Delete**.
![Clean up resources](../images/7.cleanup/7.5.cleanup.png?pc=90pt)

5. Input the IAM Role's name ```eksworkspace-administrator``` to confirm.
6. Click on **Delete**.
![Clean up resources](../images/7.cleanup/7.6.cleanup.png?pc=90pt)