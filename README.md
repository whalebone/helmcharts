# How to install Whalebone resolver in Kubernetes using HELM

1. Prereq: Install HELM v3 (https://helm.sh/).
2. Prereq: Create NameSpace for whalebone resolver ```kubectl create ns <your_namespace> ```
3. Add whalebone HELM repo: ```helm repo add whalebone "https://raw.githubusercontent.com/whalebone/helmcharts/main/"```
4. Optional: ```helm repo update```
5. Optional: Get versions in whalebone repo: ```helm search repo whalebone --versions```
6. Installation  ```helm install wb-resolver whalebone/wb-resolver -f ./<resolver_params_file>.yaml -f ./<resolver_secrets_file.yaml> --set namespace=<your_namespace> -n <your_namespace>```
Note: Files ```resolver_params_file>.yaml``` and  ```<resolver_secrets_file.yaml>``` in portal when you add k8s resolver
# How to check installation.
1. Check helm:  ```helm list -n <your_namespace>```
2. Check components: ```kubectl get all -n <your_namespace>```

You should see similar output:
```
NAME                               READY   STATUS    RESTARTS   AGE
pod/wb-resolver-5f5649c967-bq526   9/9     Running   0          78m
pod/wb-resolver-5f5649c967-chxbd   9/9     Running   0          78m

NAME                           TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)                     AGE
service/wb-resolver-nodeport   NodePort   10.56.11.22   <none>        53:30545/TCP,53:30545/UDP   78m

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/wb-resolver   2/2     2            2           78m

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/wb-resolver-5f5649c967   2         2         2       78m
```
# Next steps
The helm installation does NOT expose the resolver to the internet. This step is on the customer side. Below are examples of services (both must be applied), which will expose the resolver to the internet and assign external IP adress

```
apiVersion: v1
kind: Service
metadata:
  name: wb-resolver-tcp-external
  labels:
    app.kubernetes.io/instance: resolver
  namespace: <your_namespace> 
spec:
  selector:
    app: wb-resolver
  type: LoadBalancer
  loadBalancerIP: <external_IP>
  ports:
    - name: dns-tcp
      port: 53
      protocol: TCP
      targetPort: 53

---
apiVersion: v1
kind: Service
metadata:
  name: wb-resolver-udp-external
  labels:
    app.kubernetes.io/instance: resolver
  namespace: <your_namespace> 
spec:
  selector:
    app: wb-resolver
  type: LoadBalancer
  loadBalancerIP: <external_IP>
  ports:
    - name: dns-udp
      port: 53
      targetPort: 53
      protocol: UDP 
```

# Uninstall
To uninstall resolver please run: ```helm uninstall wb-resolver -n <your_namespace>```








