## Security > Security Advisor > Overview

Security Advisor checks the security setting status of NHN Cloud organization and project resources created by customers and provides recommendations. You can use the recommendations for a secure cloud environment.

## Main Features
* Inspects the governance settings of NHN Cloud organizations and applies recommended actions to improve the security of your cloud environment.
* Checks long-term idle accounts in a NHN Cloud project and provides recommendations.
* Checks security groups to confirm the security rules applied to instances.
* Inspects access settings to RDS and blocks unnecessary access.
* Provides periodic auto inspection and sends the result via email.

## Target Resources and Supported Region
### Supported Range for Selected Inspection per Region
|Category|Supported Region|
|---|---|
|Inspection Items by organization|Korea (Pangyo) region, Korea (Pyeongchon) region, Japan (Tokyo) region, and USA (California) region|
|Inspection Items by project|Korea (Pangyo) region, Korea (Pyeongchon) region, and Japan (Tokyo) region|

### Target Resources in Project Inspection Item for Selected Inspection Items
|Category&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Inspection Item|Target Resources|Notes|
|---|---|---|---|
|Project &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |Security Groups|Instance, Security Groups|Database Instance and NKS clusters are excluded|
|Project &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Database Security Groups|Database Instance(MS-SQL Instance, MySQL Instance, PostgreSQL Instance, CUBIRD Instance, MariaDB Instance, Tibero Instance, Redis Instance), Security Groups|
|Project &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |RDS Access Control &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|RDS for MySQL, RDS for MariaDB, RDS for MS-SQL|Inspection is only available in Korea (Pangyo) region because RDS for MariaDB and RDS for MS-SQL are available in the Pangyo region.|

