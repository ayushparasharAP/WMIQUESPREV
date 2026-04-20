# WMIQUESPREV
**1. What are two major ports used for WinRM communication? (1 Mark)**
Port 5985 (HTTP) → Used when systems are domain-joined and on the same network
Port 5986 (HTTPS) → Used when systems are on different networks
**2. What is COM & DCOM? Command to launch DCOM config tool? Default permissions? (5 Marks)**
COM (Component Object Model):

COM is a language-independent, platform-independent, distributed object-oriented system that allows components to interact using a binary standard interface.

It enables communication locally within the same system
It defines how objects work over a distributed environment
It promotes reuse of software components from different vendors
DCOM (Distributed Component Object Model):

DCOM is an extension of COM that allows communication between components located on remote systems over a network.

Command to launch DCOM Configuration Tool:
dcomcnfg
Default DCOM Permissions:
Remote Access & Remote Launch are:
 Enabled by default for Administrators
 Disabled by default for Standard Users
DCOM Security Aspects:
Access Security
Launch Security
Identity
Connection Policy


**3. What is Event Forwarding in Windows? What are the ways events can be forwarded?** (5 Marks)
Event Forwarding:

Event forwarding allows events from multiple remote computers to be collected and stored on a central collector system.
It was introduced in Windows Server 2008.

Types of Event Forwarding:
1. Collector-Initiated (Pull):
Collector establishes outbound WinRM connection
Pulls events from clients
Requires clients to be reachable
Not scalable
2. Source-Initiated (Push):
Clients send events to collector
Requires policy configuration
More scalable and preferred
Common Requirements:
WinRM must be enabled on both client and collector
Subscription must be created on collector
Uses Windows Event Collector service (Wecsvc)


**4. What are WMI Classes, Instances & Namespaces? Default namespace? Command to repair repository? (5 Marks)**
WMI Classes:

Templates that define properties and methods
Example: Win32_OperatingSystem

WMI Instances:

Actual objects created from classes that represent real system resources
Instances are real-time representations of those resources

WMI Namespace:

A container that organizes WMI classes and instances in a hierarchical structure
Example: Root\CIMV2

Default Namespace:
Root\CIMV2
Commands:
Verify repository: winmgmt /verifyrepository
Repair repository: winmgmt /salvagerepository
**5. What are 4 basic components in WMI architecture? Explain WMI architecture. Service name & startup type. (10 Marks)**
1. WMI Consumers
Management applications or scripts that interact with WMI
Perform:
Query
Enumeration
Execute provider methods
2. WMI Infrastructure
a) CIM Object Manager (CIMOM / WMI Core)
Manages CIM objects
Facilitates interaction between clients
Manages repository
Performs authentication and security checks
b) CIM Repository
Language-independent database
Stores:
Namespaces
Classes
Objects
Instances
c) COM
Enables communication between components locally
d) DCOM
Enables communication between components on remote systems
3. WMI Providers
Intermediaries between WMI service and system resources
Run inside Wmiprvse.exe
Each query can run in a separate provider host process
Types:
SNMP Providers
Win32 Providers
Registry Providers
4. WMI Managed Objects
Instances of WMI classes
Represent real system resources like hardware, software, processes
Types:
SNMP objects
Win32 objects
Registry objects
Working of WMI Architecture:
Consumer sends query
CIMOM processes request
Contacts WMI provider
Provider fetches data
Data returned to consumer
Important Note:
WMI service (Winmgmt) starts when a management application or script makes a request
Service Name:
Winmgmt
Startup Type:
Automatic
**6. Command to launch WMI Management Console (1 Mark)**
wmimgmt.msc
**7. Command to get WinRM listener configuration (1 Mark)**
winrm enumerate winrm/config/listener
**8. What is Event Viewer? Types of events? Command to launch? (4 Marks)**
Event Viewer:

A Windows tool used to view, monitor, and troubleshoot system and application logs.
Event logs are stored in the system for analysis.

Types of Events:
Critical
Error
Warning
Information
Verbose
Command:
eventvwr
**9. What is Task Scheduler? Service name? Types of sessions? (3 Marks)**
Task Scheduler:

A Windows utility used to automate tasks based on time or event conditions.

Service Name:
Schedule
Types of Sessions:
Interactive Session → Requires user login
Non-Interactive Session → Runs in background without user login
**10. Command to launch WMI Tester Tool (1 Mark)**
wbemtest
**11. What is WinRM? What is Wmiprvse? (2 Marks)**
WinRM (Windows Remote Management):

WinRM is Microsoft’s implementation of the WS-Management protocol used for remote management of systems.

Wmiprvse.exe:

WMI Provider Host that executes provider operations and handles WMI queries

**12. What is MMC? What is its purpose? (2 Marks)**
MMC (Microsoft Management Console):

MMC is a Windows utility that provides a unified interface for administrators to manage system components.

Purpose:
Hosts administrative tools called snap-ins
Used to manage:
Event Viewer
Disk Management
Group Policy
Users and Groups
Can manage local and remote systems






---

## **1. What is WMI? Explain its purpose.**

WMI (Windows Management Instrumentation) is a set of extensions to the Windows driver model that provides an operating system interface through which instrumented components can provide information and notifications.

It is Microsoft’s implementation of **WBEM (Web-Based Enterprise Management)** and **CIM (Common Information Model)** standards from DMTF.

**Purpose:**
The purpose of WMI is to define a set of environment-independent specifications that allow management information to be shared between management applications. It enables monitoring, configuration, and management of system resources.

---

## **2. What is WQL? Give examples.**

