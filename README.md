## GKE Bootcamp

This repo deploy one VPC and GKE cluster to host **Online Boutique** application.

## Quickstart (GKE)

1. Ensure you have the following requirements:
   - [Google Cloud project](https://cloud.google.com/resource-manager/docs/creating-managing-projects#creating_a_project).
   - Shell environment with `gcloud`, `git`, and `kubectl`.

2. Terraform Plan/Apply to create the infrastructure.
```sh
terraform init
terraform plan
terraform apply
```

3. Deploy Online Boutique to the cluster.

```sh
kubectl apply -f ./release/kubernetes-manifests.yaml
```

4. Wait for the pods to be ready.

```sh
kubectl get pods
```

After a few minutes, you should see the Pods in a `Running` state:

```
NAME                                     READY   STATUS    RESTARTS   AGE
adservice-76bdd69666-ckc5j               1/1     Running   0          2m58s
cartservice-66d497c6b7-dp5jr             1/1     Running   0          2m59s
checkoutservice-666c784bd6-4jd22         1/1     Running   0          3m1s
currencyservice-5d5d496984-4jmd7         1/1     Running   0          2m59s
emailservice-667457d9d6-75jcq            1/1     Running   0          3m2s
frontend-6b8d69b9fb-wjqdg                1/1     Running   0          3m1s
loadgenerator-665b5cd444-gwqdq           1/1     Running   0          3m
paymentservice-68596d6dd6-bf6bv          1/1     Running   0          3m
productcatalogservice-557d474574-888kr   1/1     Running   0          3m
recommendationservice-69c56b74d4-7z8r5   1/1     Running   0          3m1s
redis-cart-5f59546cdd-5jnqf              1/1     Running   0          2m58s
shippingservice-6ccc89f8fd-v686r         1/1     Running   0          2m58s
```

5. Access the web frontend in a browser using the frontend's external IP.

```sh
kubectl get service frontend-external | awk '{print $4}'
```

Visit `http://EXTERNAL_IP` in a web browser to access your instance of Online Boutique.

6. Congrats! You've deployed the default Online Boutique. 

7. Once you are done with it, delete the GKE cluster.

```sh
terraform destroy
```

Deleting the cluster may take a few minutes.