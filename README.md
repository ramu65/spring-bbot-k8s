Prerequisites
    Minikube: Ensure you have Minikube installed and running.
    kubectl: Install kubectl for interacting with your Minikube cluster.
    Docker: Have Docker installed for building your images.
    kustomize : Ensure you have Kustomize installed and running

Build and Push API Docker Image
    Set the Docker environment to Minikube:
        eval $(minikube docker-env)
    Build the Docker image:
        cd spring-boot-api
        docker buildx build -t <dockerhub-name>/spring-boot-api:<version> --platform linux/amd64,linux/arm64 .
        ##### This command should be run in the above format if you run on Mac otherwise you can run simple docker build -t <image-name> .#####
    Push the image:
        docker push <dockerhub-name>/spring-boot-api:<version>

Build and Push API Docker Image
    Build the Docker image:
        cd nginx
        docker buildx build -t <dockerhub-name>/nginx-frontend:<version> --platform linux/amd64,linux/arm64 .
        ##### This command should be run in the above format if you run on Mac otherwise you can run simple docker build -t <image-name> .#####
    Push the image:
        docker push <dockerhub-name>/nginx-frontend:<version>

Deployment:
    Update the api-deploy.yaml and nginx-deploy.yaml file with the new image pushed to your docker hub repo
    cd k8s
    minikube start
    kubectl apply -k .

Testing:
    Run the below command to give an URL
    minikube service nginx-frontend --url 



