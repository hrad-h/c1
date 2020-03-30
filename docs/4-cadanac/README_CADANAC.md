# CADANAC - A System and Method for tracking Covid19 and multiple host infections using Google Cloud, Kubernetes and Hyperledger Fabric


**Maintainers:** [hrad-h](https://github.com/hrad-h/)

Cadanac is a SAAS Virus Case Management System including Financial and Location Tracking Capabilities.  It is developed in response to Covid19 and can accomodate dual and multiple infections (for example the Flu and Covid19 on the same host).

## Cadanac Business Archicture Capabilities

### Virus Case Management ability for Hospitals and Health Care Providers  

- Creating and Updating infected Hosts records  

### Host Location Management ability for Location Providers (such as Cell Phone Companies)  

- Creating and Updating geographical positions of infected Hosts  

### Financial Allocation Management ability for Health Care Providers, NGOs and Governments  

#### Assigning Finances to different Health Care Providers for specific purposes  

- specific virues  

- specific remediation plans  

#### Health Care Providers track Expenditures accordingly  

### Overall System Monitoring, Governance and Intelligence/Trend Gathering by Governments  

#### Increases/Decreases in Host infections  

- per specific virus  

- per remediation plan  

#### Location Proximity of Host infections  

#### Remediation plans analysis  

- Efficacy vs Cost  


## Cadanac Data Archicture

### Data Types

#### HostLocation

currently Host = Person, but can be other Hosts as well

- PrimaryKey per Host
- StateTracking on/off
- Latitude
- Longitude

#### HostHealth

currently Host = Person

- PrimaryKey per Host
- VirusType (Covid19, ...)
- Remediation (Isolation, Hospitalization, ...)
- HealthStatus (Healthy, Symptomatic, Positive, Vaccinated, Recovering, Relapse, PiningForTheFjords)

#### HealthFinance

- PrimaryKey per Health Care Centre Department (i.e. the same Hospital can have multiple accounts)
- VirusType (Covid19, ...)
- Remediation (Isolation, Hospitalization, ...)
- BalanceRemaining (running +/- account balance)

### Persistence

Separate Cadanac Hyperledger Fabric Ledgers store the history for each of the Data Types above.

### Temporal data

Dates and Times are implicity stored in Cadanac via Hyperledger Fabric Block Timestamps.

## Cadanac Application Archicture

### Channels

The entire Cadanac System is partitioned into 3 separate Hyperledger Fabric Channels per the 3 Data Types above

- HostLocation
- HostHealth
- HealthFinance

### Organizations

The Cadanac System fosters participation between different Organizations per the following templates:

- HostLocation Providers (such as Cell Phone Companies)
- HostHealth Providers (such as Hospitals and other Treatment Centres)
- HealthFinance Providers (such as NGOs and Goverments)
- HealthFinance Consumers (such as Hospitals and other Treatment Centres)
- Regulators (such as Governments)

#### Inter Organization Collaboration

Cadanac permits the following Collaboration Groups

- Regulators + HostLocation Providers
- Regulators + HostHealth Providers
- Regulators + HostHealth Providers + HealthFinance Providers + HealthFinance Consumers

As you can see Regulators are central.

#### 3rd Party Regulator Collaboration

Each individual Cadanac System provides connection capability via Hyperledger Fabric Peers to other Cadanac Systems.  For example each country's Government can operate a separate Cadanac System and interconnect as required.

### Peers

Each Organization is required to provide at least 1 Peer to the Cadanac System.  Regulators typically provide many.

### Initial Application Deployment

Kubernetes Jobs configure and initialize all Cadanac Application Architecture components including:

- Creating Channels
- Creating Genesis Blocks in each Ledger
- Joining Peers to Channels
- Instantiating ChainCode on Channels


## Cadanac Technology Archicture

Please see
- https://github.com/hrad-h/c1/blob/master/docs/gcp/README_GCP.md
- https://github.com/hrad-h/c1/blob/master/docs/k8s/README_K8S.md
- https://github.com/hrad-h/c1/blob/master/docs/hlf/README_HLF.md

## Summary

The Cadanac Virus Case Management SAAS uses Hyperledger Fabric PAAS, Kubernetes & GCP IAAS to 