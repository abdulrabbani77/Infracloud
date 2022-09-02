**Assignment- Part-A - Setup the cluster**

[osboxes@osboxes boutique-assignment]$ kubectl get nodes</br>
NAME &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;                   STATUS&emsp;&emsp;&emsp;  ROLES &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;  AGE &emsp;&emsp;&emsp;  VERSION</br>
qa-cluster-control-plane&emsp;&emsp;Ready   &emsp;&emsp;&emsp; control-plane,master  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; 5m4s  &emsp;&emsp;&emsp; v1.20.7</br>
qa-cluster-worker   &emsp;&emsp;&emsp;&emsp;&emsp;Ready &emsp;&emsp;&emsp;   <none>    &emsp;&emsp;&emsp;&emsp;&emsp;&emsp; &emsp;&emsp;&emsp;&emsp;            4m1s &emsp;&emsp;&emsp; &emsp;  v1.20.7</br>
[osboxes@osboxes boutique-assignment]$


**Assignment- Part-B - Deployment Issues**

1. Issue  : redis-cart pod was in pending state
   Reason : 1 node(s) didn't match Pod's node affinity, 1 node(s) had taint {node-role.kubernetes.io/master: }, that the pod didn't tolerate.
            Since there are only two nodes and one of them is control node, so I have proceeded with choosing another node
   Fix    : Edited the "redis-cart.yaml" deployment file with correct NodeSelector value which is "qa-cluster-worker".
            command used to apply the modified changes - "kubectl apply -f redis-cart.yaml"
   
2. Issue  : adservice pod was in CrashLoopBackOff 
   Reason : It is unable to pull and unpack the image "gcr.io/google-samples/microservices-demo/adservice:v0.3.1" becuase there is no such version (v0.3.1)  available at gcr.io/google-samples/microservices-demo/adservice
   Fix    : Edited the "adservice.yaml" deployment file with image version, modified from v0.3.1 to v0.3.9. 
            command used to apply the modified changes - "kubectl apply -f adservice.yaml"
  
3. Issue  : recommendationservice pod was not deployed 
   Reason : Deployment was not initiated because there is an issue with serviceAccountName in deployment file.
   Fix    : Edited the "recommendationservice.yaml" deployment file with serviceAccountName to default from boutique.
            command used to apply the modified changes - "kubectl apply -f recommendationservice.yaml"
		   
**Assignment- Part-C - Application Issues**

1. port-forward
2. modified currencyservice port to 7000 in currency deployment file
3. load balancer added

Unable to access the application.

https://developers.google.com/accounts/docs/application-default-credentials
project ID must be specified in the configuration if running outside of GCP





















