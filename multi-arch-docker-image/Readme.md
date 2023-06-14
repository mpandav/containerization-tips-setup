# How to create multi architecture (amd/arm) docker images? 

You can use experimental feature from Docker called buildx to create the multi architecture supported images. The tool itself do not store the image to local repository but would help you to create and directly push the images to docker hub or registry.

## How to use buildx

### 1. Create a builder consist of required architecture that you want ypir image/app to be supported on
    docker buildx create --name mybuilder --platform linux/arm64,linux/amd64

### 2. Switch to above created builder 
By default, builder configured for the architecture on your hardware. You can verify by running  docker buildx inspect --builderName

    docker buildx use mybuilder

### 3. Create an multi arch supported image
    docker buildx build --platform linux/arm64,linux/amd64 -t repository/imageName:version --push . 

This will create an image of your provided name and version on your docker registry.
