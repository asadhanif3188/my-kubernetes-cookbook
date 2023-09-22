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



-------------------------
<!-- 
## Task 03

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
## Task 04

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

