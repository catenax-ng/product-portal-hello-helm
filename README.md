# A minimal Catena-X NG CI pipeline

Project template featuring
- simple web page
- Docker build
- Helm chart
- GitHub action CI pipeline


### Login to ghcr.io

Go to https://github.com/settings/tokens and create a token with "repo read&write" permissions.
Use it to login with the GitHub container registry.

    echo YOUR_TOKEN | docker login ghcr.io -u USERNAME --password-stdin


### CI build & publish

Edit the web page content. Replace the "Hello *" message with your username.
Then push your changes to trigger the GitHub action CI pipeline.

    sed -i 's/Hello [^!<]*/Hello '$USER'/g' docs/index.html
    git commit -am "greet myself"
    git push


Wait until the action is finished (~30s). Check the status here
https://github.com/catenax-ng/product-portal-hello-helm/actions


### Download & run the image

Download the image, start the web application and check if your changes are applied.

    export IMAGE=ghcr.io/catenax-ng/product-portal-hello-helm:main
    docker pull $IMAGE
    docker run --rm -d -p 3000:8080 --name hello-helm.ci $IMAGE
    curl -s http://localhost:3000/ | grep Hello


### cleanup

Delete unused resources

    docker stop hello-helm.local
    docker stop hello-helm.ci
    docker rm hello-helm.local
    docker rm hello-helm.ci
    docker rmi $IMAGE

