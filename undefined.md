# Release Notes Guide

> ### **Release Highlights**
> 
> - New Support for Source Database PostgreSQL
> - New Support for Target Database PostgreSQL
> - Stabilization for Source Oracle

# New Features

### Adding PostgreSQL as a Source Database

For PostgreSQL-related constraints, refer to the documentation below.

### Adding PostgreSQL as a Target Database

**Constraints**

- Bidirectional synchronization is not supported for PostgreSQL databases.
- Initial load via ProSyncManager is not supported.
- DDL synchronization is not supported.
- Consistency checks using Flashback query are not supported.

---

# **Changes**

## Bug Fixes

### Synchronization with Missing Characters After Whitespace 

Fixed an issue where, when the Character Set of Oracle and Tibero differ and a VARCHAR column contains data with trailing whitespace, characters after the whitespace were truncated during synchronization.

## Improvements

### Synchronization with Missing Characters After Whitespace 

When the Character Set of Oracle and Tibero differ and a VARCHAR column contains data with trailing whitespace, characters after the whitespace were truncated during synchronization. 

## Usability Improvements

### Added Skip Processing Feature

A feature has been added to allow skipping a Record when an uninterpretable Record is encountered during the Source Oracle extraction process.

## Removal Information

### Deleted Parameter

**Extract Parameters**

| Parameter Name | Remarks |
| --- | --- |
| ORACLE10G_LOG_FILE_BLOCKSIZE | Deleted |
| CLIENT_DRIVER | Deleted |
| LISTENER_PORT | Deleted |

**Apply Parameters**

| Parameter Name | Remarks |
| --- | --- |
| CLIENT_DRIVER | Deleted |
| LISTENER_PORT | Deleted |

**LLOB Parameters**

| Parameter Name | Remarks |
| --- | --- |
| CLIENT_DRIVER | Deleted |
| LISTENER_PORT | Deleted |

## Deprecated Features

Features deprecated in ProSync 4.5.

- Meta tables containing the deprecated term (TOP) have been changed. **PRS_IMPORTED_ARCHIVE_LOG** Table deleted **PRS_INSTALL_TOP **Table name changed to **PRS_INSTALL_INSTANCE**Changed to **TOP_ID** Column name changed to **INSTANCE_ID**Changed to

##
