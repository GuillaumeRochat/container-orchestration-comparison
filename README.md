# Container Orchestration Comparison

### About

My employer wants to move our application to the cloud over the next few years. To do that, we need to see the state of the current ecosystem. This is the result of a few days/weeks of reading on the container orchestration subject and collecting data from different sources of information. It is in an attempt at getting an overview of the different container orchestrators available prior to attempting a proof of concept. **It is by no mean formed from personnal experience regarding those tools and should not be treated as such.**

We haven't found a centralized source of comparison between the different tools available and had to search for what needs to be taken into consideration and what each tool has to offer. The result is what we believe most outsiders of this ecosystem would observe over their first contact. Is this the true portrait of the ecosystem? Have we missed tools or features that should also be considered? Are some of the information wrong?

**Your contributions are welcomed. Your experience is valuable to create a better overview of the ecosystem.**

### Contribution

### Orchestrator softwares

|Orchestrator|Maintainer|V1 Release|Development Status|License|Support|
|------------|----------|----------|------------------|-------|-------|
|[**Docker Swarm**][1]|[Docker][2]|[2015][3]|Active but flagged as legacy|[Apache License 2.0][4]|Yes|
|[**Docker Swarm Mode**][22]|[Docker][2]|[2016][71]|Active|[Apache License 2.0][4]|Yes|
|[**Kubernetes**][5]|[CNCF][6]|[2015][7]|Active|[Apache License 2.0][4]|From third parties|
|[**Mesos**][8]|[Apache Software Foundation][9]|[2016][10]|Active|[Apache License 2.0][4]|Yes|
|[**Nomad**][11]|[Hashicorp][12]|N/A|Active|[Mozilla Public License 2.0][13]|Yes|


### Orchestrator features

