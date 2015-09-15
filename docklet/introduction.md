<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. Introduction of DCOS</a>
<ul>
<li><a href="#sec-1-1">1.1. why we need a data center operation system?</a>
<ul>
<li><a href="#sec-1-1-1">1.1.1. Managing a datacenter was very hard, recently the popular of microservices and big data frameworks make it worse. we need a tool to manage the whole resources of a data center, including computing, storages, network infrastructures, and to provide a unified interface to control, monit the whole datacenter. The main challenges are to improve resource utilization and to make it user-friendly.</a></li>
</ul>
</li>
<li><a href="#sec-1-2">1.2. what types of workloads can I run on DCOS?</a></li>
<li><a href="#sec-1-3">1.3. What are some popular use cases for Mesos and the DCOS?</a></li>
<li><a href="#sec-1-4">1.4. what are the main advantages of DCOS over othere solutions, such as CoreOS+Kubernetes or Openstack?</a>
<ul>
<li><a href="#sec-1-4-1">1.4.1. run everything on the same shared cluster</a></li>
<li><a href="#sec-1-4-2">1.4.2. scaling the elastic datacenter</a></li>
<li><a href="#sec-1-4-3">1.4.3. simple, powerful interfaces</a></li>
</ul>
</li>
<li><a href="#sec-1-5">1.5. how is the mesosphere DCOS different from apache mesos?</a></li>
<li><a href="#sec-1-6">1.6. how is DCOS cluster different from a private cloud, or from virtualization?</a></li>
<li><a href="#sec-1-7">1.7. how is DCOS different from other container technologies, such as Kubernetes and Dcoker?</a></li>
</ul>
</li>
<li><a href="#sec-2">2. Introduction of CoreOS+KubernetesOSS (Operational Support System)</a>
<ul>
<li><a href="#sec-2-1">2.1. why we should use containers?</a>
<ul>
<li><a href="#sec-2-1-1">2.1.1. Application-centric management:</a></li>
<li><a href="#sec-2-1-2">2.1.2. Dev and Ops separation of concerns:</a></li>
<li><a href="#sec-2-1-3">2.1.3. Agile application creation and deployment:</a></li>
<li><a href="#sec-2-1-4">2.1.4. Continuous development, integration, and deployment:</a></li>
<li><a href="#sec-2-1-5">2.1.5. Loosely coupled, distributed, elastic, liberated micro-services:</a></li>
<li><a href="#sec-2-1-6">2.1.6. Environmental consistency across development, testing, and production:</a></li>
<li><a href="#sec-2-1-7">2.1.7. Cloud and OS distribution portability:</a></li>
<li><a href="#sec-2-1-8">2.1.8. Resource isolation:</a></li>
<li><a href="#sec-2-1-9">2.1.9. Resource utilization:</a></li>
</ul>
</li>
<li><a href="#sec-2-2">2.2. what is kubernetes</a></li>
<li><a href="#sec-2-3">2.3. the use cases of kubernetes</a>
<ul>
<li><a href="#sec-2-3-1">2.3.1. targets</a></li>
<li><a href="#sec-2-3-2">2.3.2. benefits</a></li>
</ul>
</li>
<li><a href="#sec-2-4">2.4. main advantages:</a></li>
<li><a href="#sec-2-5">2.5. Design Overview</a></li>
</ul>
</li>
<li><a href="#sec-3">3. Introduction of Docklet</a>
<ul>
<li><a href="#sec-3-1">3.1. Motivation</a>
<ul>
<li><a href="#sec-3-1-1">3.1.1. why we should use containers?</a></li>
<li><a href="#sec-3-1-2">3.1.2. docklet supports both containers and big data analytics in one data center, achieves higher resource utilization at the same time.</a></li>
</ul>
</li>
<li><a href="#sec-3-2">3.2. the use cases of Docklet</a>
<ul>
<li><a href="#sec-3-2-1">3.2.1. target</a></li>
<li><a href="#sec-3-2-2">3.2.2. benefits</a></li>
</ul>
</li>
<li><a href="#sec-3-3">3.3. main advantages</a>
<ul>
<li><a href="#sec-3-3-1">3.3.1. open source</a></li>
<li><a href="#sec-3-3-2">3.3.2. lean</a></li>
<li><a href="#sec-3-3-3">3.3.3. portable</a></li>
<li><a href="#sec-3-3-4">3.3.4. extensible</a></li>
</ul>
</li>
<li><a href="#sec-3-4">3.4. how is Docklet different from DCOS?</a>
<ul>
<li><a href="#sec-3-4-1">3.4.1. open source</a></li>
<li><a href="#sec-3-4-2">3.4.2. lightweight</a></li>
</ul>
</li>
<li><a href="#sec-3-5">3.5. how is Docklet different from Kubernetes?</a></li>
</ul>
</li>
</ul>
</div>
</div>

