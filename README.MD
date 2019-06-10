Containerized a basic "Hello World" Vertx project with a unit test (https://github.com/bassdude5/Vertx_HelloWorld) 




oc login

oc new-project vertx

mvn clean install

#ideally want to push to namespace like defaut or openshift so can be accessable by everyone
docker build -t openshift/java-fat-jar-example:latest .

docker images #to view the image

docker login -u username -p $(oc whoami -t) docker.registry.url

docker push docker.registry.url/openshift/java-fat-jar-example:latest .

oc new-app --docker-image=docker.registry.url/openshift/java-fat-jar-example:latest

#make sure your pods are up
oc edit svc servicename #change port 8080 -> 8081 as app requires

oc expose svc servicename

oc get route #to see the route

curl route or open in browser

