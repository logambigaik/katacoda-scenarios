# Secret:

```
   kubectl create secret generic db-secret \
           --from-literal=DB_Host=sql01 \
           --from-literal=DB_User=root \
           --from-literal=DB_Password=password123 \ 
           --dry-run=client -o yaml > db-secret.yaml
           
  apiVersion: v1
  data:
    DB_Host: c3FsMDE=
    DB_Password: cGFzc3dvcmQxMjM=
    DB_User: cm9vdA==
  kind: Secret
  metadata:
    creationTimestamp: null
    name: db-secret
    
 ```


# Docker -security:

```
   date -s '19 APR 2012 11:14:00'
   
   
   For setting date, we need to add capability in Pod.yaml,
   
   controlplane $ kubectl exec -it ubuntu-sleeper -- date -s '19 APR 2012 11:14:00'
   Thu Apr 19 11:14:00 UTC 2012
   
   ubuntu-sleeper.yaml
   
   apiVersion: v1
   kind: Pod
   metadata:
      name: ubuntu-sleeper
      namespace: default
   spec:
      containers:
         - command:
            - sleep
            - "4800"
           image: ubuntu
           name: ubuntu-sleeper
           securityContext:
             capabilities:
               add: ["SYS_TIME"]
            
 ```