|Features|[Docker Swarm][1]|[Docker Swarm mode][22]|[Kubernetes][5]|[Mesos][8]|[Nomad][11]|
|--------|-----------------|-----------------------|---------------|----------|-----------|
|[Scheduler Architecture][14]|[Monolithic][15]|Shared State [source required]|[Shared State][15]|[Two Level][15]|[Shared State][15]|
|Container agnostic|No|No|Yes, Docker and [rkt][16]|Yes, [Docker][17], [rkt][17] and [other drivers][18]|Yes, [Docker][19], [rkt][20] and [other drivers][21]|
|Service discovery|No native support, requires third parties [source][72]|Native support [source][22]|Native support with an intra-cluster DNS [source][23]|Native support with Mesos-DNS [source][24]|Requires Consul but easy integration provided [source][25]|
|Secret management|No native support [source required]|Native support with Docker Secret Management [source][26]|Native support with secret objects [source][27]|No native support, depends on the framework [source][28]|Requires Vault but easy integration provided [source][29]|
|Configuration management|Through env variables in compose files [source][30]|Through env variables in compose files [source][30]|Native support through ConfigMap [source][31]|No native support, depends on the framework [source][32]|Through the env stanza in the job specifications [source][33]|
|Logging|Requires to configure a [logging driver][34] and forward to a third party such as the [ELK stack][35]|Requires to configure a [logging driver][34] and forward to a third party such as the [ELK stack][35]|Requires to forward logs to a third party such as the [ELK stack][36] [source][37]|With ContainerLogger or provided by the frameworks [source][38]|With the logs stanza to configure where to store the logs for the containers [source][39]|
|Monitoring|Requires to use a third party to keep track of all the containers status [source][40]|Requires to use a third party to keep track of all the containers status [source][40]|With Heapsters providing a base monitoring platform sending data to a storage backend [source][41]|Sends Observability Metrics to a third party monitoring dashboard [source][42]|By outputting resource data to statsite and statsd [source][43]|
|High-Availability|Native support by creating multiple manager [source][73]|Native support from the distribution of manager nodes [source][44]|Native support by replicating master in a HA-cluster [source][45]|Native support from having multiple masters with ZooKeeper coordinating [source][46]|Native support from the distribution of server nodes [source][47]|
|Load balancing|No native support [source required]|By exposing ports for services to an external load balancer [source][22]|External load balancer automatically created in front of a service configured for such [source][48]|Provided from the selected framework such as Marathon [source][49]|Can use Consul integration to do the load balancing using third parties [source][50]|
|Networking|Uses Docker networking facilities [source][74]|Uses Docker networking facilities [source][51]|Requires the use of third parties to form an overlay network [source][52]|Requires the use of third parties for networking solutions [source][53]|No native support for network overlay but handles the exposed services through the network stanza [source][54]|
|Application definition|Uses Docker Compose files [source][1]|Can use the experimental stack command to read Docker-Compose format [source][67]|Using yaml format to define the different objects [e.g.][70]|Depends on the framework [source][68]|Using HCL, a proprietary language similar to json [source][69]|
|Deployment|No deployment strategies, only applies the Docker Compose on a cluster [source required]|Supports rolling update in service definitions and applies it on image update [source][55] <br/>Supports roll-back [source][22]|Native support for deployment with the Deployment definition [source][56]|Depends on the framework [source][57]|Natively support multiple deployment strategies such as rolling upgrades and canary deployments [source][58]|
|Auto-scaling|No [source required]|No, but has easy manual scalling available [source][59]|Native supports to autoscale pods within a given range [source][60]|Depends on the framework [source][61]|Only available through HashiCorp private platform Atlas [source][62]|
|Self-healing|No [source required]|Yes [source][63]|Yes [source][64]|Depends on the framework [source][65]|Yes [source][66]|
|Stateful support|Through the use of data volumes [source][75]|Through the use of data volumes [source][75]|Through StatefulSets [source][76]|Through the creation of persistent volumes [source][77]|Using Docker Volumes [source][78]|
|Development environment|Can use the same or similar Docker Compose files to create the dev environment|Can use the same or similar Docker Compose files to create the dev environment|Can use minikube to quickly create a single node Kubernetes cluster to create the dev environment [source][79]|Depends on the framework but a Mesos cluster can be installed locally|By running a single nomad agent that is both server and client to create the dev environment|
|Documentations|Initially confusing due to the change from [Docker Swarm][1] to [Docker engine Swarm mode][22]|Initially confusing due to the change from [Docker Swarm][1] to [Docker engine Swarm mode][22]|Sometimes difficult to search due to the changes of documentation platforms (github to kubernetes.io) and then organisation (from user-guide/ to tasks/, tutorials/ and concepts/|Very detailed and centralized. The chosen framework will also have to be considered as it will have its own documentation|Simple and centralized but as the project is young, it lacks in external sources|

### Additional Sources

- [Kubernetes vs ECS](https://platform9.com/blog/compare-kubernetes-vs-ecs/)
- [Kubernetes vs Docker Swarm](https://platform9.com/blog/compare-kubernetes-vs-docker-swarm/)
- [Kubernetes vs Mesos](https://platform9.com/blog/compare-kubernetes-vs-mesos/)
- [Evaluating Container Platforms at Scale](https://medium.com/on-docker/evaluating-container-platforms-at-scale-5e7b44d93f2c#.omorj9ur8)
- [A Handy Guide to the Mesos-Kubernetes-Swarm Jungle](https://medium.com/@mustwin/a-handy-guide-to-the-mesos-kubernetes-swarm-jungle-ad6bc086c736#.se1lxemw3)
- [Comparison of Container Schedulers](https://medium.com/@ArmandGrillet/comparison-of-container-schedulers-c427f4f7421#.ymvq3dg1v)
- [Docker Swarm vs Kubernetes](https://www.upcloud.com/blog/docker-swarm-vs-kubernetes/)
- [The Present State of Container Orchestration](https://thenewstack.io/tns-research-present-state-container-orchestration/)

[1]: https://docs.docker.com/swarm/overview/
[2]: https://www.docker.com/
[3]: https://github.com/docker/swarm/wiki/1.0.0-Milestone-Project-Page
[4]: https://en.wikipedia.org/wiki/Apache_License
[5]: https://kubernetes.io/
[6]: https://www.cncf.io/
[7]: https://github.com/kubernetes/kubernetes/releases/tag/v1.0.0
[8]: http://mesos.apache.org/
[9]: http://www.apache.org/
[10]: http://mesos.apache.org/blog/mesos-1-0-0-released/
[11]: https://www.nomadproject.io/
[12]: https://www.hashicorp.com/
[13]: https://en.wikipedia.org/wiki/Mozilla_Public_License
[14]: http://web.eecs.umich.edu/~mosharaf/Readings/Omega.pdf
[15]: https://medium.com/@mustwin/a-handy-guide-to-the-mesos-kubernetes-swarm-jungle-ad6bc086c736#.b9s4qvu66
[16]: http://blog.kubernetes.io/2016/07/rktnetes-brings-rkt-container-engine-to-Kubernetes.html
[17]: http://thenewstack.io/mesos-simplifies-support-container-formats-unified-containerizer/
[18]: http://mesos.apache.org/documentation/latest/container-image/
[19]: https://www.nomadproject.io/docs/drivers/docker.html
[20]: https://www.nomadproject.io/docs/drivers/rkt.html
[21]: https://www.nomadproject.io/docs/drivers/index.html
[22]: https://docs.docker.com/engine/swarm/
[23]: https://kubernetes.io/docs/user-guide/connecting-applications/
[24]: https://mesosphere.github.io/mesos-dns/
[25]: https://www.nomadproject.io/docs/service-discovery/
[26]: https://blog.docker.com/2017/02/docker-secrets-management/
[27]: https://kubernetes.io/docs/user-guide/secrets/
[28]: https://github.com/mesosphere/marathon/issues/2295
[29]: https://www.nomadproject.io/docs/vault-integration/index.html
[30]: https://docs.docker.com/compose/environment-variables/
[31]: https://kubernetes.io/docs/user-guide/configmap/
[32]: http://elasticcompute.io/2016/02/28/application-configuration-management-with-mesos/
[33]: https://www.nomadproject.io/docs/job-specification/env.html
[34]: https://docs.docker.com/engine/admin/logging/overview/
[35]: http://logz.io/learn/complete-guide-elk-stack/
[36]: https://kubernetes.io/docs/user-guide/logging/elasticsearch/
[37]: https://kubernetes.io/docs/user-guide/logging/overview/
[38]: https://mesos.apache.org/documentation/latest/logging/
[39]: https://www.nomadproject.io/docs/operating-a-job/accessing-logs.html
[40]: https://technologyconversations.com/2016/11/07/collecting-metrics-and-monitoring-the-cluster/
[41]: https://kubernetes.io/docs/user-guide/monitoring/
[42]: http://mesos.apache.org/documentation/latest/monitoring/
[43]: https://www.nomadproject.io/docs/operating-a-job/resource-utilization.html
[44]: https://docs.docker.com/engine/swarm/admin_guide/#/operating-manager-nodes-in-a-swarm
[45]: https://kubernetes.io/docs/admin/ha-master-gce/
[46]: http://mesos.apache.org/documentation/latest/high-availability/
[47]: https://www.nomadproject.io/docs/internals/architecture.html
[48]: https://kubernetes.io/docs/user-guide/load-balancer/
[49]: https://mesosphere.github.io/marathon/docs/service-discovery-load-balancing.html
[50]: https://medium.com/@mustwin/service-discovery-and-load-balancing-with-hashicorps-nomad-db435c590c26#.2sz1qebib
[51]: https://docs.docker.com/engine/userguide/networking/
[52]: https://kubernetes.io/docs/admin/networking/
[53]: http://mesos.apache.org/documentation/latest/networking-for-mesos-managed-containers/
[54]: https://www.nomadproject.io/docs/job-specification/network.html
[55]: https://docs.docker.com/engine/swarm/swarm-tutorial/rolling-update/
[56]: https://kubernetes.io/docs/user-guide/deployments/
[57]: https://mesosphere.com/blog/2015/04/02/continuous-deployment-with-mesos-marathon-docker/
[58]: https://www.nomadproject.io/docs/operating-a-job/update-strategies/
[59]: https://docs.docker.com/docker-cloud/apps/service-scaling/
[60]: https://kubernetes.io/docs/user-guide/horizontal-pod-autoscaling/
[61]: https://docs.mesosphere.com/1.8/usage/tutorials/autoscaling/cpu-memory/
[62]: https://github.com/hashicorp/nomad/issues/871
[63]: https://blog.docker.com/2016/06/docker-1-12-built-in-orchestration/
[64]: https://kubernetes.io/docs/whatisk8s/
[65]: https://www.digitalocean.com/community/tutorials/an-introduction-to-mesosphere
[66]: https://www.hashicorp.com/c1m.html
[67]: https://docs.docker.com/engine/reference/commandline/stack_deploy/
[68]: https://mesosphere.github.io/marathon/docs/application-basics.html
[69]: https://www.nomadproject.io/docs/job-specification/index.html
[70]: https://kubernetes.io/docs/tasks/configure-pod-container/define-environment-variable-container/
[71]: https://blog.docker.com/2016/06/docker-1-12-built-in-orchestration/
[72]: https://docs.docker.com/swarm/discovery/
[73]: https://docs.docker.com/swarm/multi-manager-setup/
[74]: https://docs.docker.com/swarm/networking/
[75]: https://docs.docker.com/engine/tutorials/dockervolumes/
[76]: https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/
[77]: http://mesos.apache.org/documentation/latest/persistent-volume/
[78]: https://github.com/hashicorp/nomad/issues/150#issuecomment-249041670
[79]: https://github.com/kubernetes/minikube
