# product-portal-hello-helm

A minimal project template with a pipeline for docker, helm, argocd

steps

    export IMAGE=ghcr.io/catenax-ng/hello-helm
    docker build -t $IMAGE -f .conf/Dockerfile .
    docker run --rm -d -p 3000:8080 --name cx-hello-helm $IMAGE
    docker push $IMAGE

