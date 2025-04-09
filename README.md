##  Task: Dockerization - Publishing the microservice into the cloud

This document outlines the steps taken to publish a Dockerized microservice to a private container registry on Google Cloud Platform (GCP). This task involves containerizing a microservice using Docker and pushing it to Google Cloud Artifact Registry.

##  Prerequisites

* Google Cloud Platform (GCP) account and project
* Google Cloud SDK (gcloud CLI) installed and configured
* Docker installed
* Git

##  Steps

1.  **Created a Private Container Registry on Google Cloud**

    * We used Google Cloud Artifact Registry to host the Docker image.
    * The following `gcloud` command was used to create the repository:

        ```bash
        gcloud artifacts repositories create my-docker-repo \
        --repository-format=docker \
        --location=australia-southeast1
        ```

        * Repository Name: `my-docker-repo`
        * Location: `australia-southeast1`

    * Alternatively, this could be done through the Google Cloud Console by navigating to Artifact Registry and using the "Create Repository" workflow.

2.  **Authenticated Docker to GCP**

    * Docker was authenticated with GCP using the `gcloud auth configure-docker` command:

        ```bash
        gcloud auth configure-docker australia-southeast1-docker.pkg.dev
        ```

        * This command configures Docker to use the credentials provided by the Google Cloud SDK to authenticate with Artifact Registry in the `australia-southeast1` region.

3.  **Tagged the Docker Image**

    * The local Docker image was tagged to match the Artifact Registry repository:

        ```bash
        docker tag j_skshm/server.js:latest australia-southeast1-docker.pkg.dev/sit323-25t1-jhamb-35c663a/my-docker-repo/j_skshm/server.js:latest
        ```

        * `sit323-25t1-jhamb-35c663a` is the Google Cloud Project ID.
        * `j_skshm/server.js:latest` is the local Docker image name and tag (as shown in the provided screenshot)[cite: 1].

4.  **Pushed the Image to the Registry**

    * The tagged image was pushed to Artifact Registry using the `docker push` command:

        ```bash
        docker push australia-southeast1-docker.pkg.dev/sit323-25t1-jhamb-35c663a/my-docker-repo/j_skshm/server.js:latest
        ```

5.  **Verified the Published Image**

    * To ensure the image was successfully pushed and could be retrieved, it was pulled and run from Artifact Registry:

        ```bash
        docker pull australia-southeast1-docker.pkg.dev/sit323-25t1-jhamb-35c663a/my-docker-repo/j_skshm/server.js:latest
        docker run australia-southeast1-docker.pkg.dev/sit323-25t1-jhamb-35c663a/my-docker-repo/j_skshm/server.js:latest
        ```

    * The microservice started correctly, confirming the successful push and pull.

##  Repository Details

* GitHub Repository URL: `https://github.com/j_skshm/sit323-2025-prac5d`
* Google Cloud Artifact Registry Repository: `australia-southeast1-docker.pkg.dev/sit323-25t1-jhamb-35c663a/my-docker-repo`

##  Notes

* This task was completed using Google Cloud Artifact Registry for container image storage.
* All `gcloud` commands were executed in the terminal after installing and configuring the Google Cloud SDK.
* Ensure that the Google Cloud Project ID and Artifact Registry location are correctly set in the commands.
* The Docker image was tagged and pushed according to the requirements of the assignment to a private container registry on GCP.
* The successful execution of `docker run` confirms the image's viability for deployment.
