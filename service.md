# Service Overview

OwlDB is a database management service that automates deployment, configuration, and administration. Starting from v1.3.0, it newly supports on-premises environments in addition to the existing cloud environments. 

In cloud environments, it supports automated database provisioning based on cloud infrastructure. In on-premises environments, it supports fresh database installation and registration of existing databases based on customer-owned infrastructure.

You can experience a stable operational environment through various features related to database operations.

---

# Operating Environments

## Cloud Environment Support

A cloud environment is a mode in which databases are created and operated based on cloud infrastructure.

OwlDB automates infrastructure creation and database configuration based on IaC (Infrastructure as Code), enabling users to easily provision databases with desired specifications from the console.



## On-Premises Environment Support

An on-premises environment is a mode in which databases are operated based on customer-owned infrastructure such as servers, networks, and storage.

Starting from OwlDB v1.3.0, fresh database installation and registration of existing databases are supported in on-premises environments.

The on-premises environment was designed with the following characteristics in mind.

- **Operation Based on Fixed Infrastructure Resources **: Because it is difficult to scale resources up or down immediately as in cloud environments, database configurations are based on the available hosts and resources within the customer's infrastructure.
- **Air-Gapped Network Environment Support** : OwlDB can be operated even in environments that are isolated from external networks.
- **Installation and Registration Mode Support** : You can install a new database through OwlDB, or register an already-running database as a managed target in OwlDB.



## Service Scope by Operating Environment

The database configuration method, infrastructure preparation scope, and available management features differ depending on the operating environment. The service scope for each environment is as follows.

| Category | Cloud Environment | On-Premises Environment |
| --- | --- | --- |
| Operational Basis | Cloud Infrastructure | Customer-Owned Infrastructure |
| Database Configuration Method | Create a new database from the console | Install a new database or register an existing database |
| Infrastructure Preparation | Follows cloud resource policies | Customer environment must be prepared in advance, including servers, networks, and storage |
| Resource Management | Scaling and management based on cloud resources | Managed within the scope of pre-prepared infrastructure resources |
| Network Environment | Cloud network environment | Customer internal network or air-gapped network environment |
| Key Management Features | Creation, status inquiry, monitoring, backup/recovery, configuration management | Installation/registration, discovery, status inquiry, monitoring, backup/recovery, resource management |
| Pre-Configuration | Automatically configured based on the specifications selected in the console | OwlDB Server and OwlDB Agent installation required |

{% hint style="info" %}
Note

In on-premises environments, features such as database installation, registration, and discovery become available only after the OwlDB Server and OwlDB Agent have been successfully installed and network communication has been verified.

