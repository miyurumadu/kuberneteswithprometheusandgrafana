# kuberneteswithprometheusandgrafana
This project will demonstrate how to setup  a Prometheus monitoring setup and how it's used to monitor the external sites using blackbox exporter. Also this will visualize that monitoring setup on Grafana with a nice dashboard 

# Step 01
Clone the reporsiory and connect with your Kubernetes cluster (You can export the kubeconfig.yaml and connect using export KUBECONFIG=kubeconfig.yaml)

# Step 02
Create a Config Map for Prometheus including the details of the site which is going to be monitored using blackbox exporter

# Step 03
Create a new Namespace as monitoring.
```
kubectl create namespace monitoring
```
Create the prometheus deployment and service and try to access using nodeport
```
kubectl create -f configmap.yaml
```

# Step 04
Create a deployment as well as a service for Grafana and test the Grafana access.
kubectl create  -f prometheus-deployment.yaml 
You can check the created deployment using the following command
kubectl get deployments --namespace=monitoring

# Step 05
Create the Blackbox exporter deployment and deploy it as a service 
kubectl create  -f blackbox-exporter.yaml 

# Step 06
Check the pods running
![image](https://github.com/miyurumadu/kuberneteswithprometheusandgrafana/assets/18532502/e93ade61-3bab-459f-9b84-7c0dcd88ab3a)

# Step 07
Check the services running
![image](https://github.com/miyurumadu/kuberneteswithprometheusandgrafana/assets/18532502/f0af3742-2d19-4439-baea-157bde18976c)

# Step 08
Get the external-ip address to access the services
![image](https://github.com/miyurumadu/kuberneteswithprometheusandgrafana/assets/18532502/9622f8da-b500-40b7-a385-465633374c08)

# Step 09
Combine the externalip:nodeport to access the Prometheus and Grafana Services
See the below example
http://85.215.193.215:30000  Prometheus
http:// 85.215.193.215:30748 Grafana


# Step 10
Now go to Prometheus targets and you will see our mail.ionos.con monitoring job status
![image](https://github.com/miyurumadu/kuberneteswithprometheusandgrafana/assets/18532502/fd84336e-4820-41f2-a892-3f0fe6977a88)

# Step 11
Next step is to create a dashboard in Grafana, for that I will get the existing dashboard copied from Grafana official website and import. After that you will be able to visualize the metrics. 
![image](https://github.com/miyurumadu/kuberneteswithprometheusandgrafana/assets/18532502/d26d3a59-36a0-4219-bb74-0fb96fbf427b)
