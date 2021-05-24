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
![image](https://user-images.githubusercontent.com/54719289/119391877-d94a3e00-bcc6-11eb-8019-82d2a607fb60.png)


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
# Serviceccounts:

```
kubectl get serviceaccounts

controlplane $ kubectl get serviceaccounts
NAME      SECRETS   AGE
default   1         36m

controlplane $ kubectl describe serviceaccounts default
Name:                default
Namespace:           default
Labels:              <none>
Annotations:         <none>
Image pull secrets:  <none>
Mountable secrets:   default-token-pxcq5
Tokens:              default-token-pxcq5
Events:              <none>

```

![image](https://user-images.githubusercontent.com/54719289/119395964-27ae0b80-bccc-11eb-89ab-ada81a9fad8c.png)


```

controlplane $ kubectl exec -it web-dashboard-548dff47bd-qjxsk ls /var/run/secrets/kubernetes.io/serviceaccount 

web-dashboard-548dff47bd-qjxsk  - pod name

or else

kubectl get secret

controlplane $ kubectl describe secret dashboard-sa-token-5nv9d
Name:         dashboard-sa-token-5nv9d
Namespace:    default
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: dashboard-sa
              kubernetes.io/service-account.uid: 7dc642df-0c71-49f6-85d1-0bb464adf077

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1066 bytes
namespace:  7 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IlV0Y3B1elp3cFJPZmpKUkViM1hIZ1YydHlEWjdpeXRUdXZzQmNHeXdOY1EifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRhc2hib2FyZC1zYS10b2tlbi01bnY5ZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJkYXNoYm9hcmQtc2EiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI3ZGM2NDJkZi0wYzcxLTQ5ZjYtODVkMS0wYmI0NjRhZGYwNzciLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGVmYXVsdDpkYXNoYm9hcmQtc2EifQ.OhuKyeJMd0lIjJi2OT6sM23iZvihGclSiqo6-1wwjxsjNUmVJ-rNAjEC4mLZw4rR2NW4CTcO0-5_k91NB-YZ9-qxNFms0hVUuevSdCJFGnOrc7PNDlbaQ946-VAUuwZ3DaSSofteF8xFIVe6xxL645MCEUba0UsssD8-AEHm7Kz4Krgqu1ba4gDVckUGpShc_ST7PDB5IoRidECd414knM4oi5hjuGhJEE3pajyATn5xY8YExLLM0v4Vkk3qhMuMq-WqrACookwdab4DWUHDTZjISYkiumQlXu35jIvFgt4NlRcnUZkD_BUIPhypFn7C0UlIt_T4eTKDbCBhs9xXKw 


sample dashboard-sa  rbac:  Note: dashboard-sa  created using kubectl create serviceaccount dashboard-sa
=========================

---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: ServiceAccount
  name: dashboard-sa # Name is case sensitive
  namespace: default
roleRef:
  kind: Role #this must be Role or ClusterRole
  name: pod-reader # this must match the name of the Role or ClusterRole you wish to bind to
  apiGroup: rbac.authorization.k8s.io
  
  
 dashboard-sa:
 ------------
 
 
Sample-role.yaml for pod-reader:
===============================

---
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups:
  - ''
  resources:
  - pods
  verbs:
  - get
  - watch
  - list


```
![image](https://user-images.githubusercontent.com/54719289/119401300-3a780e80-bcd3-11eb-8a89-90112bfc3d4e.png)


