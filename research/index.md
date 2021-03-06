---
layout: article
title: "Cloud Reliability and Resilience"
date:
modified:
excerpt: "excerpt"
tags: []
image:
  feature:
  teaser:
  thumb:
ads: false
toc: true
---  


## Overview
Reliability is a measure of the percentage uptime of cloud services to customers, considering the downtime due to faults. Many cloud providers are setting a reliability level of 99.95% ([download uptime cheat sheet](http://royal.pingdom.com/wp-content/uploads/2015/04/pingdom_uptime_cheat_sheet.pdf)). This means that if you provision a VM it will be available 99.95% of the time, with a possible downtime of 21.6 minutes per month. Reliability is an important characteristic which enables platforms to adapt and recover under stress and remain functional from a customer perspective. You can find additional information from a Meetup meeting on [Cloud Reliability and Resilience](http://www.slideshare.net/JorgeCardoso4/cloud-resilience-with-open-stack).

Every year big companies made the headlines for the wrong reason: reliability problems. In Q1 2016, Microsoft (9 days), Twitter (8h), Apple (7h), are PayPal (7h) are the "lucky" winners:

+ Two separate outages meant [Microsoft's biggest customers haven't had access to email](http://www.businessinsider.de/microsoft-has-a-9-day-long-office-365-outage-2016-1?r=UK&IR=T) for several days.
+ [Twitter Went Down](http://recode.net/2016/01/19/twitter-went-down-because-of-an-internal-code-change/) Because of an ‘Internal Code Change’.
+ eBay, Etsy and Online Merchants Hit by [PayPal Outage](http://www.ecommercebytes.com/C/blog/blog.pl?/pl/2016/3/1457113386.html)
+ [Apple Pay suffers](http://www.theinquirer.net/inquirer/news/2446737/apple-pay-suffers-first-wobble-with-seven-hour-outage) first wobble with seven-hour outage. Problem saw Visa users unable to sign up to iPhone payments service.

According to section of [IEEE Society](http://rs.ieee.org) working on Reliability, "reliability engineering is a design engineering discipline which applies scientific knowledge to assure that a system will perform its intended function for the required duration within a given environment, including the ability to test and support the system through its total lifecycle (...) it is the probability of failure-free software operation for a specified period of time in a specified environment."

Cloud resiliency is the ability of a cloud platform or service to recover and continue operating when failures occur. Automated means for recovery are the most desirable solutions.

### Open Positions
+ MSc thesis. [Reliability of OpenStack usign Fault Injection](http://jorge-cardoso.github.io/research/Master_Thesis_Cloud_Resilience_Reliability_Fault-Library-2016-04-12.pdf)
+ MSc thesis. [Intelligently Instrument OpenStack](http://jorge-cardoso.github.io/research/Master_Thesis_Cloud_Resilience_Reliability_Intelligent_Instrumentation-2016-06-03.pdf).
+ PhD student. OpenStack Reliability
+ PhD student. Data Science.
+ PhD student. Orchestration of cloud services/microservices.
+ Permanent position. [Cloud Reliability Engineer](http://jorge-cardoso.github.io/research/JD_IT_Cloud_Reliability_Engineer_(May 2016).pdf)
+ Permanent position. [OpenStack Software Engineer](http://jorge-cardoso.github.io/research/JD_IT_OpenStack_Software_Engineer_(Jan 2016).pdf)
+ Permanent position. [Junior/Senior Researcher Large-scale Distributed Systems](http://jorge-cardoso.github.io/research/JD_IT_Junior_Senior_Researcher_Large-Scale_Distributed_Systems_(Jul 2016).pdf)


## OpenStack Cloud OS
OpenStack is a cloud operating system (Cloud OS) for building public and private clouds. It can control pools of compute, storage, and networking recourses located in large data centres. It is supported by major IT players in the world which include IBM, HP, Intel, Huawei, Red Hat, AT&T, and Ericsson. At Huawei Research we are currently developing the next generation of reliable cloud platforms for Deutsche Telekom. The Open Telekom Cloud engineered by Huawei and operated by T-Systems was launched at CeBIT 2016 and delivers flexible and convenient cloud services.

<img align="right" src="/images/OTC.png" width="450">

Major players are building competences in the field of cloud reliability. [Microsoft Trustworthy Computing](https://www.microsoft.com/en-us/twc/reliability.aspx) has a division dedicated to Reliability and IBM offers specialized [Resiliency Services](http://www-935.ibm.com/services/us/en/it-services/business-continuity/) to assure continuous business operations and improve overall reliability.

Cloud reliability and resilience of OpenStack can be analyzed and improved at 3 levels:

+ Level 1. OpenStack paltform and services
+ Level 2. Hypervisor and virtual machines (VM) managed
+ Level 3. Applications running inside VMs

We concentrate our efforts on Level 1.

## General Problems with Building Large-scale Distributed Systems

Reliable large-scale distributed systems are hard to build since their validation is time consuming, complex, and often non-deterministic. OpenStack is not an exception. Research from Microsoft with [MODIST](https://www.usenix.org/legacy/event/nsdi09/tech/full_papers/yang/yang_html/) (Junfeng Yang, et al., MODIST: Transparent Model Checking of Unmodified Distributed Systems Proceedings of the 6th Symposium on Networked Systems Design and Implementation (NSDI '09), Pages 213-228) exemplifies well the problems associated with general distributed systems. Experiments found a total of 35 bugs in Berkeley DB, a Paxos implementation, and a primary-backup replication protocol implementation. Thus, validation, testing, and benchmarking frameworks are needed, specifically, when OpenStack is used to support mission critical applications.

Building large-scale distributed systems requires the consideration of several theories, technologies, and methodologies, such as:
+ [CAP Theorem](https://en.wikipedia.org/wiki/CAP_theorem)
+ [Microservices](http://martinfowler.com/articles/microservices.html)
+ [Twelve Factor App](https://12factor.net)


## Available Approaches (Industry solutions, Patents, Research Papers)

### Fault Injection
+ [Fault-injection technologies](https://en.wikipedia.org/wiki/Fault_injection) or FIT provides approaches to demonstrate that software is robustness and fault tolerance by injecting faults to damage internal components to test its fault tolerance.
+ Domenico Cotroneo and Henrique Madeira. [Introduction to software fault injection](http://link.springer.com/chapter/10.1007/978-88-470-2772-5_1). In Domenico Cotroneo, editor, Innovative Technologies for Dependable OTS-Based Critical Systems, pages 1–15. Springer Milan, 2013.
+ Haissam Ziade, Rafic A Ayoubi, Raoul Velazco, et al. [A survey on fault injection techniques](http://ccis2k.org/iajit/PDF/vol.1,no.2/04-Hissam.pdf). Int. Arab J. Inf. Technol., 1(2):171–186, 2004.
+ (Graph-based) In [Towards a Fault-Resilient Cloud Management Stack](https://kabru.eecs.umich.edu/papers/publications/2013/socc2013_ju.pdf), the authors use execution graphs to monitor and observe the processing of external requests. Intrumentation is done between openStack and the hypervisor, the database, REST, HTTP, and AMQP. Server-crash faults are injected by killing relevant service processes via systemd.
+ (Graph-based) In [HANSEL: Diagnosing Faults in OpenStack](http://conferences2.sigcomm.org/co-next/2015/img/papers/conext15-final156.pdf]), the auhtors intercept AMQP and REST messages to reconstruct an execution graph. The approach requires network monitoring agents at each node in the OpenStack deployment. One of the challenges is the so-called transaction stitching to reconstruct full transactions to recreate the execution graph.
+ (String-based) In [Toward achieving operational excellence in a cloud](http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=6798708&url=http%3A%2F%2Fieeexplore.ieee.org%2Fxpls%2Fabs_all.jsp%3Farnumber%3D6798708) and [US20150161025 A1: Injecting Faults at Select Execution Points of Distributed Applications ](http://www.google.com/patents/US20150161025), the authors rely on the operating system level information to build message traces by observing system events such as SEND or RECV system calls (or LIBC calls). These events are monitored per thread since with higher granularities (i.e., process-level or system-level), the job of separating events is difficult. Message sequences are converted into string of symbols and strings are comapred using an edit distance function. High distances indicate possible anomalies between executions.
+ [DICE Fault Injection](https://github.com/dice-project/DICE-Fault-Injection-Tool): A tool to generate faults within Virtual Machine. Under development.
+ [Lineage-driven Fault Injection](https://people.eecs.berkeley.edu/~palvaro/molly.pdf) by Peter Alvaro, Joshua Rosen, Joseph M. Hellerstein UC Berkeley, Proceeding SIGMOD '15.
+ [New Functional Testing in etcd](https://coreos.com/blog/new-functional-testing-in-etcd/). CoreOS uses a fault-injection framework to simulate the most common cases of failures that the system etcd may meet in real life.
+ To guarantee HA, [LinkedIn](linkedin.com) simulates data center failures and measure the effects. To improve response time and lower the cost of operations, they have built the [Nurse](https://engineering.linkedin.com/sre/introducing-nurse-auto-remediation-linkedin) system, a workflow engine which enables to define tasks to recover automatically from failures.

+ The book [Resilience and Reliability on AWS](https://www.amazon.com/Resilience-Reliability-AWS-Jurg-Vliet/dp/1449339190) provides  a motivation and a few examples (for beginners) on the importance of reliability. The author shares their experience to achieve resilience and reliability with code examples to monitor Redis or MongoDB. The use of simple techniques to solve the complex problem of reliability of clouds clearly indicates that current solutions are limited and further systmathic approaches are needed.

+ Microsoft proposed the Resilience Modeling and Analysis [(RMA)](http://download.microsoft.com/download/f/a/2/fa2a49ab-13af-44fc-883c-7b8c48d8a042/resilience-by-design-for-cloud-services.pdf) methodology. It is an approach for improving resilience adapted from the industry-standard technique known as Failure Mode and Effects Analysis (FMEA).

+ [Fault Injection at Cloudera](http://blog.cloudera.com/blog/2016/04/quality-assurance-at-cloudera-fault-injection-and-elastic-partitioning/) uses fault-injection tools and elastic-partitioning techniques for the continuous improvement and verification of their Hadoop ecosystem (CDH) via an extensive QA process during the software-development life cycle.
+ [OpenStack Reliability Testing](http://docs.openstack.org/developer/performance-docs/test_plans/reliability/plan.html) describes an abstract methodology for OpenStack cluster high-availability testing and analysis.


### Anomaly Detection

+ (Process-based) In [Experience report: Anomaly detection of cloud application operations using log and cloud metric correlation analysis (2015)](http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=7381796&url=http%3A%2F%2Fieeexplore.ieee.org%2Fxpls%2Fabs_all.jsp%3Farnumber%3D7381796), the authors present an approach to detect anomalies by correlating data & events extracted from logs and metrics generated by Amazon AWS. While the approach is interesting, the level of detail provided by Amazon logging system does not enable to gain an insightful view and prediction of failures.
+ (Path-based) In patent [Diagnosing distributed applications using application logs and request processing paths](https://www.google.com/patents/US20140136692) and [Patent US9069668](https://www.google.com/patents/US9069668), the authors inject faults into the so-called transaction path, detecting a writing action to a log of the distributed application. When a failure occurs, the path is marked as problematic.
+ Generic approaches for reliability such as Fault Tree Analysis (FTA), Root cause analysis (RCA), Failure mode and effects analysis (FMCA), Cause–effect graphs, Ishikawa diagram, Five whys, etc.


### Tracing

Traditional monitoring solutions for cloud platforms and applications, such as [Cloudwatch](https://aws.amazon.com/cloudwatch/) from Amazon AWS, [Ceilometer](https://wiki.openstack.org/wiki/Telemetry) from Openstack, and [Nagios](https://www.nagios.org/), place emphasis on *component-based monitoring*. Existing solutions collect detailed information on system statistics about virtual machines, CPU, disk IO, hosts, RPC, etc.

Component-based monitoring tools provide not information into the relationship between the components of a distributed service. Since debugging a distributed system is a danting task using these tools, cross-component monitoring (tracing) solutions were explored to aliviate exisitng limitation by tracing the path of events and method calls that are generated at runtime.

The study from Sambasivan, Raja R., et al. titled [So, you want to trace your distributed system? Key design insights from years of practical experience](http://www.pdl.cmu.edu/PDL-FTP/SelfStar/CMU-PDL-14-102.pdf) (Vol. 102. Technical Report, CMU-PDL-14, 2014) provides a very good overview of tracing systems developed up to 2014, and include the analysis of X-Trace, Magpie, Dapper, etc. The thesis from Nathan Scott of the Monash University, Australia, titled [Unifying Event Trace and Sampled Performance Data] (http://pcp.io/papers/unifying-thesis.pdf) also give a fairly good overview of these main tracing systems.

+ [X-Trace](http://people.eecs.berkeley.edu/~istoica/papers/2007/xtr-nsdi07.pdf) from [Berkeley](http://www.berkeley.edu/) outputs a set of task graphs according to Lamport’s happens before relation to trace the execution path of a distributed system. It does not rely on physical clocks and uses low level primitives for instrumentation (e.g., xtr::logEvent(string), xtr::logEvent("end"), pushdown(), and pushnext()).
+ [Magpie](http://research.microsoft.com/en-us/projects/magpie/) from [Microsoft](http://www.microsoft.com) infers traces by combining event logs generated by low level black-box instrumentation. It automatically extracting individual requests from a running system and constructs a probabilistic workload model. Magpie relies on experts with deep knowledge about the system to construct a schema of how to correlate events in different components. In contrast to other approach (from Google, Twitter, and Cloudera), it infers causal relations from the events generated by the operating system and application instrumentation.
+ [Dapper](http://research.google.com/pubs/pub36356.html) from [Google](http://www.google.com) focuses on library and middleware modifications and provides a special context to track execution across async callbacks and RPCs.
+ [HTrace](https://github.com/cloudera/htrace) from [Cloudera](www.cloudera.com/) is a tracing framework intended for use with distributed systems written in java. It is similar to Dapper and performs end-to-end tracing to capture detailed paths of causally between events generated by the components which make a distributed system.
+ [Zipkin](http://zipkin.io) from Twitter is also a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures. Zipkin's design is based on the Google Dapper.
+ [Distributed Tracing at Netflix with Salt](https://speakerdeck.com/niteshkant/distributed-tracing-at-netflix) Dependency and tracing from Netflix.
+ [Jaeger](https://pypi.python.org/pypi/jaeger-client/2.1.0) and [Tracing HTTP request latency](https://medium.com/opentracing/tracing-http-request-latency-in-go-with-opentracing-7cc1282a100a#.74u76hglk). The approach from Uber on tracing (similar to Dapper and Zipkin).
+ [Openstracing](https://github.com/opentracing) OpenTracing is an open distributed tracing standard for applications. Since distributed tracing is important for large-scale distributed systems management and complex services architectures, OpenTracing was created in 2016 to address the standardization problems from instrumentation.

Netflix uses Salp

Facebook uses mystery machine
https://www.usenix.org/system/files/conference/osdi14/osdi14-paper-chow.pdf


+ [Methods and Systems of Distributed Tracing](http://www.google.com/patents/US20140215443) and US 20140215443 A1 Application and US 9135145 B2 Grant by Rackspace Us, Inc. (Sept 2015). A system and methods are provided for distributed tracing in a distributed application by observing messages sent and received among components of the distributed application, generating a probabilistic model of a call flow, and constructing a call flow graph based on the probabilistic model for the distributed application.
+ Mike Y. Chen, Anthony Accardi, Emre Kiciman, Jim Lloyd, Dave Patterson, Armando Fox, and Eric Brewer. 2004. [Path-based faliure and evolution management](http://people.eecs.berkeley.edu/~brewer/papers/nsdi2004_chen_paths.pdf). In Proceedings of the 1st conference on Symposium on Networked Systems Design and Implementation - Volume 1 (NSDI'04), Vol. 1. USENIX Association, Berkeley, CA, USA, 23-23.

### Monitoring

+ [Eliot](https://github.com/ClusterHQ/eliot) A Python library for Logging for complex distributed systems
+ [Monitoring without Infrastructure @ Airbnb](https://www.usenix.org/conference/srecon15/program/presentation/serebryany) Airbnb uses logstash, statsd, NewRelic, Datadog, and their own open-sourced configuration-as-code alerting framework for monitoring.
+ [RefStack](https://refstack.openstack.org/#/results/303e7538-136d-4802-a7e9-a85cfe3c9fc1). RefStack provides users in the OpenStack community with a Tempest wrapper, refstack-client, that helps to verify interoperability of their cloud with other OpenStack clouds. It does so by validating any cloud implementation against the OpenStack Tempest API tests

Other tools from the field of APM ([Application Performance Management](https://en.wikipedia.org/wiki/Application_performance_management)), such as [NewRelic](https://newrelic.com) limite their span to monitor the performance of transactions across web application stacks.

### Repair and Recovery
Automation is having an important role in making the management of cloud data centers automated and 'automatic'. The principals underlying Google SRE and DevOps all call for automation. For cloud reliability and resilience, the procedures to repair the IT infrastructure need to be encoded into executable processes. Large-scale distributed monitoring (dapper), stream and events (spark and flink), and time-based databases (prometheus) provide the base to identify important event that when flagged as alarms need to trigger encoded procedures to repair faulty systems. An important question is 'How to encode procedures to repair IT infrastructure automatically?'

## Huawei's Approach

Ensuring the reliability of large-scale, complex distributed cloud platform requires new innovative approaches. While NetFlix’s ChaosMonkey proposed a new tool (and concept) for site reliability engineers, it only enables the analysis of cloud native applications. Since at Huawei we are developing highly reliable cloud platforms (e.g., Openstack), the site reliability engineering team developed a new approach framework, called Butterfly Effect, to automatically inject faults into cloud infrastructures.

+ Efficient execution trace processing using stream processing
+ Dynamic time-based fingerprinting to detect timeouts
+ Position and negative fingerprints for automated diagnosis and localization of user commands
+ Rely as much possible on open source and Python (see [Python frameworks, libraries, software and resources](https://github.com/vinta/awesome-python))

## Research Groups and Initiatives

+ [Reliable Software Systems (RSS) Group](http://www.iste.uni-stuttgart.de/rss.html), Institute for Software Technology (ISTE)
University of Stuttgart, Germany.
+ [Resilient Computing Lab (RCL)](http://rcl.dsi.unifi.it), University of Florence, Italy.
+ [Software and Systems Engineering](https://www.cisuc.uc.pt/groups/show/sse), University of Coimbra, Portugal.
+ [Dependable Cloud Operations](http://ssrg.nicta.com.au/projects/cloud), Software Systems Research/NICTA, Australia.
+ [InIT Cloud Computing Lab (ICCLab)](http://blog.zhaw.ch/icclab/), Zurich, Switzerland.
+ [ICT COST Action IC1304](http://www.cost.eu/COST_Actions/ict/Actions/IC1304). Autonomous Control for a Reliable Internet of Services (ACROSS).
+ [OpenStack Foundation](http://www.openstack.org/foundation/companies/)
+ [IFIP WG10.4 on Dependable Computing and Fault Tolerance](http://www.dependability.org/wg10.4/)
+ [IEEE Reliability Society](http://rs.ieee.org/) and [IEEE Reliability Society at LinkedIn](https://www.linkedin.com/groups/1855391)

### Conferences
+ [IEEE International Conference on Cloud Computing (IEEE CLOUD)](http://www.thecloudcomputing.org/).
+ [IEEE International Conference on Cloud Engineering (IC2E)](http://conferences.computer.org/IC2E/).
+ [International Conference on Cloud Computing and Services Science (CLOSER)](http://closer.scitevents.org).
+ [International Conference on Service-Oriented Computing (ICSOC)](http://icsoc.in)
+ [IEEE International Conference on Utility and Cloud Computing (UCC)](http://cyprusconferences.org/ucc2015/)
+ [Workshop on Resiliency in High Performance Computing (Resilience) in Clusters, Clouds, and Grids](http://www.csm.ornl.gov/srt/conferences/Resilience/2016/)

### Literature
+ [Software Fault Injection](https://www.amazon.com/Software-Fault-Injection-Jeffrey-Voas/dp/0471183814) by Jeffrey M. Voas and Gary McGraw.
+ [Patterns of resilience](http://www.slideshare.net/ufried/patterns-of-resilience) by Uwe Friedrichsen
+ [Site Reliability Engineering: How Google Runs Production Systems](https://books.google.de/books?id=81UrjwEACAAJ&redir_esc=y). Edited by Betsy Beyer, Chris Jones, Jennifer Petoff and Niall Richard Murphy.
+ [How Complex Systems Fail](http://web.mit.edu/2.75/resources/random/How%20Complex%20Systems%20Fail.pdf) by Richard I. Cook, MD Cognitive technologies Laboratory, University of Chicago (2000).
