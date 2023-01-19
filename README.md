# EventLogs-LogonLogoff.tkape
KAPE Target for Windows Logon-Logoff events

This KAPE target collects event logs known to contain user account Logon/Logoff events.  Below is a list of event IDs associated with logon/logoff activity from their source logs.

Scroll to the bottom of the page to see reference tables for Logon Type codes and the typical order of Logon/Logoff events in a corporate environment.


## Microsoft-Windows-OfflineFiles%4Operational.evtx
-  Event ID 7: User Logon Detected
-  Event ID 8: User Logoff Detected

## Microsoft-Windows-User Profile Service%4Operational.evtx
- Event ID 1: Received user logon notification on session 1
- Event ID 2: Finished processing user logon notification on session 1
- Event ID 3: Received user logoff notification on session 1
- Event ID 4: Finished processing user logoff notification on session 1
- Event ID 5: Registry file is loaded
- Event ID 67: Logon type, Local profile location, Profile type

## Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx
- Event ID 41: Begin session arbitration (User/Session ID)
- Event ID 42: End session arbitration (User/Session ID)
- Event ID 21: Remote Desktop Services: Session logon succeeded: User: %USERDOMAIN%\%USERNAME%, Session ID: 1, Source Network Address: LOCAL
- Event ID 22: Remote Desktop Services: Shell start notification received: User: %USERDOMAIN%\%USERNAME%, Session ID: 1, Source Network Address: LOCAL
- Event ID 23: Remote Desktop Services: Session logoff succeeded: User: %USERDOMAIN%\%USERNAME%, Session ID: 1
- Event ID 24: Remote Desktop Services: Session has been disconnected: User: %USERDOMAIN%\%USERNAME%, Session ID: 1, Source Network Address: LOCAL

## System.evtx
- Event ID 1074 - The process <PROC_NAME> has initiated the power off of computer %COMPUTERNAME% on behalf of user %USERDOMAIN%\%USERNAME%
- Event ID 7001 - User Logon Notification for Customer Experience Improvement Program
- Event ID 7002 - User Logoff Notification for Customer Experience Improvement Program

## Security.evtx
- Event ID 4624 - An account was successfully logged on
- Event ID 4634 - An account was logged off
- Event ID 4647 - User initiated logoff
- Event ID 4648 - A logon was attempted using explicit credentials (often associated with RunAs)
- Event ID 4672 - Special privileges assigned to new logon (typically administrative privs assigned to account in associated 4624 event)
- Event ID 4776 - The domain controller attempted to validate the credentials for an account (also seen on workstations and member servers for local accounts)
- Event ID 4778 - A session was reconnected to a Window Station (seen with 4779 events during terminal service sessions)
- Event ID 4779 - A session was disconncted from a Window Station (seen with 4778 events during terminal service sessions)
- Event ID 4800 - The workstation was locked (must be enabled in local/group policy)
- Event ID 4801 - The workstation was unlocked (must be enabled in local/group policy)

### Logon Types
| Code | Logon Type | Description |
| --- | --- | --- |
| 0 | (System) | Used only by the System account, for example at system startup. |
| 2 | (Interactive) | A user logged on to this computer. |
| 3 | (Network) | A user or computer logged on to this computer from the network. |
| 4 | (Batch) | Batch logon type is used by batch servers, where processes may be executing on behalf of a user without their direct intervention. |
| 5 | (Service) | A service was started by the Service Control Manager. |
| 7 | (Unlock) | This workstation was unlocked. |
| 8 | (NetworkCleartext) | A user logged on to this computer from the network. The user's password was passed to the authentication package in its unhashed form. The built-in authentication packages all hash credentials before sending them across the network. The credentials do not traverse the network in plaintext (also called cleartext). |
| 9 | (NewCredentials) | A caller cloned its current token and specified new credentials for outbound connections. The new logon session has the same local identity, but uses different credentials for other network connections. |
| 10 | (RemoteInteractive) | A user logged on to this computer remotely using Terminal Services or Remote Desktop. |
| 11 | (CachedInteractive) | A user logged on to this computer with network credentials that were stored locally on the computer. The domain controller was not contacted to verify the credentials. |
| 12 | (CachedRemoteInteractive) | Same as RemoteInteractive. This is used for internal auditing. |
| 13 | (CachedUnlock) | Workstation logon. |


## Typical Order of Logon/Logoff Events in a Corporate Environment
| Event ID | Source Event Log | Description |
| --- | --- | --- |
| 4624 | Security.evtx | Account Logged On |
| 41 | Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx | Begin Session Arbitration |
| 42 | Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx | End Session Arbitration |
| 7001 | System.evtx | User Logon Notification |
| 1 | Microsoft-Windows-User Profile Service%4Operational.evtx | Received User Logon Notification |
| 5 | Microsoft-Windows-User Profile Service%4Operational.evtx | Registry File Loaded |
| 67 | Microsoft-Windows-User Profile Service%4Operational.evtx | Finished Processing Logon |
| 5 | Microsoft-Windows-User Profile Service%4Operational.evtx | Registry File Loaded |
| 2 | Microsoft-Windows-User Profile Service%4Operational.evtx | Finished Processing Logon |
| 21 | Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx | Session Logon Succeeded |
| 7 | Microsoft-Windows-OfflineFiles%4Operational.evtx | User Logon Detected |
| 22 | Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx | Shell Start Notification |
| 4800 | Security.evtx | Workstation Locked |
| 4801 | Security.evtx | Workstation Unlocked |
| 1074 | System.evtx | Process Initiated Power Off/Restart |
| 4647 | Security.evtx | User Initiated Logoff |
| 23 | Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx | Session Logoff Succeeded |
| 3 | Microsoft-Windows-User Profile Service%4Operational.evtx | Received User Logoff Notification |
| 8 | Microsoft-Windows-OfflineFiles%4Operational.evtx | User Logoff Detected |
| 4 | Microsoft-Windows-User Profile Service%4Operational.evtx | Finished Processing User Logoff Notification |
| 7002 | System.evtx | User Logoff Notification |
| 24 | Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx | Session Has Been Disconnected |