WQL (WMI Query Language) is a query language used to retrieve and manage information from WMI.

It is specifically designed to query operating system, applications, and system components.

**Examples:**

* `select * from Win32_OperatingSystem`
* `select * from Win32_BIOS`

---

## **3. What are WMI Providers? Explain with examples.**

WMI Providers act as intermediaries between WMI service (**Winmgmt**) and system resources.

* They provide data requested by WMI consumers
* They run inside **Wmiprvse.exe (WMI Provider Host)**
* Each query may run in a separate provider host process

**Types of Providers:**

* SNMP Providers
* Win32 Providers
* Registry Providers

---

## **4. What is CIM Repository?**

CIM Repository (WMI Repository) is a **language-independent database** that stores information related to WMI.

It contains:

* Namespaces
* Classes
* Objects
* Instances

All data is stored in **static form** and is managed by the WMI core (CIMOM).

---

## **5. What is Namespace in WMI? Give examples.**

Namespace is a container that defines the scope for a set of WMI classes and instances.

* It provides hierarchical organization of classes
* Helps manage different environments

**Examples:**

* `Root\Default`
* `Root\CIMV2`

---

## **6. What is WMI Service? Mention service name and dependency.**

WMI service provides management functionality and enables interaction between system components and management applications.

* **Service Name:** Winmgmt
* **Dependency:** RPC (Remote Procedure Call)

The WMI service starts when a management application or script makes a request and may shut down or go into low memory mode when not in use.

---

## **7. What is WMI Arbitrator?**

WMI Arbitrator is a component of the WMI service (**Winmgmt**) that manages scheduling and execution of tasks received from WMI client processes.

* Tracks queries and client requests
* Maintains information like process ID, computer name, query text, and activity time
* Event ID **5858** is generated for cancellation of idle tasks
* Default idle timeout is **20 minutes**

---

## **8. What is WinRM? How does it work?**

WinRM (Windows Remote Management) is a service that allows remote management of systems locally and remotely.

It is Microsoft’s implementation of the **WS-Management protocol**.

**Working:**

* Uses WS-Man protocol
* Communicates over HTTP (5985) and HTTPS (5986)
* Allows scripts and applications to manage systems
* Can communicate with BMC even when OS is offline

---

## **9. What is WinRM Listener?**

WinRM Listener is a service that listens for incoming management requests.

* Defined by transport (HTTP/HTTPS) and IP address
* Can have multiple listener instances
* Sends and receives WS-Management messages

---

## **10. What are authentication methods in WinRM?**

WinRM supports several authentication methods:

* **Kerberos** → Default for domain environment
* **Negotiate** → Default for non-domain
* **Basic** → Disabled by default

These methods ensure secure communication between systems.

---

## **11. What is WS-Management Protocol?**

WS-Management is a **SOAP-based, firewall-friendly protocol** used to exchange management information between systems.

It is used by WinRM and is based on:

* SOAP over HTTP
* WS-Addressing
* WS-Transfer
* WS-Enumeration
* WS-Eventing

---

## **12. What are WinRM commands used for configuration?**

* `winrm quickconfig` → Configure WinRM with default settings
* `winrm get winrm/config` → Check configuration
* `winrm enumerate winrm/config/listener` → View listeners

---

## **13. What is Event Tracing (ETW)?**

Event Tracing for Windows (ETW) is a system used to trace and log events in Windows.

* Integrated into Windows
* Used for monitoring and diagnostics
* Supports event notification, query language, and security

---

## **14. What is Wevtutil?**

Wevtutil is a command-line tool used to manage and configure event logs.

* Enables WMI event tracing
* Used to locate WMI events

---

## **15. What is Windows Event Collector Service?**

Windows Event Collector service (**Wecsvc**) is used to collect and manage events from remote systems.

* Works with event forwarding
* Uses WS-Management protocol
* Managed using **wecutil.exe**

---

## **16. Explain WMI Architecture in brief.**

WMI architecture consists of:

* **Consumers** → Request data
* **CIMOM (WMI Core)** → Processes queries and manages repository
* **Providers** → Fetch system data
* **Repository** → Stores WMI data

**Flow:**
Consumer → CIMOM → Provider → System → Response

---

## **17. What is CIM? Explain its levels.**

CIM (Common Information Model) is an object-oriented data model used to represent system components.

**Levels of CIM:**

1. Core → Common for all management
2. Common → Specific areas
3. Extended → Technology-specific

---

## **18. Difference between COM and DCOM**

* **COM** → Works locally and enables interaction between components
* **DCOM** → Works remotely and allows communication over network

Both follow object-oriented architecture and binary standards.

---

## **19. What is WBEMTest?**

WBEMTest is a WMI tool used to test and check WMI instances and queries.

---

## **20. What is MMC? Explain snap-ins.**

MMC (Microsoft Management Console) provides a unified interface to manage system components.

* Hosts administrative tools called **snap-ins**
* Snap-ins include:

  * Event Viewer
  * Disk Management
  * Group Policy
  * Local Users and Groups

---

## **21. What is Task Scheduler? What are triggers?**

Task Scheduler is used to automate tasks based on specific conditions.

* Runs tasks automatically
* Can be configured using GUI or command line

**Types of triggers:**

* Time-based
* Event-based

---

## **22. Important WMI Commands**

* `wmimgmt.msc` → WMI console
* `wbemtest` → WMI tester
* `winmgmt /verifyrepository`
* `winmgmt /salvagerepository`

---

## **23. Important WinRM Commands**

* `winrm quickconfig`
* `winrm get winrm/config`
* `winrm enumerate winrm/config/listener`

---


