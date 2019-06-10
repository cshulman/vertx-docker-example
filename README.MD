Containerized a basic "Hello World" Vertx project with a unit test (https://github.com/bassdude5/Vertx_HelloWorld) 


<h1><strong> Steps for deploying to Openshift </strong></h1>

<ol>
  <li> Login to OpenShift: 
    <br><code> oc login </code></li>
  
  <li> Login to Docker: 
    <br><code> docker login -u username -p $(oc whoami -t) docker.registry.url </code></li> 
    
  <li> Create a new OpenShift project: 
    <br><code> oc new-project vertx </code></li>
    
  <li> Build the app to get the jar (note the jar name needs to be the same as the jar name specified in the Dockerfile):
    <br><code> mvn clean install </code></li>
    
  <li> Build the image (here we are specifying the openshift namespace so the image can be accessed across all namespaces):      
    <br><code> docker build -t openshift/java-fat-jar-example:latest . </code></li>
    
  <li> View the image: 
    <br><code> docker images </code></li>
    
  <li> Tag the image with docker.registry/image-name:version
    <br><code> docker tag openshift/java-fat-jar-example docker.registry.url/openshift/java-fat-jar-example:latest </code></li>
    
  <li> Push the image to the internal registry: 
    <br><code> docker push docker.registry.url/openshift/java-fat-jar-example:latest </code></li>
    
  <li> Create the application (make sure you're in the correct namespace): 
    <br><code> oc new-app --docker-image=docker.registry.url/openshift/java-fat-jar-example:latest </code></li>
  
  <li> Verify that your pods are up: 
    <br><code> oc get pods </code></li>
    
  <li> Edit the service to route through port 8081 (as this app requires). Change the port, target port and the port name:
    <br><code> oc edit svc servicename  </code></li>
    
  <li> Confirm that the service is correct: 
    <br><code> oc describe svc servicename </code></li>
    
  <li> Expose the service: 
    <br><code> oc expose svc servicename </code></li>
  
  <li> get the route: 
    <br><code> oc get route </code></li>
    
  <li> Access the route via comand line or open in your browser: 
    <br><code> curl route </code></li>
    
    
  
