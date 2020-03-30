# CADANAC - A System and Method for tracking Covid19 and multiple host infections using Google Cloud, Kubernetes and Hyperledger Fabric


**Maintainers:** [hrad-h](https://github.com/hrad-h/)

This is a prototype to research and create a simulation of a real-world project using the capabilities of Google Cloud, Kubernetes, Docker and Hyperledger Fabric.  This work attempts to go beyond a simple "HowTo Create Your First ..."

This project has taken tidbits of inspiration from many other authors, all of whom are gratefully acknowledged.  **We are all standing on the shoulders of Giants!**

This project was coded completely on the cloud using Unix commands and vi :-)


Cadanac is a SAAS Virus Case Management System including Financial and Location Tracking Capabilities.  It is developed in response to Covid19 and can accomodate dual and multiple infections (for example the Flu and Covid19 on the same host).


## Cadanac Core Principles

Cadanac should strive for:

- Scalability
- No Data Loss
- Security

## Risks and Mitigations

Some links that challenge the core principles
-	https://www.ibm.com/blogs/blockchain/2019/04/does-hyperledger-fabric-perform-at-scale/
-	https://blog.bybit.com/research-and-analysis/blockchain-performance-and-scalability-hyperledger-fabric/
-	https://thenextweb.com/podium/2019/05/05/ibms-hyperledger-isnt-a-real-blockchain-heres-why/

Mitigation involves applying rigorous system stress tests.


## Cadanac Architecture

[Cadanac Technolgogy Architecture - GCP IAAS](https://github.com/hrad-h/c1/blob/master/docs/1-gcp/README.md)

[Cadanac Technolgogy Architecture - Kubernetes IAAS](https://github.com/hrad-h/c1/blob/master/docs/2-k8s/README.md)

[Cadanac Platform Architecture - Hyperledger Fabric PAAS](https://github.com/hrad-h/c1/blob/master/docs/3-hlf/README.md)

[Cadanac Business, Data, Application Architecture - Hyperledger Fabric PAAS](https://github.com/hrad-h/c1/blob/master/docs/4-cadanac/README.md)


## Future Directions

- with minature IoT tracking devices, Cadanac can be used to track viruses of other species
- Machine Learning capability for trending and forecasting


## SPDX-License-Identifier: Apache-2.0

- This information is provided "as is", with no assurance or guarantee of completeness, accuracy or timeliness of the information, and without warranty of any kind.