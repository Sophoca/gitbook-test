# 릴리즈노트 가이드용

> ### **Release Highlights**
> 
> - Source Database PostgreSQL 신규 지원
> - Target Database PostgreSQL 신규 지원
> - Source Oracle에 대한 안정화

# 신규 기능

### Source Database에 PostgreSQL 추가

PostgreSQL 관련 제약조건은 아래 문서를 참고합니다.

### Target Database에 PostgreSQL 추가

**제약조건**

- PostgreSQL 데이터베이스의 경우, 양방향 동기화를 지원하지 않습니다
- ProSyncManager를 통한 초기적재를 지원하지 않습니다.
- DDL 동기화를 지원하지 않습니다.
- Flashback query를 사용한 정합성 검사를 지원하지 않습니다.

---

# **변경 사항**

## 오류 개선

### 공백 이후 문자열 누락된 동기화 

Oracle과 Tibero의 Character Set이 서로 다를 경우, VARCHAR 타입 칼럼에 문자열 뒤에 공백이 포함된 데이터가 있을 경우 공백 이후의 문자열이 잘려서 동기화되는 문제가 해결되었습니다.

## 기능 개선

### 공백 이후 문자열 누락된 동기화 

Oracle과 Tibero의 Character Set이 서로 다를 경우, VARCHAR 타입 칼럼에 문자열 뒤에 공백이 포함된 데이터가 있을 경우 공백 이후의 문자열이 잘려서 

## 편의성 개선

### Skip 처리 기능 추가

Source Oracle 추출 과정에서, 해석 불가능한 Record가 발견된 경우, 해당 Record를 Skip할 수 있는 기능이 추가되었습니다.

## 삭제 정보

### Deleted Parameter

**Extract Parameters**

| Parameter Name | 비고 |
| --- | --- |
| ORACLE10G_LOG_FILE_BLOCKSIZE | Deleted |
| CLIENT_DRIVER | Deleted |
| LISTENER_PORT | Deleted |

**Apply Parameters**

| Parameter Name | 비고 |
| --- | --- |
| CLIENT_DRIVER | Deleted |
| LISTENER_PORT | Deleted |

**LLOB Parameters**

| Parameter Name | 비고 |
| --- | --- |
| CLIENT_DRIVER | Deleted |
| LISTENER_PORT | Deleted |

## 비 권장 기능(Deprecated)

ProSync 4.5 에서 deprecated 된 기능입니다.

- Deprecated 용어(TOP)가 포함된 메타테이블이 변경되었습니다. **PRS_IMPORTED_ARCHIVE_LOG** 테이블 삭제 **PRS_INSTALL_TOP **테이블명을 **PRS_INSTALL_INSTANCE**로 변경 **TOP_ID** 컬럼명을 **INSTANCE_ID**로 변경

##
