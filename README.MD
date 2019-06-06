Containerized a basic "Hello World" Vertx project with a unit test (https://github.com/bassdude5/Vertx_HelloWorld) 




Step 1: mvn clean install

Step 2: docker build -t sample/vertx-java-fat .

Step 3: docker run -t -i -p 8080:8080 sample/vertx-java-fat
