# App-Info-Ops

Usage Information
-----------
The project uses maven to build the artifacts. After thet we're deploying our artifacts to S3 bucket and docker registeryby using ANT. This process is automated by using jenkins.


Maven
----
```
mvn clean install
```
This will create target directory.

ANT
----
below is the clear explains for every target

```
clean
```
This will clean exiting artifact directory. 
```
makedir
```
Creating new directory for our artifacts
```
copy-artifacts
```
```
NOTE:Here for this target we'have given dependency so that it will only run when the previous target is success.
```
I this targt we're coping the contant in he tomcat directory to our artifacts directory and also we're copying target directory to webapss.
```
make-archive-app
```
creats a directory for our artifacts which we're going to copy into S3 buckets.
```
archive-artifacts
```
archiving the artifact directory
```
upload-s3
```
This step will upload the artifacts to S3 buckets.

If you're using ec2 machine to perform this, create an IAM role to access s3 bucket and assign the role to your instance.
You can also use aws cli to perform this target.
```
copy-artifacts-to-docker
```
This target will copy artifact directory to docker directory
```
docker-image
```
Cretaes an image using the Dockerfile
```
docker-push
```
Push our docker image to docker repo
```
all-clean
```
Deletes target directory

JENKINS
========

Goto >> Manage jenkins >> Global Tool Configutarion >> here configure your ant and maven

Managing Docker Creds
------
Manage Jenkins >> Manage credentials >> Here provide your docker registory username and password and ```SAVE```

Create a New Job 
-----
Goto >> New item >> Select pipleline >> Give a name to your project ```SAVE```

Goto >> your project >> configure >> pipeline >> select ```pipeline script from SCM``` under ```Definition``` option
Provide your Repository details and credentials.
```Branches to build``` Give the name of your branch
```Script Path``` path to your Jeninsfile. In our case it's Jenkinsfile

```SAVE```

NOW SELECT BUILD NOW
----
