# Popug

## Event storming
![Event storming](Event_storming.jpg)

## Requirements

### Auth Domain
| Actor | Command | Data | Event |
| --- | --- | --- | --- |
| User | Login to any app | Account public ID | Account.Logined |
| User | Create account | User info | Account.Created |

### Task Tracker Domain
| Actor | Command | Data | Event |
| --- | --- | --- | --- |
| Account (any) | Create Task | Task | Tasks.Created |
| Account (admin, manager), Tasks.Reassigned | Assign Task to random developer | Task + Account public ID | Tasks.Assigned |
| Account (developer) | Complete task | Task + Account public ID | Tasks.Completed |
| Account (admin, manager) | Reassign all the tasks | Tasks list | Tasks.Reassigned |
| Account.Logined (developer) | Show assigned tasks | Tasks list | ??? |

### Accounting Domain
| Actor | Command | Data | Event |
| --- | --- | --- | --- |
| Account.Logined (developer) | Show management balance | Balance  | - |
| Tasks.Assigned | Charge money | Task data + price | Balance.Charged |
| Tasks.Completed | Repaid money | Task data + price | Balance.Repaid |
| Day.Finished (job) | Count developer money | Balance + Account public ID | Balance.Totaled |
| Balance.Totaled | Send day balance to developer mail | Balance + Account public ID | - |
| Day.Started(job) | Clear day balance | Balance + Account public ID | Balance.Cleared |

### Audit domain
| Actor | Command | Data | Event |
| --- | --- | --- | --- |
| Balance.Totaled, Balance.Cleared | Update audit log | Balance + Account public ID | - |
| Account.Logined (Admin) | Show the most expensive completed task per day | Task | - |
| Account.Logined (Admin) | Show amount of developers with negative balance per day | Digit | - |

## Data model and domains
![Domain Data Model](Popug_data_model.jpg)

## Services scheme
![Services scheme](Services_scheme.jpg)

## CUD Events
| Event Name | Producer | Consumer |
| --- | --- | --- |
| AccountLogined | Auth | TaskTracker, Account, Audit |
| AccountCreated | Auth | TaskTracker, Account, Audit |
| AccountRoleChanged | Auth | TaskTracker, Account, Audit |
| TaskCreated | TaskTracker | Account, Audit |
| TaskAssigned | TaskTracker | Account, Audit |
| TaskCompleted | TaskTracker | Account, Audit |
| BalanceCharged | Account | Audit |
| BalanceRepaid | Account | Audit |
| BalanceTotaled | Account | Audit |
| BalanceCleared | Account | Audit |
