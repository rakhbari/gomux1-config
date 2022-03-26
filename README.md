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
