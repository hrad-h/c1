# CADANAC - A System and Method for tracking Covid19 and multiple host infections using Google Cloud, Kubernetes and Hyperledger Fabric


**Maintainers:** [hrad-h](https://github.com/hrad-h/)

Cadanac is a SAAS Virus Case Management System including Financial and Location Tracking Capabilities.  It is developed in response to Covid19 and can accomodate dual and multiple infections (for example the Flu and Covid19 on the same host).


## Cadanac Business Archicture


### Cadanac Actors

- Hospitals
- Other Treatment Centres
- Cell Phone Companies
- NGOs
- Goverments
- WHO

### Use Cases

Below are shown Back End Hyperledger Fabric chaincode invocation commands.

TODO: create a Front End Mobile App and REST JSON API for the Back End.

#### Hospitals & Other Treatment Centres

- create a Covid19 Symptomatic HostHealth record for a new Patient


```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["createPersonHealth", "123-456-7890", "Isolation","Symptomatic","Covid19"]}'
```

- update a Covid19 HostHealth record for a Patient as Positive

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["updateRemediationIDPersonStatus", "123-456-7890", "Isolation","Positive","Covid19"]}'
```

- create an Influenze Symptomatic HostHealth record for the same Patient

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["createPersonHealth", "123-456-7890", "Isolation","Symptomatic","Influenza"]}'
```

- update an Influenze HostHealth record for the same Patient as Positive

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["updateRemediationIDPersonStatus", "123-456-7890", "Hospitalization","Positive","Influenza"]}'
```

- update a Covid19 HostHealth record for an existing Patient with Vaccination remediation treatment

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["updateRemediationIDPersonStatus", "123-456-7890", "Vaccination","Positive","Covid19"]}'
```

- update a Covid19 HostHealth record for an existing Patient as Recovering

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["updateRemediationIDPersonStatus", "123-456-7890", "Isolation","Recovering","Covid19"]}'
```

- update a Covid19 HostHealth record for an existing Patient as Relapse


```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["updateRemediationIDPersonStatus", "123-456-7890", "Hospitalization","Relapse","Covid19"]}'
```

- update an Influenze HostHealth record for the same Patient as SymptomFree

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonhealth -n personhealth -c '{"Args":["updateRemediationIDPersonStatus", "123-456-7890", "","SymptomFree","Influenza"]}'
```

- retrieve all HostHealth records for a Patient with specific Virus

```sh
peer chaincode invoke -C channelpersonhealth  -n personhealth -c '{"Args":["getHistoryForPersonHealth","123-456-7890","Covid19"]}'
```

- retrieve latest HostHealth record for a Patient with specific Virus

```sh
peer chaincode query -C channelpersonhealth  -n personhealth -c '{"Args":["readPersonHealth","123-456-7890","Covid19"]}'
```

- consume money from a Covid19 HealthFinance record for a specific account

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "", "10000","Covid19"]}'
```

- consume money from a specific Remediation for Covid19 HealthFinance record for a specific account 

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "Hospitalization", "500",""]}'
```

- consume money from an Influenza HealthFinance record for a specific account

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "", "2000","Influenza"]}'
```

- consume money from a HealthFinance record for a specific account for any Remediation any Virus

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "", "5000",""]}'
```

- retrieve all HealthFinance records for a specific account

```sh
peer chaincode invoke -C channelhealthfinance  -n healthfinance -c '{"Args":["getHistoryForHealthFinance","Sunnybrook-Emerg"]}'
```

- retrieve latest balance for a HealthFinance record for a specific account

```sh
peer chaincode query -C channelhealthfinance  -n healthfinance -c '{"Args":["readHealthFinance","Sunnybrook-Emerg"]}'
```

#### Goverments

