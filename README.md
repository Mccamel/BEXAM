#  Exam

candidate exam

## Requirements
Build an nginx docker image that will serve a static web page saying "Hello visitor! <build_number>. '' The build number should be the jenkins job build number. You may upload the image to docker hub and use it as the main repository for your built images.
Apply a Deployment using Jenkins in the Kubernetes cluster with the image you have built. The deployment should have the Label "app: nginx" and its container port should be 80. You are encouraged to use service account tokens for authorization between Jenkins and the cluster, though you may use your user credentials for the deployment process. There is no need to create a Service object for the deployment since it's already preconfigured.
Once your Deployment is properly configured and running, it can be accessed at 
http://xxx.xxx.xxx.xxx/


## status
Done 
