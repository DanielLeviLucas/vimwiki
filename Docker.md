# Docker

## Table of contents

- [What is Docker?](#What-is-Docker?)

## What is Docker?

**Docker** is a set of platform as a service products that uses *Os-level virtualization* to deliver software in pacckages called [containers](#containers). Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each ohter through well-defined channels. Because all of the containers share the services of a single *operating system kernel*, they use fewer restources than virtual machines.

### Docker Image

**Docker image** is the *binary, library and source code* that make up an application. 

### Containers

- **Container** is an running instance of the [image](#Docker-Image) running as *process*.
- We can have many [containers](#Containers) running off the same [image](#Docker-Image).

## Docker commands

### Docker basic commands


| Command                                 | Description                                |
| ---                                     | ---                                        |
| `docker container run <image>`          | ***Starts a new container from an image*** |
| `docker container ls`                   | ***list running containers***              |
| `docker container ls -a`                | ***list all containers***                  |
| `docker container stop <container ID>`  | ***Stops the container process***          |
| `docker container start <container ID>` | ***Start an existing stopped image***      |
| `docker container logs <container ID>`  | ***Show logs for a specific container***   |
| `docker container rm <container ID>`    | ***Removes a container***                  |