For detailed prerequisites, refer to [**Environment Prerequisites**](#undefined-4).
{% endhint %}

---

## Key Features

The features provided by OwlDB may differ depending on the operating environment.

Based on commonly provided management features, optimized features are provided for both cloud and on-premises environments.

{% tabs %}
{% tab title="공통 기능" %}
The following are key features commonly available in both cloud and on-premises environments.

| Feature | Description |
| --- | --- |
| Database Status Inquiry | You can check the current status of databases and instances. |
| Monitoring | You can check key performance metrics and operational status. |
| Backup/Recovery | • You can create database backups and recover to a desired point in time.<br>• By configuring a desired backup schedule, data loss is minimized and business continuity is ensured. |
| Migration | Pre-validation and migration required for database transitions are supported. |
| Account Management | User-level permissions can be managed through role-based access control (RBAC). |
| Notifications | You can be notified when key events or abnormal conditions occur. |
{% endtab %}
{% tab title="클라우드" %}
These are database creation and operation automation features provided in cloud environments.

| Feature | Description |
| --- | --- |
| Automated Provisioning | Automates cloud infrastructure and database configuration. |
| Resource Scaling and Modification | Specifications can be flexibly changed or scaled. |
| Cloud-Based Backup/Recovery | • Backup/recovery is supported using cloud snapshot functionality.<br>• Retention functionality is provided for AWS only. |
{% endtab %}
{% tab title="온프레미스" %}
These are database installation and registration-based management features provided in on-premises environments.

| Feature | Description |
| --- | --- |
| Database Installation | A new database can be installed on a host within the customer's infrastructure. |
| Register Existing Database | You can register an already-running database as a managed target in OwlDB. |
| Discovery | You can collect configuration information from the customer infrastructure where the Agent is installed and check the current status. |
| On-Premises Backup/Recovery | Backup/recovery is supported using the Tibero RMGR method. |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Note**

The permission scope for each role can be found in ['My Page > Account Role Guide'](function.md).
{% endhint %}



---

## **Database Engine / Version / Topology**

{% tabs %}
{% tab title="Tibero" %}
Tibero is a relational database management system (RDBMS) that delivers powerful processing performance for large-scale data by applying in-memory data processing and high-performance compression technology. 

| Engine | Version | Topology |
| --- | --- | --- |
| Tibero | 7.2.4 | • Single<br>• Single + DR<br>• TAC<br>• TAC + DR |

{% hint style="info" %}
**Note**

Multi-node Cluster cannot be configured as Standby in both Cloud and On-Premise environments.

In addition, On-Premise environments support a maximum of 1 Standby node.
{% endhint %}

{% hint style="info" %}
**Note**

TAC (Tibero Active Cluster) is an Active-Active configuration that provides stable, uninterrupted service based on shared disk.

Disaster Recovery (DR) configures Primary and Standby in separate environments for service continuity, utilizing TSC (Tibero Standby Cluster) which transmits and applies Redo logs in real time.
{% endhint %}
{% endtab %}
{% tab title="Tmax OpenSQL (On-Premise)" %}
Tmax OpenSQL is a platform for building high-performance, high-availability database clusters based on PostgreSQL, an open-source relational database management system (RDBMS). 

| Engine | Version | Topology |
| --- | --- | --- |
| Tmax OpenSQL | 2.0 | - Single<br>- HA |

{% hint style="info" %}
**Note**

Currently, Tmax OpenSQL is supported in On-Premise environments only.
{% endhint %}
{% endtab %}
{% endtabs %}

## **Instance Type**

OwlDB provides the flexibility to select an appropriate resource combination based on your intended use. A variety of instance types are available, allowing you to scale your database to meet target workload requirements. 

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
For Tibero TAC, only instance types of large or higher can be used, and xlarge or higher is recommended.
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

For Tibero Single, an instance type with at least 2 vCPUs and 8 GiB of memory is recommended.
For Tibero TAC, only instance types with 4 or more vCPUs are supported, and 8 or more vCPUs are recommended.
{% endhint %}
{% endtab %}
{% endtabs %}



---

## **Storage/Disk Type**

OwlDB provides a variety of storage options for data storage and recovery. You can select the most appropriate storage based on your needs, including usage, performance, and data resiliency. Storage can be easily scaled to meet dynamic application requirements, and data backup and recovery features are also provided.

{% tabs %}
{% tab title="AWS" %}
### gp3 

An SSD-based volume optimized for high-performance workloads, offering high IOPS and low latency. It is highly durable and cost-effective per capacity. 

| Volume Size (GiB) | Volume IOPS (CNT) |
| --- | --- |
| 100 ~ 65,536 | 3,000 ~ 80,000 |

### gp2

An SSD-based volume suitable for storing or processing large amounts of data, with low cost per capacity. It provides high IOPS, though consistency may be somewhat variable. The IOPS value changes according to the allocated storage size and cannot be configured by the user.

| Volume Size (GiB) | Volume IOPS (CNT) |
| --- | --- |
| 100 ~ 16,384 | 450 ~ 16,000 |

### io2

An SSD-based volume that delivers very high IOPS and consistent performance. It is highly durable but comes at a higher cost per capacity. One drawback is that latency is relatively higher compared to other volume types. 

| Volume Size (GiB) | Volume IOPS (CNT) |
| --- | --- |
| 100 ~ 65,536 | 3,000 ~ 256,000 |

{% hint style="info" %}
**Note**

Only io2 is available for the Tibero TAC topology.
{% endhint %}
{% endtab %}
{% tab title="Azure" %}
### Ultra Disk

The highest-performance storage option for Azure virtual machines (VMs). Suitable for data-intensive workloads such as SAP HANA, top-tier databases, and transaction-heavy workloads.

| Disk Size (GiB) | Disk IOPS (CNT) |
| --- | --- |
| 100 ~ 65,536 | 3,000 ~ 400,000 |

### Premium SSD v2

Premium SSD v2 offers improved performance over the existing Premium SSD and is a cost-effective storage option. This product is suitable for a variety of high-performance workloads such as big data analytics and gaming on virtual machines or containers. 

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

LI (License Included) is an option with the license bundled in, so there is no need to purchase or register a license separately. In addition, the LI license is automatically renewed at 00:00 every day.



---

## **BYOL License Usage Guide**

When using the BYOL (Bring Your Own License) license model,** **you must upload a license file.&nbsp;&nbsp;

{% hint style="warning" %}
**Caution**

Performing license-related tasks manually without going through OwlDB may cause issues. Please be sure to follow the procedures within OwlDB for smooth operation.
{% endhint %}

### License Field Items

| Item | Description | Condition |
| --- | --- | --- |
| CSP | Cloud environment in which the database will operate | Must match the CSP in use |
| Start date | License file start date | Must be before today |
| End date | License file expiration date | Must be after today |
| Edition | Database edition | Cloud Edition |
| Topology | License type | One of single, TAC, or TSC |
| Limit CPU | CPU specification to be used | When creating a DB instance, only specs within the same range as the specified number of CPUs can be selected |
| Signature | License file identifier | Cannot be used as a duplicate within OwlDB |

### License validation items

All of the following conditions must be met to register a license file.

| Condition | Description |
| --- | --- |
| Required number of files and matching specifications | When configuring two or more nodes, license files with identical specifications (CSP, Start Date, End Date, Edition, Limit CPU) equal to the number of nodes in use are required |
| New registration restriction | A license that has already been registered cannot be newly registered again |
| Type suitability by role | A license file of a type appropriate for the node's role (Primary, Read Only, Recovery) configuration must be used |

The detailed rules for 'type suitability by role' are as follows. Depending on the node configuration method, the license Topology that Primary and Standby nodes must use should be verified.

{% tabs %}
{% tab title="Primary 노드가 Single인 경우" %}
| Standby node configuration type | Primary node license type | Read Only Standby node license type | Recovery Standby node license type |
| --- | --- | --- | --- |
| When there is at least one Read Only node | TSC | TSC | Single |
| When there is no Read Only node | Single | - | Single |

{% hint style="info" %}
**Note**
When the Primary node is Single, the license Topology of the Recovery Standby node must always be Single, regardless of whether Read Only nodes are present.
{% endhint %}

The following are examples of license Topology application according to the above policy.

| Node Role Configuration | License Topology (in order) |
| --- | --- |
| 1 Single Primary, 1 Recovery Standby | Single + Single |
| 1 Single Primary, 1 Read Only Standby | TSC + TSC |
| 1 Single Primary, 1 Recovery Standby, 1 Read Only Standby | TSC + Single + TSC |
{% endtab %}
{% tab title="Primary 노드가 TAC인 경우" %}
If the Primary node is TAC, the license Topology of all nodes must be TAC regardless of Standby mode (Recovery, Read Only).

The following are examples of license Topology application based on the above policy.

| Node Role Configuration | License Topology (in order) |
| --- | --- |
| 2 TAC Primary nodes, 1 Recovery Standby node | TAC + TAC + TAC |
| 2 TAC Primary nodes, 1 Read Only Standby node | TAC + TAC + TAC |
| 2 TAC Primary nodes, 1 Recovery Standby node, 1 Read Only Standby node | TAC + TAC + TAC + TAC |
{% endtab %}
{% endtabs %}



---

## **Common UI Elements**

| Element | Description |
| --- | --- |
| ① GNB - Menu | • Hamburger menu: Opens and closes the menu panel<br>• Menu icon: Opens and closes the detailed menu area for the main function |
| ② Detailed Menu Area | • Displays the submenu list for the selected menu icon<br>• Page navigation function |
| ③ Logo | • **Dashboard** Navigate to page |
| ④ DB / Instance Selection | • Select the database and instance to manage and monitor<br>• Available selections may vary by feature (refer to '[Feature-specific usage guide](#IAtHKOuaikB0qe5kmvf4)') |
| ⑤ GNB - Other | • Notification Center<br>• User Guide<br>• User Settings (Language, Theme)<br>• Logout |
| ⑥ Table Settings | • Select and deselect table fields to display on screen<br>• Adjust table field order |
| ⑦ Info | • Version and release information |



---

## Service Update

When a new version of OwlDB is released, you can apply the latest version directly from the console.

- **At the top of the dashboard**a light blue update notification banner will appear.
- Inside the notification banner, click the **Update** button to proceed with the update.
- Service updates do not affect the running database.

{% hint style="info" %}
**Note**

If the notification banner has been dismissed, you can proceed with the service update by clicking the **info icon**at the bottom of the detailed menu area.
{% endhint %}
