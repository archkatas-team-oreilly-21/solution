Table of content: 
- [Problem analysis](#problem-analysis)
	- [Existing system overview](#existing-system-overview)
	- [Requirements interpretation](#requirements-interpretation)
	- [Assumptions and constraints](#assumptions-and-constraints)
- [Solution](#solution)
	- [Solution Approach Summary](#solution-approach-summary)
	- [Utility tree](#utility-tree)
	- [Quality attributes walk-through](#quality-attributes-walk-through)
- [Views and Perspectives](#views-and-perspecties)
	- [System diagram](#system-diagram)
	- [Data flow diagram](#data-flow-diagram)
	- [Sequence diagrams](#sequence-diagrams)
	- [Infrastructure diagrams](#infrastructure-diagrams)

- [Migration plan](#migration-plan)

## Problem analysis

### Existing system overview

The existing system in a nutshell is a ticketing system giving possibility for client to raise issues and matching experts to resolve those issues by multiple parameters (location, expertise, availabilty etc). It has administrators for user and content management as well as managers to monitor and analyze operations via reports.

The system has some custom applications for all parties: 
 - ticket entry system for clients (web and/or mobile app) 
 - ticket entry system for call center staff (web app) 
 - experts app for ticket handling and knowledge base read-write access (mobile app)
 - admin console for user and content management, ticket read only search (web app) 
 - managers app for reports running

### Requirements interpretation

Here is problem statement: 

> *Things have not been good with the Sysops Squad lately. The current trouble ticket system is a large monolithic application that was developed many years
ago. Customers are complaining that consultants are never showing up due to lost tickets, and often times the wrong consultant shows up to fix something
they know nothing about. Customers and call-center staff have been complaining that the system is not always available for web-based or call-based problem
ticket entry. Change is difficult and risky in this large monolith - whenever a change is made, it takes too long and something else usually breaks. Due to
reliability issues, the monolithic system frequently “freezes up” or crashes - they think it’s mostly due a spike in usage and the number of customers using the
system. If something isn’t done soon, Penultimate Electronics will be forced to abandon this very lucrative business line and fire all of the experts (including
you, the architect).*

Giving statement above it is clear that due to growth or seasonal spikes in customer activities company struggles to deliver its core promises and is on the verge of complete shutdown of business operations and exit. 

Major issues identified by quick analysis are following in an descending order of importance:

 - Inability of existing technical infrastructure to accommodate current load and things getting worth during spikes of customer activity, resulting in low customer satisfaction.
 - Failing business processes, e.g. inadequate matchmaking of skills to problems leading to wasted time, resources and business opportunities.
 - It is hard to identify and eliminate system bugs due to lack of overall system transparency and poor ticket lifecycle management.

### Assumptions and constraints

 It is clear that time is critical.
 
 We assume that budget for change is not bounded meaning some reasonable limits.
 

## Solution

### Solution Approach Summary

To tackle this problem we decided to follow further steps: 

   - Identify quality attributes using existing system description and problem statement.
   - Analyze architecture significant requirements (derived from functional, non-functional requirements and constraints) using Utility tree and rate them.
   - After analysis we made decision to redesign existing monolith application into service based system providing desired system views in later chapter.
   - Design migration plan using phased approach starting from implementation of most viable features and extending system capabilities gradually.

### Utility tree
![Utility tree](./diagrams/utility_tree_diagram.svg)

### Quality attributes walk-through

## Views and Perspectives

### System diagram

#### Primary presentation

![System diagram](./diagrams/system.svg)

#### Element catalog

   - Ticket Onboarding UI - web/mobile app where client or call center representative can login and create ticket.
     Chat bot - built-in app for simple solutions proposal based on client answers. Helps save time, resources and satisfy customers.

   - Ticket Status UI - web/mobile app where client or call center representative can login and view ticket/add comments.

   - Front Service - API service in charge of receival user requests, validating, preprocessing (e.g. ensure auth) them and forwarding to underlying services.

   - Auth service - service providing auth layer for all incoming requests.

   - Chat bot service - backend service providing questions, processing answers to find solution. Uses ML algorythms. Here just for reference, to be explained in details here: [ADR 2](doc/adr/0002-chat-bot-service.md).

   - Ticket CRUD service - regular service for create, read, update, delete(soft) operations with tickets.

   - Matching service - service for automatic matching incoming tickets to most suitable experts.

   - Experts DB - here just for reference - see other diagram and ADR 2.

   - Notification Service - Service for sending alerts and notifications.

   - Expert Mobile App - Used by experts to recieve ticket assignment notifications and further ticket status updates, comments and knowledge base access. 

   - Knowledge Base Service - used for experts lookup of solutions and filling knowledge base. Uses gamification techniques - giving bonus points for articles.

   - Discrepancy service - looks for difference among created, assigned, resolved tickets and if something wrong found sends message to Healing service to try resolve issue.

   - Healing service - set of ruls how to fix ticket reported by Discrepancy service, if not fixed - send alert to manager via Notifiation service.

   - Manager UI - web/mobile app to run reports, receive alerts about problematic tickets, tools for manual ticket fix. All ticket actions audited. 

   - Reporting service - used to retrieve report data and generate reports.

   - Data Preparation service - used to prepare data for data warehouse.


#### Context diagram

#### Variability guide

#### Rationale



### Data flow diagram

### Sequence diagrams

### Infrastructure diagrams

## Migration plan
