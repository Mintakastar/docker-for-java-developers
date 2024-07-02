# docker-for-java-developers
this is part of this linked in course: https://www.linkedin.com/learning/introduction-to-docker-for-java-developers/learn-dockerfile-instructions?autoSkip=true&amp;contextUrn=urn%3Ali%3AlearningCollection%3A7212135448133918723&amp;resume=false&amp;u=2113185



volumes examples


run for the host volumes  ( no build needed, just run on the fly)

    -v : for the volume parameter
    -v HOST-FOLDER-PATH:CONTAINER-FOLDER-PATH
    alpine : this is the docker image to use


<H1>HOST VOLUME</H1>

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


<H1>ANONYMOUS VOLUME</H1>

    docker run -itd  --name ANON-volume-app -v /container-folder alpine

<H1>NAME VOLUME</H1>

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