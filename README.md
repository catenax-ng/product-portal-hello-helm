# product-portal-hello-helm

A minimal project template featuring
- simple web page
- docker build
- helm chart
- github action


local build & publish & run

    # go to https://github.com/settings/tokens create a token with "repo read&write" permissions
    echo $YOUR_TOKEN | docker login ghcr.io -u USERNAME --password-stdin

    export IMAGE=ghcr.io/$GITHUB_USER/hello-helm
    docker build -t $IMAGE -f .conf/Dockerfile .
    docker push $IMAGE
    docker run --rm -d -p 3000:8080 --name hello-helm.local $IMAGE
    curl -s http://localhost:3000/
    docker stop hello-helm.local


change content and publish through github action

    # replace the "Hello *" message with your username
    sed -i 's/Hello [^!<]*/Hello '$USER'/g' docs/index.html
    git commit -am "greet myself"
    git push

    # wait until the action is finished (~30s) - check here
    # https://github.com/catenax-ng/product-portal-hello-helm/actions

    # download and run the image - check if your changes are applied
    export IMAGE=ghcr.io/catenax-ng/product-portal-hello-helm:main
    docker pull $IMAGE
    docker run --rm -d -p 3000:8080 --name hello-helm.ci $IMAGE
    curl -s http://localhost:3000/ | grep Hello
    docker stop hello-helm.ci

