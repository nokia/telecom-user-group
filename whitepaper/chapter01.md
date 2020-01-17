# 1. Cloud Native Thinking for Telecommunications

Basic tenets and end users suggestions on how cloud native design and principles can be applied to mission critical telecommunications functions.

## Table of Contents
* [1.1 Introduction](#1.1)
* [1.2 What is Cloud Native?](#1.2)
* [1.3 Defining Cloud Native Systems](#1.3)
  * [1.3.1 What "loosely coupled" means in cloud native systems](#1.3.1)
  * [1.3.2 Cloud native applications require orchestration](#1.3.2)
  * [1.3.3 Infrastructure, Deployment and Configuration of Cloud Native Systems](#1.3.3)
* [1.4 Cloud Native Network Functions](#1.4)
* [1.5 Cloud Native for Telcos](#1.5)
  * [1.5.1 A Brief History of Virtualisation for Telcos](#1.5.1)
  * [1.5.2 Software Defined Networking And The Emergence of VNFs](#1.5.2)
  * [1.5.3 Principles for Cloud Native Telco Infrastructure and Applications](#1.5.3)
  * [1.5.4 Evolving the Stack From VNFs to CNFs](#1.5.4)
* [1.6 Cloud Native for Telcos in Practice](#1.6)
* [1.7 Conclusion](#1.7)

<a name="1.1"></a>
## 1.1 Introduction

Kubernetes or containers for workloads has celebrated its 5th Birthday recently , during this time all industry has seen wider support and adoption of this technology to build the infrastructure . It is logical that operators worldwide who have already embarked on an ambitious journey to transformation show interest in to it as a catalyst to support transformation . It will not only makes a perfect business senses to do so but it will enable networks and applications to be treated alike IT or web applications , a promise if fulfilled will support rapid digitisation and cloudification of networks. This is why understanding cloud native journey from an operator’s community perspective is so important.

The journey has already begun ..In fact. If you use voicemail on a wireless network powered by Bell Canada, your message queue is officially cloud native. In 2019, Bell Canada ported its voicemail network functions over to a container-based architecture running on top of a Kubernetes orchestration layer alongside its production instance of the ONAP architecture. Voicemail is one of a number of functions that Bell Canada has or will be migrating to Cloud Native Network Functions (CNFs). “The main driver behind cloud native for Bell Canada is service availability, namely, how can we leverage cloud native principles to make sure our services are more agile, more flexible, and more resilient?,” explains Daniel Bernier, a Senior Technical Architect at Bell Canada and a member of Cloud Native Computing Foundation’s (CNCF) Telecom User Group (TUG).

Telecommunications companies provide some of the most critical services in the world. From emergency 911 services to air traffic control to buy-sell signals that move billions of dollars worth of bonds, telecommunications networks impact our safety, social stability, and economic prosperity.. Because the stakes are so high, telecommunications infrastructure has been designed, maintained, and upgraded to minimise risks and maximise reliability and uptime.

Operators like Bell Canada intend to move more of their functionality to cloud native architectures as the telecommunications community further evolves standards and practices around deployment of mission critical applications and services over CNFs. The goal of this whitepaper is to help companies like telecom operators, as well as enterprises running internal telecommunications-like infrastructure, to better understand what cloud native means for telcos and help build consensus around industry adoption of cloud native technologies.

<a name="1.2"></a>
## 1.2 What is Cloud Native?

After a collaborative discussion, the CNCF published the following [definition](../../toc/blob/master/DEFINITION.md) of cloud native:

“Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach. These techniques enable loosely coupled systems that are resilient, manageable, and observable. Combined with robust automation, they allow engineers to make high-impact changes frequently and predictably with minimal toil.”

<a name="1.3"></a>
## 1.3 Defining Cloud Native Systems

There are some additional key principles to cloud native that are important to grasp in order to think more broadly about architecting cloud native technologies for complex systems.A fundamental principle of cloud native for telco apps is that their underlying telco systems conform to the core precepts of cloud native architecture. The lack of exceptions makes the rule, because the entire advantage of cloud native is driven by decomposability and abstraction from physical infrastructure. By deviating even slightly from these core principles, the service provider stands to lose the workload portability and minimal toil that drew them to cloud native approaches in the first place.

<a name="1.3.1"></a>
### 1.3.1 What "loosely coupled" means in cloud native systems

Cloud native systems work on the principle of breaking a larger monolithic application in to a fine tuned components  that is based on have a clear separation between their microservices. The separation is based on a technology like containers which will allow to deploy each of this split software component on an independent set of container infrastructure. Cloud native applications and systems generally benefit from segregating as many services as possible into different containers. Additional benefits of cloud native architectures include scalability (vertical and horizontal) per microservice. This simplifies deployment in a wide variety of infrastructure environments, ranging from endpoint device to edge station to large data centres. It also allows service providers to deploy resources in the most efficient manner possible while maintaining necessary service levels for regulated and unregulated service types.

The delivery of microservice software harnesses the existing group boundaries within an organisation and works with, not against, the different rates of change and business capabilities residing within those boundaries. This allows events such as security patches to be rolled out faster and easier because they don't have to be deployed in lock-step with other parts of the application.

While one microservice per container is the ideal state for cloud native applications, the reality is not always so clean and simple. It is entirely possible and sometimes required to run multiple microservices in a single container, and even to deploy very large containers for aggregations of services that are difficult or impossible to decouple due to software or network limitations. However, the general idea behind cloud native is to decompose microservices into the smallest possible infrastructure unit allowable to run the microservice and shift the burden of orchestration to the orchestration layer.

The delivery of software as microservices enables effective parallel development and communication across an organisation and works with, not against, the different rates of change and business capabilities residing within those boundaries. This allows events such as security patches to be rolled out faster and easier because they don't have to be deployed in lock-step with other parts of the application. Cloud native applications also have all of their runtime dependencies packaged with them during the build phase which is then used for deployment. This allows for individual business units and operations teams to care and maintain for their software with less risk of other stakeholders disrupting their service’s “uptime”. In practice, this allows for scenarios such as owner of service “X” being able to theoretically scale their chosen software independent of service “Y”. These potentially clear lines of demarcation provide a paradigm that makes sense to legacy operations groups who are being forced to rapidly assess how they’ve delegated roles and responsibilities.

<a name="1.3.2"></a>
### 1.3.2 Cloud native applications require orchestration

Because they are loosely coupled, cloud native services are always managed by an application orchestrator, such as Kubernetes. As cloud native applications are built from a loosely coupled collection of services which are delivered via an API, this coordination function is paramount, not only for reliability but also for performance and resiliency. In addition, from an operational standpoint, an orchestrator is necessary to manage and deploy these services; manual deployment and LCM meshing of these services and applications would be complex, error-prone, and overly resource intensive.

The orchestration layer is tasked with composing, decomposing, and reshaping or resizing the resources assigned to specific applications provided by the infrastructure. It does this based on assessments and monitoring of performance and availability of the actual infrastructure used by application. In that manner, the applications are the “brains”, directing the orchestration layer towards functional goals and outcomes (for example, low latency or specific uptime and resiliency metrics). Thus, the objective of orchestration is to create an entity that aggregates the microservices into services which can be easily mapped to network functions.

<a name="1.3.3"></a>
### 1.3.3 Infrastructure, Deployment and Configuration of Cloud Native Systems

[Immutable infrastructure](https://docs.google.com/document/d/1fwV3vZB5IgHb6uUgQpHts9mFR0HheYbIrlg9hGfWYfA) (the orchestrator and all of the software and hardware that it depends on) is provisioned using baked and versioned templates (e.g. server images) or a combination of templates and bootstrapping (some repeatable and versioned process that is applied to the template e.g. Kubeadm).  The underlying infrastructure is not changed after it is made ready for use. New changes to the infrastructure are rolled out as new instances of infrastructure. By separating the application layer from the infrastructure layer, it is possible to iterate faster with minimal dependency risk. Similarly it enables the vision of programmable and software defined infrastructure that can made possible to automate end to end deployment .

In cloud native systems, the atomic unit of deployment is the container, on an immutable and decoupled compute environment that nearly completely abstracts function from the underlying physical infrastructure and network architecture. At present, the most commonly used container environment is an OCI-compliant implementation. A container is different than a Virtual Machine (VM), which was the initial base unit of cloud computing. A VM hosts a Guest OS capable of delivering a service's required compute and networking. This guest runs on top of a hypervisor consuming the virtual infrastructure and orchestration it provides. In contrast, containers run on top of a shared Host OS (with a shared kernel) kernel. This distinction is key because containerisation enables immutability, disposability and resource efficiency in ways that are not easily achievable with VMs.

For Kubernetes specifically, the atomic unit of management is a PodOD. A PodOD is a set of containers co-located in the same or different host and sharing the same Linux networking namespace.  For telco (and other) cloud native apps, the PodOD is the basic building block of deployment, scaling operations, and upgrades.

Cloud native applications consist of sets of cloud native microservices. The configuration of these microservices is not changed after deployment (note, this does allow for changes in application data such as "add a new user"). New features for a cloud native application and the underlying PodODs are rolled out as new artefacts and new configuration. Cloud native systems are configured declaratively. This means that the system configuration declares “what” a loosely coupled system should look like, not ”how” the system should be created. The “how” of the application is determined by the tooling (e.g. the orchestrator, operators, and CRDs).

<a name="1.4"></a>
## 1.4 Cloud Native Network Functions

Three types of definitions:
1. **Analogous**: This piece is *similar* to that piece
1. **Contrasting**: This is the new way, this is the old way
1. **Aliasing**: This piece *is* that piece

ALT4.6:
>A cloud native network function is a cloud native application that implements one or more Network Functions. A cloud native network function consists of one or more microservices, and has been developed using Cloud Native Principles including immutable infrastructure, declarative APIs and a “repeatable deployment process”. Network Functions in the telecommunications context are defined by standards (3GPP) when it comes to functional scope (e.g. S-GW) and interfaces (e.g. S1).
>
>Note: ETSI defines a Network Function as “a functional block within a network infrastructure”, such functional block - similarly to a cloud native network function - can correspond to one or more 3GPP defined network functions.

ALT4.8:
>A cloud native network function is a cloud native application that implements or facilitates network functionality. A cloud native network function consists of one or more microservices, and has been developed using Cloud Native Principles including immutable infrastructure, declarative APIs and a “repeatable deployment process”.
>
>An example of a simple CNF is a packet filter which implements a single piece of network functionality as a microservice. A firewall is an example of a CNF which may be composed of more than one microservice.
>
>The CNFs themselves, by nature of following cloud native principles, are also composable and can implement and facilitate more complex network functionality if needed.
>
>A more complex network service example, which might be implemented using cloud native principles, is the LTE S1 protocol stack which connects an LTE RAN with an evolved packet core (EPC) and components which use the S1 protocol stack such as a Serving Gateway (S-GW). [ref. ETSI TS 136 410

<a name="1.5"></a>
## 1.5 Cloud Native for Telcos

<a name="1.5.1"></a>
### 1.5.1 A Brief History of Virtualisation for Telcos

Until the 1990’s  1990s, most functionality and applications for telecommunications resided primarily in physical hardware (aka ‘boxes’). While software powered these systems, the software functioned more like firmware and was not easy to abstract and run on multiple platforms in virtual environments.

This fostered a “top-down” approach to telecommunications systems that were imperative rather than declarative. This approach was exceptionally resource intensive and expensive; redundancy literally meant acquiring multiple physical instances of required systems. Not surprisingly, this guiding architectural decision encouraged the tight bundling of numerous services and capabilities into individual physical systems. This resulted not only in inflated infrastructure and provisioning costs but also inefficient hyper-redundancy in system engineering for overlapping capabilities.

<a name="1.5.2"></a>
### 1.5.2 Software Defined Networking And The Emergence of VNFs

In the late 1990s, the concept of virtualisation for enterprise computing garnered interest as enterprises tired of spending large sums of money on high-powered servers. Simultaneously, we saw the rapid rise in popularity of the commodity Open Source Linux Operating System. In 1999, VMware released its first virtualisation product for x86 devices. In the early 2010s, the concept of Network Functions Virtualisation (NFV) emerged as telcos and other users of big networking gear sought to virtualise their networking functionality, enhance resiliency, and take advantage of commodity hardware. The concept of NFV encapsulated Virtual Network Functions (VNFs) , Network Function Infrastructure (NFVI) and an orchestration component (MANO). The entire NFV hardware and software stack could be integrated and distributed across geographically dispersed data centres. In 2017, ONAP emerged as the open source standard platform for orchestrating and automating physical and virtual network elements with full lifecycle management. NFV and ONAP primarily focused on creating and orchestrating virtual analogs for physical equipment - virtual boxes.

This was the same pattern followed during server virtualisation, when initial efforts focused on replicating physical servers as virtual entities. Cloud native however, requires a more fundamental redesign and rethink of how telco and backbone/core network systems function. In that sense, as well, cloud native for telco is actually not dissimilar from forklifting over monolithic legacy applications into virtual environments and then decoupling the tightly bundled functions and processes to create a more resilient, manageable, and performant infrastructure that derives immutability precisely from its ephemerality. In reality, CNFs will be introduced alongside VNFs and PNFs (physical network functions) and will need to fit into operational models that govern those earlier types of network functions. Additionally, CNFs will require the capability to be orchestrated by management systems already present in the service providers' networks.

<a name="1.5.3"></a>
### 1.5.3 Principles for Cloud Native Telco Infrastructure and Applications

At its core, the evolution from box-centric to process and function-centric requires an evaluation of the OSI Layers through a cloud native lens. The best general practices of cloud native infrastructure deployment and application design should also be applied to networking infrastructure Two key shifts required for CNFs to function well are deployment pipelines and the use of declarative programming and scripts in configuration. By pipelines, we mean the use of continuous integration (CI) and continuous delivery / deployment (CD) platforms. This is fundamental because it allows for rapid iteration, proper versioning, easier rollbacks, canary testing, and many other capabilities that are presently complex and often not possible in deploying VNFs. By declarative language, we mean a shift to intelligent orchestration that is better able to  maintain required service levels and maximise efficiencies based on available resources. This will ultimately mean a transition of network intelligence and design  - function, description, and configuration -  into other parts of Kubernetes (Helm Charts and CRDs).

<a name="1.5.4"></a>
### 1.5.4 Evolving the Stack From VNFs to CNFs

The emergence of Kubernetes as the most widely used container orchestration layer allows telecommunications operators to shift their infrastructure over from more bespoke, expensive, and higher friction stacks to a de facto standard platform while also improving performance and resiliency. The malleability of Kubernetes should allow a gradual transition from legacy VNFs built on OpenStack or VMWare over to a Kubernetes telco stack that accommodates all aspects of their business - including legacy VNFs, which can be easily managed via an abstraction layer on top of Kubernetes (KubeVirt/Virtlet/Openstack).

Back-office applications, such as BSS and OSS functions, can run directly on Kubernetes and will enjoy all the same benefits that enterprise applications derive from Kubernetes. Operators should also be able to run real-time, critical functions on Kubernetes. CNFs must be able to  run  on Kubernetes and benefit directly and strongly from cloud native principles. It is important to note that, in theory, Kubernetes and containerisation should allow for true cloud-blind immutability and portability. This will only be true if conforming Kubernetes versions and configurations are used and supported by operators. That said, creating a conformance model for Kubernetes for telecommunications is non-trivial, requiring validation and certification of key elements such as network software (CNI plug-in, network service mesh, etc.) and other aspects.

<a name="1.6"></a>
## 1.6 Cloud Native For Telcos In Practice
Likely deployment pattern for cloud native applications into telcos will move from functions that are not as latency sensitive or as fault intolerant (voicemail, OSS/BSS, etc) to more critical functions such as the backbone cores. Telcos will gain on multiple fronts by deploying cloud native systems. Those benefits include operational consistency, application resilience, simplified and responsive scaling at the microservice level, simplified integration with enterprise-facing cloud native applications, and improved portability between public, private, and hybrid cloud environments. Another key improvement would be transparency, observability, and control, all of which would be increased by operating network functions under a Kubernetes umbrella as opposed to operating purpose-built boxes. Because it is so much simpler to instrument and observe at the service level in Kubernetes running microservices, telco operators should also benefit from built-in tools and metrics.

As cloud native involves decomposing tightly coupled processes into loosely coupled microservice, rearchitecting applications for CNFs often will entail decomposing functional aspects into services running in discrete containers or as separate microservices. For an example of how cloud native telecommunications principles might work in practice, consider a UTM (universal threat management) firewall. These are generally large physical or virtual appliances that encompasses multiple functions including: DDoS protection, IP filtering, VPN provisioning and termination, stateful packet inspection, and anti-virus / spam filtering. They are complicated to troubleshoot and a clear single point of failure for multiple critical functions. UTMs are also, by design, decidedly imperative - making them brittle and poor handlers of edge cases. UTMs cannot be easily managed via CI/CD and standard DevOps practices.  

Through a cloud native lens, all of the functions of the UTM could be decomposed as microservices, each functioning as its own application, running in it is own container (or containers). These services could be controlled and monitored from aa single management plane, giving the operator the same visibility into what’s happening and the same ability to manage the composed whole, but offering additional granularity on service performance. This should also allow for easier bursting to handle outlier events (spikes) and for running security infrastructure as an agile pipeline rather than a cumbersome snake. Additionally, if one microservice fails, other services in the meshed CNFs would remain functional, resulting in improved overall resiliency.Similarly this architecture will support vision of network services on the common infrastructure that can scale and enhance performance and reliability in the most optimum manner and in operational environment to address DevOps models in the most adequate manner .

The manipulation of namespaces and multi-tenancy within the orchestration layer will be crucial for operators if they are to deploy these examples at scale. For there to be any hope of gaining a return on investment, smarter deployments of the infrastructure will be as important as the deployment of the CNF itself. Building upon the UTM example, if it and subsequent CNFs adhere to the cloud native design philosophies, then it should be feasible to deploy them into a single Kubernetes cluster, leveraging the available tooling to ensure logical isolation/segmentation.

If the CNF has extreme opinions on what the infrastructure must provide i.e. “CNF-X will only run in a 3rd-party-provided Kubernetes deployment”), then a lot of economy of scale in both infrastructure costs and operational simplicity is quickly eroded. For example, if an operator must run multiple types of Kubernetes for different CNFs, then the infrastructure and required orchestration software is no longer a commodity and each CNF suite may require more masters and instances of etcd than is economical. Additionally, the different flavours of Kubernetes will require different operational playbooks and potentially will inject more complexity into analytics, application performance monitoring, and infrastructure management.  Looking at a provider’s far edge, it is highly infeasible to assume that a cupboard sized data centre will be cost effective if the expectation is for it to host an instance of Kubernetes per application. At the same time, a conforming “Plain Vanilla” flavour of Kubernetes for telcos would also need to run on all multiple infrastructure components including X86, ARM and RISC due to the different infrastructure composition of centralised data centres and edge data centres.

<a name="1.7"></a>
## 1.7 Conclusion
Telecommunications services demand a higher bar for resiliency, security, and performance than nearly any other set of services. Our society increasingly relies on our telecommunications infrastructure for critical capabilities that keep us safe and allow us to conduct research, commerce, and our daily lives.

This high bar was attained at a high price. Traditionally, telecommunications infrastructure and applications have been designed in tightly composed physical or virtual units in order to better control the software stack and with a model of redundancy and resiliency derived from ready overcapacity. This has also ensured that deployment of new applications is complicated and often slow; tightly-bundled applications are not easy to modify and cannot be provisioned or versioned with modern DevOps tools. Thus, telecommunications progress was usually quite expensive, both in implementation and physical infrastructure. The reliance on custom-made telecommunications platforms meant it was necessary to retain and rely on architects and consultants with arcane expertise in those bespoke platforms.

The great promise of cloud native for telecommunications is to turbocharge the development and improvement of telecommunications applications by finally allowing these critical services to run on largely commodity physical infrastructure, and to finally decouple them from purpose-built boxes. In addition, customised, tightly-coupled and hardware-bound telecommunications platforms can give way to Kubernetes, enhancing modularity, scalability, observability and operability. This transition in general will open a venue for the telecommunications industry to benefit from the dynamic and vigorous community sprawling around Kubernetes. In general adopting cloud-native ways should deliver on promises to become more agile, responsive, and adaptive both internally and externally that are main agenda points for telecommunications industry already for some time and years to come.  Moreover, the telecommunications industry  stands to benefit even more than enterprises because the implications for reducing CapEx and improving the speed of application development (and by extension, service improvement) are profound.

Telcos have traditionally struggled to keep pace with startup technology companies in deploying newer software-driven technologies because they played by a different set of rules - the “Rules of the Boxes” and strict regulatory rules defining service delivery and reliability. In the cloud native realm, boxes can be broken up into distributed CNFs composed of microservices and following cloud native principles.

As a result, telcos will be able to freely test, design, deploy, provision, revise, and ultimately innovate at a far greater pace. With process and organisation adaptations to cloud native thinking and design, telcos will be able to leverage this new freedom to build more resilient infrastructure and applications, and to accelerate the roll out of new features and new capabilities more quickly with less risk and less fear of disrupting critical regulated systems and functions.

Work is ongoing to bring the most demanding and mission critical telecommunications systems to cloud native, including those that must fulfil regulatory requirements (including emergency call handling). However, in theory, CNFs running on Kubernetes should provide equivalent regulatory compliance for the same reasons that cloud native applications for enterprises tend to be more fault-tolerant, more responsive, and more resilient; because loosely coupled, immutable systems are inherently better at handling highly complex applications with strict SLAs and multiple dependent and interactive functions. This is the significant promise of cloud native for telecommunications applications and functions.

Contributors: Daniel Bernier, [Tom Kivlin](@tomkivlin), Gergely Castari, Tamas Zsiros, Jeff Saelens, Khawaja Daniyal, Bill Mulligan, Taylor Carpenter, Wavell Watson, Frederick Kautz, Herbert Damker, Ildiko Vancsa, Dave Cremins, Henrik Saveedra Persson, Dan Kohn, Saad Sheikh, Lei Wang, Ervins Kampans