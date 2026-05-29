# OwlDB Installation

## 0. Preparing Deployment Files

Extract the CP deployment files to the desired path on the OwlDB server.

```bash
tar -zxvf owldb-cp-installer-%Y%m%d-%H.tar.gz
```

After extraction, the directory structure is as follows.

```
owldb-cp-installer-%Y%m%d-%H.tar.gz
└── owldb-cp-installer
    ├── docker-compose.yaml.template  # Docker Compose configuration file template
    ├── owldb-be
    │   ├── owldb_be.tar        # Backend Docker image
    │   └── owldb_h2.tar        # H2 Docker image
    ├── owldb-fe                
    │   └── owldb_fe.tar        # Frontend Docker image
    ├── owldb.env               # OwlDB env file
    ├── owldb_install.sh        # OwlDB configuration script
    └── validate_infra.sh       # Infrastructure validation script
```

## 1. Configuring owldb.env

Before installation `owldb.env` Enter the following items in the file.

```bash
############################################################
#                     OWLDB ENV FILE                       #
#----------------------------------------------------------#
# This file contains environment variables for OwlDB      #
# Do NOT add spaces around '='                            #
# Lines starting with '#' are comments                    #
############################################################

# ------------------------------
# UI Configuration
# ------------------------------
UI_PORT=

# ------------------------------
# Server Configuration
# ------------------------------
SERVER_PORT=

# ------------------------------
# Database Credentials
# ------------------------------
DB_USERNAME=
DB_PASSWORD=

############################################################
# End of owldb.env
############################################################
```

| Item | Description | Example | Required |
| --- | --- | --- | --- |
| UI_PORT | OwlDB web UI access port | `80` | Required |
| SERVER_PORT | OwlDB server port | `8080` | Required |
| DB_USERNAME | OwlDB meta DB account ID | `db_user` | Required |
| DB_PASSWORD | OwlDB meta DB password | `db_password` | Required |

{% hint style="warning" %}
**Caution**

DB_USERNAME / DB_PASSWORD cannot be changed after the initial configuration.
{% endhint %}

## 2. Running the Installation Script

`owldb.env` After completing the file configuration, run the following command. 

```bash
sudo bash ./owldb_install.sh
```

{% hint style="info" %}
**Note**

Before running the script [Environment Prerequisites](owldb.md)please verify that you have completed.
{% endhint %}

The script operates in the following order.

1. Hardware and package pre-validation
2. Docker image load
3. `docker-compose.yml` Creation and container startup
4. Health Check execution

** Example execution output **

```bash
$ sudo bash owldb_install.sh 
[INFO] Reading configuration from owldb.env file: ./owldb.env
======================================
 Pre-Check Script
 MODE : CP
======================================

== Hardware Check ==
[PASS] CPU : 16 cores (minimum 2 cores)
[PASS] Memory : Total 15 GB, Available 14 GB (CP requires Total ≥ 8GB)

== Package Check ==
[PASS] Package : docker (Docker version 29.1.3, build f52814d)
[PASS] Package : docker-compose (Docker Compose version v2.40.3-desktop.1)

======================================
 Result Summary
======================================
 PASS : 4
 FAIL : 0
 Overall Result : PASS
[INFO] Loading H2 image...
Loaded image: owldb_h2:latest
[INFO] Loading BE image...
Loaded image: owldb_be:20260303-19
[INFO] Loading FE image...
Loaded image: owldb_fe:20260303-19
[INFO] Image load and file preparation complete.
[INFO] docker-compose.yaml substitution complete.
[+] Running 4/4
 ✔ Network owldb-net   Created                                                                                                                                                                         0.0s 
 ✔ Container owldb_h2  Started                                                                                                                                                                         0.5s 
 ✔ Container owldb_be  Started                                                                                                                                                                         0.6s 
 ✔ Container owldb_fe  Started                                                                                                                                                                         0.7s 
[INFO] 🔍 Health Check
[INFO] Health Check Failed (Attempt 1): Retrying in 10 seconds...
[INFO] Health Check Failed (Attempt 2): Retrying in 10 seconds...
[INFO] Health Check Success: OK
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    24    0     0  100    24      0    132 --:--:-- --:--:-- --:--:--   132
Response: 
[INFO] OwlDB installation complete. UI access: http://[OwlDB host IP]:80/owldb/#/auth/login
```

## 3. Verifying Installation Results

Open the URL below in a browser and confirm that the login screen is displayed.

```
http://[OwlDB server IP]:[UI_PORT]/owldb/#/auth/login
```

{% hint style="info" %}
**Note**

Initial root account credentials: ID `admin` / Password `admin` .
{% endhint %}

---

### If a port change is required

`owldb.env` modify the port value and re-run the script. When the following prompt appears, select **option 1**.

- UI_PORT
- SERVER_PORT

```
$sudo bash owldb_install.sh 
...
⚠️  Warning: docker-compose.yaml file already exists.

  1) Overwrite existing docker-compose.yaml and continue
  2) Use existing docker-compose.yaml as-is and continue
  3) Cancel

Select [1-3]: 
```
