# Popug

## Requirements

### Auth Domain
| Actor | Command | Data | Event |
| --- | --- | --- | --- |
| User | Login to any app | Account public ID | Account.Logined |
| User | Create account | User info | Account.Created |

### Auth Domain
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
![Domain Data Model](https://github.com/kotbegimot/Popug/blob/main/Popug%20data%20model.jpg)


