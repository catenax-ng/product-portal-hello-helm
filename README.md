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


change content and publish through github action

    # replace the "Hello *" message with your username
    sed -i 's/Hello [^!<]*/Hello '$USER'/g' docs/index.html
    git commit -am "greet myself"
    git push

    # wait until the action is finished (~30s) - check here
    # https://github.com/catenax-ng/product-portal-hello-helm/actions

    export IMAGE=ghcr.io/catenax-ng/product-portal-hello-helm:main
    docker pull $IMAGE
    docker run --rm -d -p 3000:8080 --name cx-hello-helm $IMAGE
    curl -s http://localhost:3000/ | grep Hello

