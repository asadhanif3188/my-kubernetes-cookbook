# Kubernetes - Practice Tasks
Following are the practice tasks of Kubernetes along with their solutions. 

## Task 01 - Creating Simple Pods 

### Part A

Create a pod named pod-httpd using httpd image with latest tag only and remember to mention the tag i.e httpd:latest.
Labels app should be set to httpd_app, also container should be named as httpd-container.

#### Solution:

**Declarative** 

```
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
  labels:
    app: httpd_app
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    ports:
    - containerPort: 80
```

### Part B
Create a pod named pod-nginx using nginx image with latest tag only and remember to mention the tag i.e nginx:latest.
Labels app should be set to nginx_app, also container should be named as nginx-container.

#### Solution:

**Declarative** 

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx_app
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```
-------------------------
## Task 02 - Creating Simple Deployments 

### Part A

The ABC DevOps team has started practicing some pods and services deployment on Kubernetes platform, as they are planning to migrate most of their applications on Kubernetes. Recently one of the team members has been assigned a task to create a deployment as per details mentioned below:

Create a deployment named *httpd* to deploy the application *httpd* using the image *httpd:latest* (remember to mention the tag as well).

#### Solution:

**Imperative**

```
kubectl create deployment httpd --image=httpd:latest --dry-run=client -o yaml
kubectl create deployment httpd --image=httpd:latest 
```

**Declarative** 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: httpd_app
  name: httpd
spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpd_app
  template:
    metadata:
      labels:
        app: httpd_app
    spec:
      containers:
      - image: httpd:latest
        name: httpd
```

### Part B
Create a deployment named *nginx-deployment* to deploy the application *nginx* using the image *nginx:latest*.

#### Solution:

**Imperative**

```
kubectl create deployment nginx-deployment --image=nginx:latest --dry-run=client -o yaml
kubectl create deployment nginx-deployment --image=nginx:latest 
```

**Declarative** 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx_app
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx_app
  template:
    metadata:
      labels:
        app: nginx_app
    spec:
      containers:
      - image: nginx:latest
        name: nginx
```

### Part C

Create a Kubernetes Deployment named *web-app* using the *nginx* image with *three replicas*. Ensure the deployment has labels like *app: web* and *tier: frontend*.
#### Solution:

Generate a sample deployment file using followng command and update labels in the file: 

```
kubectl create deployment web-app --image=nginx:latest --replicas=3 --dry-run=client -o yaml > web-app-deployment.yaml
```
Final deployment file: 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: web
    tier: frontend
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
      tier: frontend
  template:
    metadata:
      labels:
        app: web
        tier: frontend
    spec:
      containers:
      - image: nginx:latest
        name: nginx
```


-------------------------

## Task 03 - Create Namespaces
Create a namespace named dev and create a POD under it; name the pod dev-nginx-pod and use nginx image with latest tag only and remember to mention tag i.e nginx:latest.

#### Solution:

Creating Namespace

**Imperative**

```
kubectl create namespace dev
```

**Declarative** 

```
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

Creating Pod

**Declarative** 

```
apiVersion: v1
kind: Pod
metadata:
  name: dev-nginx-pod
  namespace: dev
  labels:
    app: nginx_app
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```


-------------------------

## Task 04 - Set Limits for Resources in Kubernetes

Recently some of the performance issues were observed with some applications hosted on Kubernetes cluster. The Nautilus DevOps team has observed some resources constraints, where some of the applications are running out of resources like memory, cpu etc., and some of the applications are consuming more resources than needed. Therefore, the team has decided to add some limits for resources utilization. Below you can find more details.

Create a pod named `httpd-pod` and a container under it named as `httpd-container`, use `httpd` image with `latest` tag only and remember to mention tag i.e `httpd:latest` and set the following limits:
- Requests: Memory: `15Mi`, CPU: `100m`
- Limits: Memory: `20Mi`, CPU: `100m`

#### Solution:

**Declarative** 

```
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
  labels:
    app: httpd_app
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    ports:
    - containerPort: 80
    resources:
      requests:
        cpu: "100m"
        memory: "15Mi"
      limits:
        cpu: "100m"
        memory: "20Mi"
```

Describe the pod

```
kubectl describe pod httpd-pod 
```

Output:

```
Name:             httpd-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             kodekloud-control-plane/172.17.0.2
Start Time:       Wed, 27 Sep 2023 10:28:16 +0000
Labels:           app=httpd_app
Annotations:      <none>
Status:           Running
IP:               10.244.0.5
IPs:
  IP:  10.244.0.5
Containers:
  httpd-container:
    Container ID:   containerd://b8e888e04878c822ac2ad7b7c11912572c3541d2ce2445d70b8d471d139f2999
    Image:          httpd:latest
    Image ID:       docker.io/library/httpd@sha256:5123fb6e039b83a4319b668b4fe1ee04c4fbd7c4c8d1d6ef843e8a943a9aed3f
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 27 Sep 2023 10:28:26 +0000
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     100m
      memory:  20Mi
    Requests:
      cpu:        100m
      memory:     15Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-q2npz (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-q2npz:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  30s   default-scheduler  Successfully assigned default/httpd-pod to kodekloud-control-plane
  Normal  Pulling    29s   kubelet            Pulling image "httpd:latest"
  Normal  Pulled     21s   kubelet            Successfully pulled image "httpd:latest" in 7.907490156s (7.907512558s including waiting)
  Normal  Created    21s   kubelet            Created container httpd-container
  Normal  Started    20s   kubelet            Started container httpd-container
```

-------------------------
<!-- 
## Task 05

#### Solution:

**Imperative**

```
```

**Declarative** 

```
```

 -->

-------------------------
<!-- 
## Task 06

#### Solution:

**Imperative**

```
```

**Declarative** 

```
```

 -->