# Introduction of DCOS<a id="sec-1" name="sec-1"></a>

## why we need a data center operation system?<a id="sec-1-1" name="sec-1-1"></a>

### Managing a datacenter was very hard, recently the popular of microservices and big data frameworks make it worse. we need a tool to manage the whole resources of a data center, including computing, storages, network infrastructures, and to provide a unified interface to control, monit the whole datacenter. The main challenges are to improve resource utilization and to make it user-friendly.<a id="sec-1-1-1" name="sec-1-1-1"></a>

## what types of workloads can I run on DCOS?<a id="sec-1-2" name="sec-1-2"></a>

The DCOS can run nearly any type of workload. Among the dozens of services it supports are databases such as Cassandra and MemSQL; big data systems such as Hadoop and Spark; and orchestration services like Marathon and Kubernetes for hosting long-running and cloud-native applications.

## What are some popular use cases for Mesos and the DCOS?<a id="sec-1-3" name="sec-1-3"></a>

Although the DCOS supports nearly every type of workload, it is especially popular for supporting Platform-as-a-Service (PaaS) offerings, big data analytics (e.g., Hadoop, Spark and Kafka), as well as stateful services such as HDFS, Cassandra and MemSQL. Coming soon will be support for even more diverse services, including traditional SQL databases such as MySQL.

## what are the main advantages of DCOS over othere solutions, such as CoreOS+Kubernetes or Openstack?<a id="sec-1-4" name="sec-1-4"></a>

### run everything on the same shared cluster<a id="sec-1-4-1" name="sec-1-4-1"></a>

Gone are the days of 12-15% datacenter and cloud utilization. The DCOS multiplexes all of your workloads across the entire cluster, automatically "bin-packing" applications onto shared machines for maximum utilization.

### scaling the elastic datacenter<a id="sec-1-4-2" name="sec-1-4-2"></a>

Your infrastructure needs aren't static, and neither is the DCOS. We make it easy to add new resources to the pool as your business grows and new services come online.

### simple, powerful interfaces<a id="sec-1-4-3" name="sec-1-4-3"></a>

It has never been easier to deploy distributed services or view the health of tens of thousands of servers.

## how is the mesosphere DCOS different from apache mesos?<a id="sec-1-5" name="sec-1-5"></a>

The DCOS is a robust and commercially supported software product that is built on top of the open source Mesos. Major improvements in the DCOS include its command line and web interfaces, its simple packaging and installation, and its growing ecosystem of technology partners.

## how is DCOS cluster different from a private cloud, or from virtualization?<a id="sec-1-6" name="sec-1-6"></a>

The DCOS is the next-generation private cloud. It’s different from software involving virtual machines because the DCOS organizes servers of any kind — physical, virtual or cloud — into a single pool of shared resources. Its Mesos core dynamically provisions the necessary compute, memory and storage resources, rather than preconfigured machine images.

## how is DCOS different from other container technologies, such as Kubernetes and Dcoker?<a id="sec-1-7" name="sec-1-7"></a>

The DCOS supports both Kubernetes and Docker. Because the DCOS manages infrastructure at the server level and runs directly atop Linux servers, it is able to launch Docker containers at scale. Mesosphere and Google have collaborated to bring Kubernetes to DCOS, where Kubernetes talks directly to the DCOS API and runs like any other DCOS service.

# Introduction of CoreOS+KubernetesOSS (Operational Support System)<a id="sec-2" name="sec-2"></a>

## why we should use containers?<a id="sec-2-1" name="sec-2-1"></a>

### Application-centric management:<a id="sec-2-1-1" name="sec-2-1-1"></a>

Raises the level of abstraction from running an OS on virtual hardware to running an application on an OS using logical resources. This provides the simplicity of PaaS with the flexibility of IaaS and enables you to run much more than just 12-factor apps.

### Dev and Ops separation of concerns:<a id="sec-2-1-2" name="sec-2-1-2"></a>

Provides separatation of build and deployment; therefore, decoupling applications from infrastructure.

### Agile application creation and deployment:<a id="sec-2-1-3" name="sec-2-1-3"></a>

