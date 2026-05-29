# Service Overview

OwlDB is a database management service that automates everything from setup and configuration to administration. Starting from v1.3.0, it adds support for on-premises environments in addition to the existing cloud environment. 

In cloud environments, it supports automated database provisioning based on cloud infrastructure. In on-premises environments, it supports new database installation and registration of existing databases based on customer-owned infrastructure.

A stable operating environment can be experienced through a variety of features related to database operations.

---

# Operating Environments

## Cloud Environment Support

The cloud environment is an approach to creating and operating databases based on cloud infrastructure.

OwlDB automates infrastructure creation and database configuration based on IaC (Infrastructure as Code), enabling users to easily provision a database with desired specifications from the console.



## On-Premises Environment Support

The on-premises environment is an approach to operating databases based on customer-owned infrastructure such as servers, networks, and storage.

Starting from OwlDB v1.3.0, new database installation and registration of existing databases are supported in on-premises environments.

The on-premises environment was designed with the following characteristics in mind.

- **Operation Based on Fixed Infrastructure Resources **: Because it is difficult to instantly scale resources up or down as in cloud environments, database configuration is based on available hosts and resources within the customer's infrastructure.
- **Closed Network Environment Support** : OwlDB can be operated even in environments disconnected from external networks.
- **Installation and Registration Method Support** : You can install a new database through OwlDB, or register an already-running database as an OwlDB-managed target.



## Service Scope by Operating Environment

The database configuration method, infrastructure preparation scope, and available management features differ depending on the operating environment. The service scope for each environment is as follows.

| Category | Cloud Environment | On-Premises Environment |
| --- | --- | --- |
| Operating Basis | Cloud Infrastructure | Customer-Owned Infrastructure |
| Database Configuration Method | Create a new database from the console | Install a new database or register an existing database |
| Infrastructure Preparation | Subject to cloud resource policies | Customer environment must be prepared in advance, including servers, networks, and storage |
| Resource Management | Scale and manage based on cloud resources | Managed within the scope of pre-prepared infrastructure resources |
| Network Environment | Cloud network environment | Customer internal network or closed network environment |
| Key Management Features | Create, status inquiry, monitoring, backup/recovery, configuration management | Install/register, discovery, status inquiry, monitoring, backup/recovery, resource management |
| Pre-Configuration | Automatically configured based on specifications selected in the console | OwlDB Server and OwlDB Agent installation required |

{% hint style="info" %}
Note

In an on-premises environment, features such as database installation, registration, and discovery become available only after the OwlDB Server and OwlDB Agent have been successfully installed and network communication has been confirmed.

For detailed prerequisites, refer to the [**Installation Guide**](undefined/README.md).
{% endhint %}

---

## Key Features

The features provided by OwlDB may differ depending on the operating environment.

Based on commonly provided management features, optimized functionality is provided for both cloud and on-premises environments.

{% tabs %}
{% tab title="Common Features" %}
These are the key features available in common across both cloud and on-premises environments.

| Feature | Description |
| --- | --- |
| Database Status Inquiry | You can check the current status of databases and instances. |
| Monitoring | You can check key performance metrics and operational status. |
| Backup/Recovery | • You can create database backups and recover to a desired point in time.<br>• Set a desired backup schedule to minimize data loss and ensure business continuity. |
| Migration | Pre-validation and migration required for database transition are supported. |
| Account Management | User permissions can be managed through role-based access control (RBAC). |
| Alerts | You can be notified when key events or abnormal states occur. |
{% endtab %}
{% tab title="Cloud" %}
These are the database creation and operations automation features provided in cloud environments.

| Feature | Description |
| --- | --- |
| Automated Provisioning | Automates cloud infrastructure and database configuration. |
| Resource Scaling and Modification | Specifications can be flexibly changed or scaled. |
| Cloud-Based Backup/Recovery | • Backup/recovery is supported using cloud snapshot functionality.<br>• Retention functionality is provided for AWS only. |
{% endtab %}
{% tab title="On-Premises" %}
This is a database installation and registration-based management feature provided in on-premises environments.

