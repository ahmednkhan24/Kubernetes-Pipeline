## npm start
> node-to-aws@1.0.0 start /Users/ahmedkhan/Documents/kub
> node ./src/server
Server is up on 3000

## gcloud builds submit --tag gcr.io/banded-anvil-273516/nodeapp:latest .                          
BUILD
Already have image (with digest): gcr.io/cloud-builders/docker
Sending build context to Docker daemon  2.006MB
Step 1/7 : FROM node:8-alpine
8-alpine: Pulling from library/node
e6b0cf9c0882: Pulling fs layer
93f9cf0467ca: Pulling fs layer
a564402f98da: Pulling fs layer
b68680f1d28f: Pulling fs layer
b68680f1d28f: Waiting
a564402f98da: Verifying Checksum
a564402f98da: Download complete
e6b0cf9c0882: Verifying Checksum
e6b0cf9c0882: Download complete
93f9cf0467ca: Verifying Checksum
93f9cf0467ca: Download complete
b68680f1d28f: Verifying Checksum
b68680f1d28f: Download complete
e6b0cf9c0882: Pull complete
93f9cf0467ca: Pull complete
a564402f98da: Pull complete
b68680f1d28f: Pull complete
Digest: sha256:38f7bf07ffd72ac612ec8c829cb20ad416518dbb679768d7733c93175453f4d4
Status: Downloaded newer image for node:8-alpine
 ---> 2b8fcdc6230a
Step 2/7 : RUN mkdir -p /usr/src/app
 ---> Running in ae3388b9711a
Removing intermediate container ae3388b9711a
 ---> 68def2d5882c
Step 3/7 : WORKDIR /usr/src/app
 ---> Running in a97b628c6618
Removing intermediate container a97b628c6618
 ---> e923de9a8358
Step 4/7 : COPY . .
 ---> 86f6ad104e52
Step 5/7 : RUN npm install
 ---> Running in efde9c90ddf2
audited 126 packages in 0.899s
found 0 vulnerabilities

Removing intermediate container efde9c90ddf2
 ---> 43d676ef74ae
Step 6/7 : EXPOSE 3000
 ---> Running in d7e029c6ecb4
Removing intermediate container d7e029c6ecb4
 ---> ef545720fc52
Step 7/7 : CMD ["npm", "start"]
 ---> Running in 39b3f887f27a
Removing intermediate container 39b3f887f27a
 ---> ebf10fcf5e1c
Successfully built ebf10fcf5e1c
Successfully tagged gcr.io/banded-anvil-273516/nodeapp:latest
PUSH
Pushing gcr.io/banded-anvil-273516/nodeapp:latest
The push refers to repository [gcr.io/banded-anvil-273516/nodeapp]
b593f92bfe85: Preparing
e67fb6b72293: Preparing
df1c2ca39dd3: Preparing
6b73202914ee: Preparing
9851b6482f16: Preparing
540b4f5b2c41: Preparing
6b27de954cca: Preparing
540b4f5b2c41: Waiting
6b27de954cca: Waiting
6b73202914ee: Layer already exists
9851b6482f16: Layer already exists
540b4f5b2c41: Layer already exists
6b27de954cca: Layer already exists
b593f92bfe85: Pushed
e67fb6b72293: Pushed
df1c2ca39dd3: Pushed
latest: digest: sha256:606aa0f5a4dd3226aeb64e9294e3ab5b789925affb22461c865eaec9a3c097ef size: 1782
DONE
------------------------------------------------------------------------------------------------------------------------------------------

## gcloud container clusters create cluster1 --zone=us-central1-f
NAME      LOCATION       MASTER_VERSION  MASTER_IP      MACHINE_TYPE   NODE_VERSION    NUM_NODES  STATUS
cluster1  us-central1-f  ..............  .........      ............   ............       3       RUNNING

## kubectl get svc    
NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   ..........      <none>      443/TCP   10m

## kubectl create -f service.yml
service/nodeapp created

## kubectl get svc              
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP      ..........        <none>      443/TCP        11m
nodeapp      LoadBalancer   ..........        <pending>   80:31829/TCP   21s

## kubectl create -f deployment.yml
deployment.apps/nodeapp created

## kubectl get deployment
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
nodeapp   7/7     7            7           62s

## kubectl get pods      
NAME                       READY   STATUS    RESTARTS   AGE
nodeapp-66898768d8-52s4m   1/1     Running   0          81s
nodeapp-66898768d8-79fdv   1/1     Running   0          82s
nodeapp-66898768d8-7qc2d   1/1     Running   0          81s
nodeapp-66898768d8-c6nd4   1/1     Running   0          81s
nodeapp-66898768d8-jvgqq   1/1     Running   0          81s
nodeapp-66898768d8-rd58s   1/1     Running   0          81s
nodeapp-66898768d8-zkrp7   1/1     Running   0          81s

## kubectl get svc                 
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)        AGE
kubernetes   ClusterIP      ..........        <none>        443/TCP        15m
nodeapp      LoadBalancer   ..........     34.67.118.219   80:31829/TCP   4m24s
