# simple webapp helm chart

Helm chart to deploy a simple webapp to Kubernetes.

steps

    helm install -f values-dev003.yaml simple-webapp my-simple-webapp --namespace portal
    helm list --all-namespaces
    helm uninstall my-simple-webapp --namespace portal