| Feature | Description |
| --- | --- |
| Database Installation | You can install a new database on a host within the customer's infrastructure. |
| Registering an Existing Database | You can register an already-operational database as a managed target in OwlDB. |
| Discovery | You can collect configuration information from the customer's infrastructure where the Agent is installed and check the current status. |
| On-Premises Backup/Recovery | Backup/recovery is supported using the Tibero RMGR method. |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Note**

The permission scope for each role can be found in ['My Page > Account Role Guide'](function/README.md).
{% endhint %}



---

## **Database Engine / Version / Topology**

{% tabs %}
{% tab title="Tibero" %}
Tibero is a relational database management system (RDBMS) that applies in-memory data processing and high-performance compression technology, delivering powerful processing performance for large-scale data. 

| Engine | Version | Topology |
| --- | --- | --- |
| Tibero | 7.2.4 | • Single<br>• Single + DR<br>• TAC<br>• TAC + DR |

{% hint style="info" %}
**Note**

Multi-node Cluster cannot be configured as Standby in both Cloud and On-Premise environments.

Additionally, in On-Premise environments, the number of Standby nodes is supported up to a maximum of 1.
{% endhint %}

{% hint style="info" %}
**Note**

TAC (Tibero Active Cluster) is an Active-Active configuration that provides stable, uninterrupted service based on shared disk.

Disaster Recovery (DR) configures Primary and Standby in separate environments for service continuity, utilizing TSC (Tibero Standby Cluster), which transmits and applies Redo logs in real time.
{% endhint %}
{% endtab %}
{% tab title="Tmax OpenSQL (On-Premise)" %}
Tmax OpenSQL is a platform for building high-performance, high-availability database clusters based on PostgreSQL, an open-source relational database management system (RDBMS). 

| Engine | Version | Topology |
| --- | --- | --- |
| Tmax OpenSQL | 2.0 | - Single<br>- HA |

{% hint style="info" %}
**Note**

Currently, Tmax OpenSQL is supported only in On-Premise environments.
{% endhint %}
{% endtab %}
{% endtabs %}

## **Instance Types**

OwlDB provides the flexibility to select an appropriate combination of resources based on your intended use. A variety of instance types are available, allowing you to scale the database to meet your target workload requirements. 

{% tabs %}
{% tab title="AWS" %}
| Instance Type | vCPU (CNT) | Memory (GiB) |
| --- | --- | --- |
| t3.medium | 2 | 4 |
| t3.large | 2 | 8 |
| t3.xlarge | 4 | 16 |
| t3.2xlarge | 8 | 32 |
| m6i.large | 2 | 8 |
| m6i.xlarge | 4 | 16 |
| m6i.2xlarge | 8 | 32 |
| m6i.4xlarge | 16 | 64 |
| m6i.8xlarge | 32 | 128 |
| m6i.12xlarge | 48 | 192 |
| m6i.16xlarge | 64 | 256 |
| m6i.24xlarge | 96 | 384 |
| r6i.large | 2 | 16 |
| r6i.xlarge | 4 | 32 |
| r6i.2xlarge | 8 | 64 |
| r6i.4xlarge | 16 | 128 |
| r6i.8xlarge | 32 | 256 |
| r6i.12xlarge | 48 | 384 |
| r6i.16xlarge | 64 | 512 |
| r6i.24xlarge | 96 | 768 |
| r5.large | 2 | 16 |
| r5.xlarge | 4 | 32 |
| r5.2xlarge | 8 | 64 |
| r5.4xlarge | 16 | 128 |
| r5.8xlarge | 32 | 256 |
| r5.12xlarge | 48 | 384 |
| r5.16xlarge | 64 | 512 |
| r5.24xlarge | 96 | 768 |

{% hint style="info" %}
**Note**

