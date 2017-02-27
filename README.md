# dockernotes - help understanding docker

## command: 'docker run -i -it debian /bin/bash'
* this wwill give you a new command prompt inside the containe, very similar toi sshing into a remote machine
* in this case, the flags -i and -t tell docker we want an interavyive session with a tty attached
* the comman "/bin.bash" give us a bash shell
* when you enter 'exit' the container will stop - containers only run as long as their main proccess


## let’s launch a new container; but this time, we’ll give it a new hostname with the -h flag
* docker run -h CONTAINER -i -t debian /bin/bash
* lets break the container
* 'mv /bin /basket'
* ls
* response should be "bash: ls: command not found"
* onpen another terminal enter: "docker ps"
* should give you details about all the currently running containers
* CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
* 969b476fe294        debian              "/bin/bash"         3 minutes ago       Up 3 minutes                            stupefied_lumiere
* the name stupefiend_turing  is the containers readable name that can be used to identify it from the host
* we can get more information by running the following in ternimal(notcontainer): docker inspoect stupefiued_turing
* alot of info is returned but its not easy to parse 
* run the following "docker inspect stupefied_lumiere | grep IPAddress"
* or
* docker inspect --format {{.NetworkSettings.IPAddress}} stupefied_lumiere
* both gives ip address of of the running container
* know if we run: 'docker diff stupefile_lumiere'
* because we changed all /bin to /backet we get a list of all the changed files in the running container
* if you run: 'docker logs stupefied_turning' you get a list of everything thats happend inside the container
* exit the container and enter: "docker ps", you should see that no containers are running
* if you enter docker ps -a you will see all of all containers(stopped and exited)
* if you run: "start docker stupefied_lumiere" you can restart the container but in this case we broke the above container so it wont run again (the mv /bin /bucketr)
* so to delete run docker rm stupefied_lumiere

## cleaning up stopped contaioners
* id you want to get all IDS of stopped container run: docker ps -aq -f status=exited
* if you wanrt to get rid off all stopped containers: docker rm -v $(docker ps -aq -f status=exited)
* the -v argument will delete any Docker-managed volums that arent referenced by other containers

