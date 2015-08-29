
***REMOVED***

***REMOVED***

***REMOVED***
***REMOVED***
***REMOVED***

## Usage

Build the container that will be responsible for composing and building the api gateway jar (a Spring Boot application)

    docker build -t lambda/builder .

Run the lambda/builder container and pass the required environment variables:

Using a fresh builder image (no maven dependencies downloaded)

    docker run -d \
        -e "LAMBDA_JAR=/data/import/lambda.jar" \
        -e "LAMBDA_HANDLER=com.digitalsanctum.lambda.samples.HelloWorld" \
        -e "LAMBDA_RESOURCE_PATH=/hello" \
        -e "LAMBDA_TIMEOUT=5" \
        -v ~/projects/lambda/import:/data/import \
        -v ~/projects/lambda/export:/data/export \
        --name builder lambda/builder:primed /data/build.sh

Or, use the primed image (most maven dependencies already downloaded)

    docker run -d \
    -e "LAMBDA_JAR=/data/import/lambda.jar" \
    -e "LAMBDA_HANDLER=com.digitalsanctum.lambda.samples.HelloWorld" \
    -e "LAMBDA_RESOURCE_PATH=/hello" \
    -e "LAMBDA_TIMEOUT=5" \
    -v ~/projects/lambda/import:/data/import \
    -v ~/projects/lambda/export:/data/export \
    --name builder lambda/builder


Optionally, build and run a container to run the exported api.jar:

    cd export
    docker build -t lambda/api .
    docker run -d -p 8080:8080 --name api lambda/api


## Priming the Builder Container

First, run interactively:

    docker run -it --rm \
        -e "LAMBDA_JAR=/data/import/lambda.jar" \
        -e "LAMBDA_HANDLER=com.digitalsanctum.lambda.samples.HelloWorld" \
        -e "LAMBDA_RESOURCE_PATH=/hello" \
        -e "LAMBDA_TIMEOUT=5" \
        -v ~/projects/lambda/import:/data/import \
        -v ~/projects/lambda/export:/data/export \
        --name builder lambda/builder /bin/bash

Second, from inside the builder container run /data/build.sh

Last, from the Docker host commit the container.

    docker commit builder lambda/builder:primed



***REMOVED***
***REMOVED***
    - complete Jersey/Spring Boot jar
    - Docker image
***REMOVED***
***REMOVED*** with persistence to map functions to endpoints    
***REMOVED***
***REMOVED***

***REMOVED***
***REMOVED***
***REMOVED***
***REMOVED***

