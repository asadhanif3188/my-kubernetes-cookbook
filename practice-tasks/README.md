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
## Task 02

#### Solution:

**Declarative** 

```
```

**Imperative**

```
```

-------------------------
<!-- 
## Task 03

#### Solution:

**Declarative** 

```
```

**Imperative**

```
```
 -->

