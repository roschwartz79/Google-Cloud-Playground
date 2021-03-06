# Google-Cloud-Playground & Jenkins Test Repo

Learning and experimenting with the Google Cloud Platform and the Google Kubernetes Engine! Also playing with a local Jenkins pipeline,
I'd love to try and use the managed Jenkins pipelines that Google has to offer but this will be a good start.

Trying to get my own Spring app out on the intersphere and experiment with the managed Kubernetes instance to see what kind
of cool stuff I come up with!

### Instructions

How to push the docker image to the Google Container Registry:

1. Clone the repository in the Google Cloud Shell `git clone https://github.com/roschwartz79/Google-Cloud-Playground.git`
2. Change the `jib.to.image` property in build.gradle to bump the Docker tag
3. Build the repo with the gradle wrapper `./gradlew build`
4. Build a docker image with the jib gradle plugin `./gradlew jibDockerBuild`
5. Test it locally (Locally as in the google cloud shell) docker run -ti --rm -p 8080:8080 `gcr.io/$GOOGLE_CLOUD_PROJECT/hello-java:v3`
6. Push the image to the container registry! Woohoo! `docker push gcr.io/my-spring-test-305005/hello-java:v3`

Note that I will be trying to simplify this process in the future but for now this is the way I have found to work with gradle! There
are other ways with maven.

### Working with Kubernetes

- To see the current pods and replicas that are up and running `kubectl get pods`
- To push a new image to the cluster `kubectl set image deployment/hello-java hello-java=gcr.io/$GOOGLE_CLOUD_PROJECT/hello-java:<tag>`
- Scale the deployment `kubectl scale deployment hello-java --replicas=0`
- If you need to roll the deployment back `kubectl rollout undo deployment/hello-java`

### Jenkins Instructions (For local use)

I am using the docker image of Jenkins and running it locally

From the [docs](https://github.com/jenkinsci/docker/blob/master/README.md): `docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
`

