
[dɪ'vɑːpz] 

监控的层次
* 系统监控
   * 服务器硬件CPU
   * 操作系统
   * 服务和应用
* 业务监控
  * 业务指标
  * 用户使用





CI/CD 

持续集成、持续交付和持续部署
* CI 持续集成（Continuous Integration)
* CD 持续交付（Continuous Delivery）
* CD 持续部署（Continuous Deployment）

 to get useful insights about the cluster's performance, utilization, and troubleshooting outages.


You should deploy a monitoring and alerting stack, such as Node Exporter, Prometheus, and Grafana, and deploy a central logging stack, such as ELK (Elasticsearch, Logstash, and Kibana). 

 OpenID Connect (OIDC)

Role-Based Access Control (RBAC), Attribute-Based Access Control (ABAC)

Pod security policy (PSP)

The 12 principles of infrastructure design and management
1. Go managed
2. Simplify
3. Everything as Code (XaC):It is a recommended approach to use declarative infrastructure as code (IaC) and configuration as code (CaC) tools and technologies over their imperative counterparts.
4. Immutable infrastructure
5. Automation
6. Standardization
7. Source of truth
8. Design for availability
9. Cloud-agnostic
10. Business continuity
11. Plan for failures
12. Operational efficiency

[The Cloud Native Computing Foundation](https://www.cncf.io)


[NATS](https://nats.io)

the famous monitoring approaches, such as RED (Rate, Errors, and Duration), and USE (Utilization, Saturation, and Errors).


Cloud-native landscape and ecosystem
* Provisioning: This layer has projects for infrastructure automation and configuration management, such as Ansible and Terraform, and container registry, such as Quay and Harbor, then security and appliance, such as Falco, TUF, and Aqua, and finally, key management, such as Vault.
* Runtime: This layer has projects for container runtime, such as containerd and CRI-O, cloud-native storage, such as Rook and Ceph, and finally, cloud-native networking plugins, such as CNI, Calico, and Cilium.
* Orchestration and management: This is where Kubernetes belongs as a schedular and orchestrator, as well as other key projects, such as CoreDNS, Istio, Envoy, gRPC, and KrakenD.
* App definition and development: This layer is mainly about applications and their life cycle, where it covers CI/CD tools, such as Jenkins and Spinnaker, builds and app definition, such as Helm and Packer, and finally, distributed databases, streaming, and messaging.






Kubernetes is not a Platform as a Service (PaaS). It doesn't dictate many important aspects that are left to you or to other systems built on top of Kubernetes, such as Deis, OpenShift, and Eldarion.


https://kubernetes.io/zh/docs/tasks/tools/install-kubectl-linux/


https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-interactive/


* The sidecar pattern
* The ambassador pattern
* Multi-node patterns

 alpha to beta to GA (general availability) and from V1 to V2, and so on.


[docker engine install](https://docs.docker.com/engine/install/ubuntu/)

https://chinese.freecodecamp.org/news/the-docker-handbook/






Manning’s Docker in Action, second edition


Manning.Learn.Docker.in.a.Month.of.Lunches

[open source](https://github.com/sixeyed/diamol)

There’s a powerful framework for implementing DevOps called CALMS—Culture, Automation, Lean, Metrics, and Sharing. Docker works on all those initiatives: automation is central to running containers, distributed apps are built on lean principles, metrics from production apps and from the deployment process can be easily published, and Docker Hub is all about sharing and not duplicating effort.

```
docker version
docker-compose version
```

https://docs.docker.com/engine/reference/run/


```
sudo service docker start
sudo service docker restart
sudo service docker stop
sudo service docker status

sudo systemctl start docker
sudo systemctl stop docker
sudo systemctl restart docker
sudo systemctl status docker

docker info
docker --help

docker images -a
docker ps -a

docker rmi -f  ....

docker system df


docker container rm -f $(docker container ls -aq)

docker image rm -f $(docker image ls -f reference='diamol/*' -q)


docker container run diamol/ch02-hello-diamol


docker container run --interactive --tty diamol/base

docker container ls

docker container top f1

docker container logs f1

docker container inspect f1

docker container ls --all

docker container run --detach --publish 8088:80 diamol/ch02-hello-diamol-web

docker container stats 

docker container rm --force $(docker container ls --all --quiet)



```


-p（小写）则可以指定要映射的IP和端口，但是在一个指定端口上只可以绑定一个容器。支持的格式有 hostPort:containerPort、ip:hostPort:containerPort、 ip::containerPort

* --detach—Starts the container in the background and shows the container ID 
* --publish—Publishes a port from the container to the computer




https://hub.docker.com/settings/security


Linux kernel namespaces, such as process ID (pid) namespaces or network (net) namespaces, allow Docker to encapsulate or sandbox processes that run inside the container. Control Groups make sure that containers cannot suffer from the noisy-neighbor syndrome, where a single application running in a container can consume most or all of the available resources of the whole Docker host. Control Groups allow Docker to limit the resources, such as CPU time or the amount of RAM, that each container is allocated.

 [containerd – an industry-standard container runtime](https://containerd.io)

 https://github.com/PacktPublishing/Learn-Docker---Fundamentals-of-Docker-19.x-Second-Edition


 192.168.65.0/24

[docker镜像仓库](https://www.jianshu.com/p/fecbe5602cae)

[Container Training](https://container.training)

[kubernetes](https://kubernetes.io/docs/home/)


```

minikube start --image-mirror-country cn --registry-mirror https://registry.docker-cn.com  --image-repository registry.cn-hangzhou.aliyuncs.com/google_containers --vm-driver=docker

minikube delete --all 

minikube ssh

minikube dashboard

ls ~/.minikube


 kubectl cluster-info  



docker exec -it gitlab-runner /bin/bash

```



https://hub.docker.com/u/dockerinaction/


The specific features are as follows:
* PID namespace—Process identifiers and capabilities
* UTS namespace—Host and domain name
* MNT namespace—Filesystem access and structure
* IPC namespace—Process communication over shared memory  NET namespace—Network access and structure
* USR namespace—User names and identifiers
* chrootsyscall—Controls the location of the filesystem root  cgroups—Resource protection
* CAP drop—Operating system feature restrictions
* Security modules—Mandatory access controls

The component that fills the shipping container role is called an image.

# CI/CD

 software development life cycle (SDLC)

 functional tests

Happy path testing

edge- case testing

corner-case testing

unhappy path testing

* user tests: test large, user-facing features
* integration test: test functions working together
* unit tests: test individual functions


performance test

 load tests

 soak tests

 Fuzz tests


  static code analysis

Security-testing code manually

Dynamic analysis

测试左移（Shift-Left testing）



# Books
Pipeline as Code Continuous Delivery with Jenkins, Kubernetes, and Terraform

* Cloud-native architecture
* DevOps 

pipeline-as-code approach.


 the microservice architectural style 

 Jenkins (www.jenkins.io), Spinnaker (https:// spinnaker.io/), or GoCD (www.gocd.org)

 
Pipeline as code (PaC) 

infrastructure as code (IaC)