For Tibero Single, instance types of large or higher are recommended.
For Tibero TAC, only instance types of large or higher are supported, and xlarge or higher is recommended.
{% endhint %}
{% endtab %}
{% tab title="Azure" %}
| Instance Type | vCPU (CNT) | Memory (GiB) |
| --- | --- | --- |
| Standard_B2ls_v2 | 2 | 4 |
| Standard_B2s_v2 | 2 | 8 |
| Standard_B4s_v2 | 4 | 16 |
| Standard_B8s_v2 | 8 | 32 |
| Standard_D2s_v5 | 2 | 8 |
| Standard_D4s_v5 | 4 | 16 |
| Standard_D8s_v5 | 8 | 32 |
| Standard_D16s_v5 | 16 | 64 |
| Standard_D32s_v5 | 32 | 128 |
| Standard_D48s_v5 | 48 | 192 |
| Standard_D64s_v5 | 64 | 256 |
| Standard_D96s_v5 | 96 | 384 |
| Standard_E2s_v5 | 2 | 16 |
| Standard_E4s_v5 | 4 | 32 |
| Standard_E8s_v5 | 8 | 64 |
| Standard_E16s_v5 | 16 | 128 |
| Standard_E32s_v5 | 32 | 256 |
| Standard_E48s_v5 | 48 | 384 |
| Standard_E64s_v5 | 64 | 512 |
| Standard_E96s_v5 | 96 | 672 |
| Standard_E2s_v6 | 2 | 16 |
| Standard_E4s_v6 | 4 | 32 |
| Standard_E8s_v6 | 8 | 64 |
| Standard_E16s_v6 | 16 | 128 |
| Standard_E32s_v6 | 32 | 256 |
| Standard_E48s_v6 | 48 | 384 |
| Standard_E64s_v6 | 64 | 512 |
| Standard_E96s_v6 | 96 | 768 |

{% hint style="info" %}
**Note**

For Tibero Single, an instance type with 2 vCPU and 8 GiB or more of memory is recommended.
For Tibero TAC, only instance types with 4 vCPU or more are supported, and 8 vCPU or more is recommended.
{% endhint %}
{% endtab %}
{% endtabs %}



---

## **Storage/Disk Type**

OwlDB provides various storage options for data storage and recovery. You can select the appropriate storage based on your needs, such as usage, performance, and data resilience. Storage can be easily scaled to meet dynamic application requirements, and data backup and recovery features are also provided.

{% tabs %}
{% tab title="AWS" %}
### gp3 

An SSD-based volume optimized for high-performance workloads, providing high IOPS and low latency. It offers excellent durability and low cost per capacity. 

| Volume Size (GiB) | Volume IOPS (CNT) |
| --- | --- |
| 100 ~ 65,536 | 3,000 ~ 80,000 |

### gp2

An SSD-based volume suitable for storing or processing large amounts of data, with low cost per capacity. It provides high IOPS, though consistency may vary somewhat. The IOPS value changes according to the allocated storage size and cannot be configured by the user.

| Volume Size (GiB) | Volume IOPS (CNT) |
| --- | --- |
| 100 ~ 16,384 | 450 ~ 16,000 |

### io2

An SSD-based volume that delivers very high IOPS and consistent performance, with excellent durability and high cost per capacity. A drawback is relatively higher latency. 

| Volume Size (GiB) | Volume IOPS (CNT) |
| --- | --- |
| 100 ~ 65,536 | 3,000 ~ 256,000 |

{% hint style="info" %}
**Note**

The Tibero TAC topology supports io2 only.
{% endhint %}
{% endtab %}
{% tab title="Azure" %}
### Ultra Disk

The highest-performance storage option for Azure virtual machines (VMs). Suitable for data-intensive workloads such as SAP HANA, top-tier databases, and transaction-heavy workloads.

| Disk Size (GiB) | Disk IOPS (CNT) |
| --- | --- |
| 100 ~ 65,536 | 3,000 ~ 400,000 |

### Premium SSD v2

Premium SSD v2 offers improved performance over the original Premium SSD and is a cost-effective storage option. It is suitable for a variety of high-performance workloads on virtual machines or containers, including big data analytics and gaming. 

| Disk Size (GiB) | Disk IOPS (CNT) |
| --- | --- |
| 100 ~ 65,536 | 3,000 ~ 80,000 |

{% hint style="info" %}
**Note**

The volume size for the Tibero TAC topology must be at least 200 GiB.
{% endhint %}
{% endtab %}
{% endtabs %}



---

## **LI License Usage Guide**

LI (License Included) is an option with the license bundled in, so there is no need to purchase or register a license separately. In addition, LI licenses are automatically renewed at 00:00 every day.



---

## **BYOL License Usage Guide**

When using the BYOL (Bring Your Own License) license model,** **you must upload a license file.&nbsp;&nbsp;

