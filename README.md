# docker-for-java-developers
this is part of this linked in course: https://www.linkedin.com/learning/introduction-to-docker-for-java-developers/learn-dockerfile-instructions?autoSkip=true&amp;contextUrn=urn%3Ali%3AlearningCollection%3A7212135448133918723&amp;resume=false&amp;u=2113185



# Volumes examples


run for the host volumes  ( no build needed, just run on the fly)

    -v : for the volume parameter
    -v HOST-FOLDER-PATH:CONTAINER-FOLDER-PATH
    alpine : this is the docker image to use


## HOST VOLUME

    docker run -itd  --name host-volume-app -v ${PWD}/dockerfile-demos/volumes/my-host-folder:/container-folder alpine

run commands on it 
    
    docker exec -it host-volume-app sh 
    #once on the CLI of the container
    cat /container-folder/host-hello.txt
    #then it print its content 
    ls /container-folder/
    # then it prints the file list
    

This is to write on the file 

    echo Hello from the container >> /container-folder/host-hello.txt
    exit


## ANONYMOUS VOLUME

    docker run -itd  --name ANON-volume-app -v /container-folder alpine

## NAMED VOLUME

    docker run -itd  --name name-volume-app -v bob:/container-folder alpine

docker command to list the volumes
    
    docker volume ls
    
    result:
        DRIVER    VOLUME NAME
        local     37c71125b801eea30e66bd07d3f0ae9ec2bb354ea01341fbcb4f8348586aecfa
        local     bob

Create a file in each volume
    
    docker exec -it ANON-volume-app touch /container-folder/anon-file
    docker exec -it name-volume-app touch /container-folder/named-file

you can go for docker desktop UI and see the docker volumes there


# PORT EXAMPLES

    cd dockerfile-demos/portdemo/
    ./mvnw package
    java -jar  target/portdemo-0.0.1-SNAPSHOT.jar 
    
    #into another terminal
        curl localhost:8080/actuator/health
    #prints
        {"status":"UP"}

docker code to run the example

8080:8080  : first 8080 is our host, second are from container ( default spring boot app )

    docker build -t portdemo .
    docker run -itd --name portdemo-app portdemo
    
    #into another terminal
        curl localhost:8080/actuator/health
    #prints
        curl: (7) Failed to connect to localhost port 8080 after 0 ms: Connection refused

exposing

    #do another example exposing the port
    docker run -p 8080:8080 -itd --name portdemo-app80 portdemo

    #into another terminal
        curl localhost:8080/actuator/health
    #prints
        {"status":"UP"}

exposing

    #do another example exposing the port
    docker run -p 9090:8080 -itd --name portdemo-app90 portdemo

    #into another terminal
        curl localhost:9090/actuator/health
    #prints
        {"status":"UP"}

# docker registry
   #already logged in
    
    docker pull alpine:latest
    docker tag docker.io/library/alpine:latest docker.io/raffenio/alpine:me
    docker push docker.io/raffenio/alpine:me
    --login
    docker push docker.io/raffenio/alpine:me
    --remove all images
    docker pull raffenio/alpine:me
    
