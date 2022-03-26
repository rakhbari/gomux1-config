# gomux1-config
Config repo for gomux1 app

# Helm Deployment
The Helm chart for `gomux1` app is under the `helm/` subdir. Apply the deployment to your K8s cluster by:
```
helm template helm/ --name-template <RELEASE-NAME> | kubectl apply -f -
```
Example:
```
helm template helm/ --name-template dev | kubectl apply -f -
```
To override any value in the `values.yaml` file, simply use the `--set` option on the `helm` command.

Example: To override the `service.port` (K8s Service EXTERNAL-IP)
```
helm template helm/ --name-template dev --set service.port=8080 | kubectl apply -f -
```
