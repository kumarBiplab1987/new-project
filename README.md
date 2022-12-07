Task1
-------
For deployment of mediawiki , we require a container image which we can either create it through Dockerfile (present in the Image folder) or we can use the container from docker hub . I have directly used it from docker hub since I feel it will provide a stable application.

The deployment-media-wiki.yml file is present in Task1 folder and I have used comment to explain  each field .

Here is the deployment snaps:



Now I have user kubernetes service to have a constant ip and load balance for the pods also used Node port as a service to access the service from outside.

The service-mediawiki.yml file present in the Task1 folder will create the required service.

Here is the snap for the same.

Next we can verify if the mediawiki ui is visible through [http://<Node]() ip>:32475

Since I have use minikube so I am able to access through below snap



Next we require to have a db to give a backend support for mediawiki and will be require on setup steps for mediawiki.

For DB I have used mariadb container and the used as a deployment  resource(for test purpose), we might wanted to use a stateful set , which will provide us consistent data.

The deployment file ‘deployment-mariadb.yml’ file can be found inside Task 1 folder .

Here is the deployment snap in the cluster.



To configure the mediawiki, we require to have a consistent ip for the db and to achieve that I have used service type ClusterIP which will provide me a consistent ip also it will be accessible through out cluster.

The service-mariadb.yml helped me to create the service and can be found inside Task1 folder.

Here is the snap for the services create part.

Now we are going to configure the mediawiki to complete the installation.
Here are the snap for the procedure I follow to configure it,






















Once the installation completed, I have downloaded theLocalSettings.php file and mouted it as a hostpath volume , which mount a directory from host nodes file system into the pod.


Task 2
-------

a. To deal with resource crunch , we can specify a memory request for a Container, include the resources:requests field in the Container's resource manifest. To specify a memory limit, include resources:limits . I have included one example pod.yaml located in Task2 folder where we can define each pod separate resource. 

b. For exporting csv data, I might create persistent volume and will use as persistent volume claim , so that I can make the volume available on entire cluster and then will mount some directory to the pod on which I will keep my csv file. By doing this the pod will be able to read the csv file.



