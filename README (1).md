# Horizontal Pod Scalling 

## Create a Deployment file from github repo:

```bash 
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.7.2/components.yaml
```

```bash
kubectl edit deployment -n kube-system metrics-server
```
Puth the arguement under the container argue section 

         --kubelet-insecure-tls

 ## check the metrics pod is running with command:

 ```bash
 kubectl get deployment -n kube-system metrics-server
 ```

 ## check metrics work properly :

 ```bash
 kubectl top nodes
```
```bash
kubectl top pods
```

## Create deployment:

```bash
kubectl create deployment mynginx --image=nginx --replicas=1
```

## After create deployment edit deployment and add the values in resouces line

```
 resouces:
    requests:
         cpu: 100m
```               
## Create servcie 

```bash
kubectl expose deployment mynginx --port=80 --type=ClusterIP
```

## Create HPA 

```bash
kubectl autoscale deployment mynginx --cpu-percent=10 --min=1 --max=10
```

## Check the autoscale is created:

```bash
kubectl get hpa 
```
```bash
kubectl describe hpa 
```

## Increase the load on the nginx pods or server run this command:

```bash
kubectl run load-generator --image=busybox:1.28 --restart=Never -- sh -c 'while true; do wget -q -O- http://mynginx; done'
```

## Check the load is incresing on the pods open second terminal run command: 

```bash
kubectl get hpa 
```
```bash 
kubectl get pods 
```
```bash
kubectl top pods 
```
