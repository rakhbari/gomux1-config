# gomux1-config
Config repo for gomux1 app

## Helm Deployment
The Helm chart for `gomux1` app is under the `helm/` subdir. Apply the deployment to your K8s cluster by:
```
helm template helm/ --name-template <RELEASE-NAME> | kubectl apply -f -
```
Example:
```
helm template helm/ --name-template dev | kubectl apply -f -
```
Once done, you should see the `gomux1` Deployment & Service live in your K8s cluster:
```
$ kubectl get deployment -n gomux1-dev
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
gomux1   1/1     1            1           5m16s

$ kubectl get service -n gomux1-dev
NAME     TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
gomux1   LoadBalancer   10.97.33.69   localhost     80:31571/TCP   5m24s
```

To override any value in the `values.yaml` file, simply use the `--set` option on the `helm` command.

Example: To override the `service.port` (K8s Service EXTERNAL-IP)
```
helm template helm/ --name-template dev --set service.port=8080 | kubectl apply -f -
```

Please refer to the app's docs on how to access the app's endpoints: https://github.com/rakhbari/gomux1#endpoints

## Argo CD
After installing Argo CD in your K8s cluster, It's best to change its `argocd-server` UI port to `9080`:
```
$ kubectl patch svc argocd-server -n argocd --type merge -p '{"spec": {"ports": [{"name":"http","port":9080,"targetPort":8080}]}}'
```
