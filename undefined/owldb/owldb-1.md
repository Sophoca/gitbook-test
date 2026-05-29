# Installation Guide / OwlDB Server Preparation and Installation / OwlDB Installation

## 0. Preparing Deployment Files

Extract the CP deployment files to the desired path on the OwlDB server.

```bash
tar -zxvf owldb-cp-installer-%Y%m%d-%H.tar.gz
```

The directory structure after extraction is as follows.

```
owldb-cp-installer-%Y%m%d-%H.tar.gz
└── owldb-cp-installer
    ├── docker-compose.yaml.template  # Docker Compose 설정 파일 템플릿
    ├── owldb-be
    │   ├── owldb_be.tar        # Backend Docker 이미지
    │   └── owldb_h2.tar        # H2 Docker 이미지
    ├── owldb-fe                
    │   └── owldb_fe.tar        # Frontend Docker 이미지
    ├── owldb.env               # OwlDB env 파일
    ├── owldb_install.sh        # OwlDB 설정 스크립트
    └── validate_infra.sh       # 인프라 검증 스크립트
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

Before running the script [Prerequisites](undefined/owldb/owldb.md)Please verify that have been completed.
{% endhint %}

The script operates in the following order.

1. Hardware and package pre-validation
2. Docker image load
3. `docker-compose.yml` Creation and container startup
4. Health Check execution

** Execution result example **

```bash
$ sudo bash owldb_install.sh 
[INFO] owldb.env 파일에서 설정을 읽습니다: ./owldb.env
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
[INFO] H2 이미지 로드 중...
Loaded image: owldb_h2:latest
[INFO] BE 이미지 로드 중...
Loaded image: owldb_be:20260303-19
[INFO] FE 이미지 로드 중...
Loaded image: owldb_fe:20260303-19
[INFO] 이미지 로드 및 파일 준비 완료.
[INFO] docker-compose.yaml 치환 완료.
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
[INFO] OwlDB 설치 완료. UI 접속: http://[OwlDB 호스트 IP]:80/owldb/#/auth/login
```

## 3. Verifying the Installation Result

Access the URL below in a browser and confirm that the login screen is displayed.

```
http://[OwlDB 서버 IP]:[UI_PORT]/owldb/#/auth/login
```

{% hint style="info" %}
**Note**

Initial root account information: ID `admin` / Password `admin` [T_42]
If a port change is required
{% endhint %}

---

### 포트 변경이 필요한 경우

`owldb.env` Modify the port value in and re-run the script. When the following prompt is displayed, select **1**[T_46]
UI_PORT

- UI_PORT
- SERVER_PORT

```
$sudo bash owldb_install.sh 
...
⚠️  경고: docker-compose.yaml 파일이 이미 존재합니다.

  1) 기존 docker-compose.yaml을 덮어쓰고 계속 진행
  2) 기존 docker-compose.yaml을 그대로 사용하고 계속 진행
  3) 취소

선택 [1-3]: 
```
