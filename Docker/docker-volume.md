In this course, we will go over how to create and use Docker volumes. We will also discuss their ability to persist data outside of the container lifecycle.

We will be making use of two seprate arguments: -v and --mount. Additional documentation for these options can be fond through the Docker Docs.

More explanation on Docker containers and volumes can be found in the Docker Overview.

---
### Choose the -v or --mount flag:

Originally, the -v or --volume flag was used for standalone containers and the --mount flag was used for swarm services. However, starting with Docker 17.06, you can also use --mount with standalone containers. In general, --mount is more explicit and verbose. The biggest difference is that the -v syntax combines all the options together in one field, while the --mount syntax separates them. Here is a comparison of the syntax for each flag.

---
### Create a persistant data Volume :

1. docker volume create devvolume
2. docker volume ls
3. docker volume inspec devvolume
4. docker volume inspect devvolume
5. docker container run -d --name devcont --mount source=devvolume,target=/app nginx
6. docker container ls
7. docker container inspect 24e24953d7e4
8. cd /var/lib/docker/volumes/devvolume/_data
9. sudo su
10. ls
11. cd /var/lib/docker/volumes/devvolume/_data && ls
12. docker exec -it devcont sh
13. cd app && touch index.php
10. history

----
### delete container and verify that data saved inside volume is exist:

1. docker container run -d --name devcont2 -v devvolume:/app nginx
2.