- create a new HostLocation request for a new Patient

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonlocation -n personlocation -c '{"Args":["createPersonLocation", "123-456-7890"]}'
```

- retrieve all HostLocation records for a Patient

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonlocation -n personlocation -c '{"Args":["getHistoryForPersonLocation", "123-456-7890"]}'
```

- retrieve latest HostLocation record for a Patient

```sh
peer chaincode query -o blockchain-orderer:31010 -C channelpersonlocation -n personlocation -c '{"Args":["readPersonLocation", "123-456-7890"]}'
```

- retrieve all HostHealth records for a Patient with specific Virus

see above

- retrieve latest HostHealth record for a Patient with specific Virus

see above


#### Cell Phone Companies

- get all new HostLocation requests (for all new Patients)

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonlocation -n personlocation -c '{"Args":["getNew"]}'
```

- update HostLocation request with present Latitude & Longitude for a new Patient (and remove new request)

First Patient is in Toronto.

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonlocation -n personlocation -c '{"Args":["updateLatitudeLongitude", "123-456-7890", "43.6532° N", "79.3832° W"]}'
```

- update HostLocation with present Latitude & Longitude for an existing Patient

Another Patient is also in Toronto.

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonlocation -n personlocation -c '{"Args":["updateLatitudeLongitude", "789-456-1230", "43.6532° N", "79.3832° W"]}'
```

First Patient is now in Mississauga.

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelpersonlocation -n personlocation -c '{"Args":["updateLatitudeLongitude", "123-456-7890", "43.5890° N", "79.6441° W"]}'
```

#### Governments & NGOs

- add money into a Covid19 HealthFinance record for a specific account

Accounts may be per Hospital, per Other Treatment Centre, per Hospital Department, of any granularity be it large or small.

Governments & NGOs may wish to prioritize funds for specific Viruses or Remediation methodologies.

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "", "50000","Covid19"]}'
```

- add money into a specific Remediation for Covid19 HealthFinance record for a specific account 

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "Vaccination", "50000","Covid19"]}'
```

- add money into an Influenze HealthFinance record for a specific account

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "", "80000","Influenza"]}'
```

- add money into a HealthFinance record for a specific account for any Remediation any Virus

```sh
peer chaincode invoke -o blockchain-orderer:31010 -C channelhealthfinance -n healthfinance -c '{"Args":["updateRemediationIDBalanceRemaining", "Sunnybrook-Emerg", "", "60000",""]}'
```

- retrieve all HealthFinance records for a specific account

see above

- retrieve latest HealthFinance record for a specific account

see above


##### TODO

Employ Machine Learning to:
- correlate increases/decreases in HostHealth records with HostLocation records
- predict geographical locations where viruses are likliest to spread to
- assertain relapse frequencies
- match spending to effective/ineffective Remediation
- ...

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
- HealthStatus (SymptomFree, Symptomatic, Positive, Vaccinated, Recovering, Relapse, PiningForTheFjords)

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

Cadanac permits the following Collaboration Groups.  Each group is assigned to a different Channel.

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

Here are some ArchiMate Diagrams.

### Location Provider

![Cadanac_LocationProvider.png](https://github.com/hrad-h/c1/blob/master/docs/gcp/images/Cadanac_LocationProvider.png)

### Regulator

![Cadanac_Regulator.png](https://github.com/hrad-h/c1/blob/master/docs/gcp/images/Cadanac_Regulator.png)

### Cadanac End-To-End

![Cadanac_Technology_Architecture.png](https://github.com/hrad-h/c1/blob/master/docs/gcp/images/Cadanac_Technology_Architecture.png)

Please see
- https://github.com/hrad-h/c1/blob/master/docs/gcp/README_GCP.md
- https://github.com/hrad-h/c1/blob/master/docs/k8s/README_K8S.md
- https://github.com/hrad-h/c1/blob/master/docs/hlf/README_HLF.md

## Summary

The Cadanac Virus Case Management SAAS uses Hyperledger Fabric PAAS, Kubernetes & GCP IAAS to 