Increased ease and efficiency of container image creation compared to VM image use.

### Continuous development, integration, and deployment:<a id="sec-2-1-4" name="sec-2-1-4"></a>

Provides for reliable and frequent container image build and deployment with quick and easy rollbacks (due to image immutability).

### Loosely coupled, distributed, elastic, liberated micro-services:<a id="sec-2-1-5" name="sec-2-1-5"></a>

Applications are broken into smaller, independent pieces and can be deployed and managed dynamically &#x2013; not a fat monolithic stack running on one big single-purpose machine.

### Environmental consistency across development, testing, and production:<a id="sec-2-1-6" name="sec-2-1-6"></a>

Runs the same on a laptop as it does in the cloud.

### Cloud and OS distribution portability:<a id="sec-2-1-7" name="sec-2-1-7"></a>

Runs on Ubuntu, RHEL, on-prem, or Google Container Engine, which makes sense for all environments: build, test, and production.

### Resource isolation:<a id="sec-2-1-8" name="sec-2-1-8"></a>

Predictable application performance.

### Resource utilization:<a id="sec-2-1-9" name="sec-2-1-9"></a>

High efficiency and density.

## what is kubernetes<a id="sec-2-2" name="sec-2-2"></a>

Kubernetes is an open-source platform for automating deployment, scaling, and operations of application containers across clusters of hosts.
Kubernetes is the leading role in CNCF (Cloud Native Computing Foundation) which will create and drive the evolution of technologies that are container packaged, dynamically scheduled and microservices oriented.

## the use cases of kubernetes<a id="sec-2-3" name="sec-2-3"></a>

### targets<a id="sec-2-3-1" name="sec-2-3-1"></a>

Kubernetes is primarily targeted at applications composed of multiple containers, such as elastic, distributed micro-services. It is also designed to facilitate migration of non-containerized application stacks to Kubernetes. It therefore includes abstractions for grouping containers in both loosely coupled and tightly coupled formations, and provides ways for containers to find and communicate with each other in relatively familiar ways.

### benefits<a id="sec-2-3-2" name="sec-2-3-2"></a>

With Kubernetes, you are able to quickly and efficiently respond to customer demand:
Scale your applications on the fly.
Seamlessly roll out new features.
Optimize use of your hardware by using only the resources you need.

## main advantages:<a id="sec-2-4" name="sec-2-4"></a>

lean: lightweight, simple, accessible
portable: public, private, hybrid, multi-cloud
extensible: modular, pluggable, hookable, composable
self-healing: auto-placement, auto-restart, auto-replication

## Design Overview<a id="sec-2-5" name="sec-2-5"></a>

Kubernetes aspires to be an extensible, pluggable, building-block OSS platform and toolkit. Therefore, architecturally, we want Kubernetes to be built as a collection of pluggable components and layers, with the ability to use alternative schedulers, controllers, storage systems, and distribution mechanisms, and we're evolving its current code in that direction.

# Introduction of Docklet<a id="sec-3" name="sec-3"></a>

## Motivation<a id="sec-3-1" name="sec-3-1"></a>

### why we should use containers?<a id="sec-3-1-1" name="sec-3-1-1"></a>

### docklet supports both containers and big data analytics in one data center, achieves higher resource utilization at the same time.<a id="sec-3-1-2" name="sec-3-1-2"></a>

## the use cases of Docklet<a id="sec-3-2" name="sec-3-2"></a>

### target<a id="sec-3-2-1" name="sec-3-2-1"></a>

private data center of one coorperation

### benefits<a id="sec-3-2-2" name="sec-3-2-2"></a>

docklet supports nearly every kinds of workload, it is especially designed for paas offerings, and big data analytics.

## main advantages<a id="sec-3-3" name="sec-3-3"></a>

### open source<a id="sec-3-3-1" name="sec-3-3-1"></a>

### lean<a id="sec-3-3-2" name="sec-3-3-2"></a>

### portable<a id="sec-3-3-3" name="sec-3-3-3"></a>

### extensible<a id="sec-3-3-4" name="sec-3-3-4"></a>

## how is Docklet different from DCOS?<a id="sec-3-4" name="sec-3-4"></a>

### open source<a id="sec-3-4-1" name="sec-3-4-1"></a>

### lightweight<a id="sec-3-4-2" name="sec-3-4-2"></a>

## how is Docklet different from Kubernetes?<a id="sec-3-5" name="sec-3-5"></a>
