# product-portal-hello-helm

A minimal project template featuring
- simple web page
- docker build
- helm chart
- github action


local build & publish & run

    export IMAGE=ghcr.io/$GITHUB_USER/hello-helm
    docker build -t $IMAGE -f .conf/Dockerfile .
    docker run --rm -d -p 3000:8080 --name cx-hello-helm $IMAGE
    docker push $IMAGE


github action

    