{% hint style="warning" %}
**Caution**

Performing license-related tasks manually without going through OwlDB may cause issues. To ensure smooth operation, please strictly follow the procedures within OwlDB.
{% endhint %}

### License Field Items

| Item | Description | Condition |
| --- | --- | --- |
| CSP | Cloud environment in which the database will operate | Must match the CSP in use |
| Start date | License file start date | Must be before today |
| End date | License file expiration date | Must be after today |
| Edition | Database edition | Cloud Edition |
| Topology | License type | One of single, TAC, or TSC |
| Limit CPU | CPU specification to be used | When creating a DB instance, only specs within the same range as the specified CPU count can be selected |
| Signature | License file identifier | Cannot be used more than once within OwlDB |

### License Validation Items

All of the following conditions must be met to register a license file.

| Condition | Description |
| --- | --- |
| Required number of files and matching specifications | When configuring two or more nodes, license files with identical specifications (CSP, Start Date, End Date, Edition, Limit CPU) are required for each node in use |
| New registration restriction | A license that has already been registered cannot be registered again as new |
| Type suitability by role | A license file of a type appropriate for the node's role (Primary, Read Only, Recovery) configuration must be used |

The detailed rules for "Type Suitability by Role" are as follows. Depending on the node configuration method, you must verify the license Topology that the Primary and Standby nodes must use.

{% tabs %}
{% tab title="When the Primary node is Single" %}
| Standby node configuration type | Primary node license type | Read Only Standby Node License Type | Recovery Standby Node License Type |
| --- | --- | --- | --- |
| When there is at least one Read Only node | TSC | TSC | Single |
| When there are no Read Only nodes | Single | - | Single |

{% hint style="info" %}
**Note**
If the Primary node is Single, the Recovery Standby node must always have a license Topology of Single, regardless of whether a Read Only node exists.
{% endhint %}

The following are examples of license Topology application based on the above policy.

| Node Role Configuration | License Topology (in order) |
| --- | --- |
| 1 Single Primary, 1 Recovery Standby | Single + Single |
| 1 Single Primary, 1 Read Only Standby | TSC + TSC |
| 1 Single Primary, 1 Recovery Standby, 1 Read Only Standby | TSC + Single + TSC |
{% endtab %}
{% tab title="When the Primary node is TAC" %}
If the Primary node is TAC, the license Topology of all nodes must be TAC regardless of the Standby mode (Recovery, Read Only).

The following are examples of license Topology application based on the above policy.

| Node Role Configuration | License Topology (in order) |
| --- | --- |
| 2 TAC Primaries, 1 Recovery Standby | TAC + TAC + TAC |
| 2 TAC Primaries, 1 Read Only Standby | TAC + TAC + TAC |
| 2 TAC Primaries, 1 Recovery Standby, 1 Read Only Standby | TAC + TAC + TAC + TAC |
{% endtab %}
{% endtabs %}



---

## **Common UI Elements**

| Element | Description |
| --- | --- |
| ① GNB - Menu | • Hamburger menu: Opens and closes the menu panel<br>• Menu icon: Opens and closes the detailed menu area for the main function |
| ② Detailed Menu Area | • Displays the submenu list for the selected menu icon<br>• Page navigation functionality |
| ③ Logo | • **Dashboard** Navigate to page |
| ④ DB / Instance Selection | • Select the database and instance to manage and monitor<br>• Selectable items may vary by feature (see '[Feature-specific Usage Guide](#IAtHKOuaikB0qe5kmvf4)') |
| ⑤ GNB - Other | • Notification Center<br>• User Guide<br>• User Settings (language, theme)<br>• Logout |
| ⑥ Table Settings | • Select or deselect table fields to display on screen<br>• Adjust table field order |
| ⑦ Info | • Version and release information |



---

## Service Update

When a new version of OwlDB is released, you can apply the latest version directly from the console.

- **At the top of the dashboard**, a light blue update notification banner appears.
- Inside the notification banner, click the **Update** button to proceed with the update.
- Service updates do not affect databases currently in operation.

{% hint style="info" %}
**Note**

If the notification banner has been closed, you can proceed with the service update by clicking the **info icon**at the bottom of the detailed menu area.
{% endhint %}
