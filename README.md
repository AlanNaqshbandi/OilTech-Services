# OilTech-Services
## **OilTech-Services – Secure Azure Industrial OT/IT Architecture**

Secure, production-grade Azure architecture designed for an industrial oil and gas services environment where operational technology (OT) and information technology (IT) integration requires strict network zone separation, asset data protection, identity governance, and centralized operational monitoring.

The architecture demonstrates how industrial workloads can securely operate in Azure using dual-zone network segmentation, private connectivity, identity-based access control, and Microsoft Defender for Cloud protection — deployed entirely through Bicep Infrastructure as Code.

## **Architecture Pattern**

IT-facing operations management portal with a fully private OT data zone using:
- Dual-zone Virtual Network segmentation (IT Zone + OT Zone)
- NSG-enforced boundary between IT and OT subnets
- Private Endpoints for all backend data services
- Managed Identity for passwordless service authentication
- RBAC-controlled access with industrial role separation
- Microsoft Defender for Cloud protection
- Centralized monitoring and alerting
- Full Bicep Infrastructure as Code deployment

## **Architecture Overview**

The environment follows a secure dual-zone industrial architecture:
- Public-facing Azure App Service — Industrial Operations Management Portal (HTTPS enforced)
- Private Azure SQL Database — Asset Registry & Operational Records
- Private Storage Account — Sensor Telemetry Logs & Field Reports
- Private Key Vault — Secrets & Service Credentials
- Dual-zone Virtual Network (IT Zone + OT Zone + Management Zone)
- NSGs enforcing strict traffic rules at the OT/IT boundary
- Private DNS zones for all backend service resolution
- Log Analytics Workspace — centralized telemetry across all services
- Azure Monitor alerts for operational health and security events
- Microsoft Defender for Cloud across all deployed resources
- Full Bicep deployment — all resources defined as code, version-controlled and repeatable

## **Security by Design Principles**
- OT zone isolated from public internet — no direct inbound exposure
- NSG rules enforce OT/IT boundary — only approved traffic flows permitted
- Least privilege RBAC enforced through Entra ID security groups
- Managed Identity eliminates hardcoded credentials across all services
- Private Endpoints for all data services — zero public-facing backend
- Private DNS resolution across all zones — no public DNS leakage
- Microsoft Defender threat detection across all resource groups
- Centralized logging captures cross-zone activity for compliance and audit
- Bicep IaC ensures consistent, repeatable, and version-controlled deployments

## **Phase 0 – Resource Organization**
- Dedicated resource groups per functional layer: Net, App, Data, Sec, Ops
- Consistent tagging model applied across all Bicep modules
- Environment classification: Confidential – Industrial Operational Data
- Bicep parameter files defined for deployment consistency

## **Phase 1 – Identity & RBAC**
- Microsoft Entra ID security groups created for industrial role separation
- Group-based RBAC assignments scoped per resource group
- Three-tier access model: OilTech-Admins / OilTech-Engineers / OilTech-Auditors
- No direct user role assignments — all access group-managed
- RBAC assignments defined as Bicep roleAssignment resources

## **Phase 2 – Network Segmentation & OT/IT Boundary**
- Dual-zone Virtual Network with IT Zone, OT Zone, and Management subnet
- NSGs deployed on all subnets with zone-aware inbound and outbound rules
- OT subnet denies all traffic except approved flows from IT zone
- Private DNS zones provisioned and linked to VNet for all backend services
- All network resources deployed and managed via Bicep modules

## **Phase 3 – Application Layer**
- Azure App Service deployed (Premium tier) — Industrial Operations Management Portal
- System-assigned Managed Identity enabled at deployment
- VNet Integration configured — app communicates through IT zone only
- HTTPS-only enforced — no HTTP permitted
- App Service deployed and configured entirely through Bicep

## **Phase 4 – Secure SQL Deployment**
- Azure SQL Database deployed for asset registry and operational records
- Public network access disabled at deployment via Bicep parameter
- Private Endpoint provisioned in OT Data subnet
- Private DNS integration enabled for internal resolution
- Defender for SQL enabled for threat detection

## **Phase 5 – Secure Storage Deployment**
- Azure Storage Account deployed for sensor telemetry logs and field reports
- Public network access disabled
- Private Endpoint configured in OT Data subnet
- Blob soft delete and versioning enabled for data resilience
- Defender for Storage enabled for anomaly detection

## **Phase 6 – Secrets Management**
- Azure Key Vault deployed using RBAC authorization model
- Public network access disabled — private access only
- Private Endpoint configured in Management subnet
- App Service Managed Identity granted Key Vault Secrets User role
- All application secrets and connection strings stored in Key Vault

## **Phase 7 – Monitoring & Threat Detection**
- Log Analytics Workspace deployed as the central telemetry hub
- Diagnostic settings deployed via Bicep — streaming from all services at provisioning
- Azure Monitor alerts configured for:
    - Operations portal availability and response time
    - SQL performance and connection anomalies
    - Storage access spikes and unauthorized access attempts
    - NSG flow anomalies at the OT/IT boundary
- Microsoft Defender for Cloud enabled across all resource groups

## **Phase 8 – Production Validation**
- Confirmed zero public exposure of all OT zone backend services
- Verified Private Endpoint connectivity and DNS resolution across both zones
- Confirmed NSG rules correctly enforce OT/IT boundary traffic policy
- Validated Managed Identity authentication for Key Vault secret retrieval
- Reviewed Defender for Cloud security recommendations
- Confirmed all monitoring, alerting, and diagnostic pipelines are operational

## **Operational Impact**

Formal security validation checklist executed post-deployment across all phases.

This architecture demonstrates:
- Industrial-grade OT/IT Azure security architecture with dual-zone isolation
- Zero Trust principles enforced at the network, identity, and data layers
- NSG-enforced OT/IT boundary — controlled, auditable inter-zone traffic
- Identity-based service authentication eliminating credential exposure
- Compliance-ready logging and audit trail across IT and OT zones
- Full Bicep Infrastructure as Code — every resource version-controlled and repeatable

## **Deployment Specifications**
| Component          | Configuration                              |
| ------------------ | ------------------------------------------ |
| Region             | Canada Central                             |
| Environment        | Production                                 |
| Architecture Model | Dual-Zone VNet (IT + OT + Management)      |
| Network Model      | Private Endpoints + Private DNS + NSG Zones|
| Identity Model     | Entra ID + Managed Identity                |
| Monitoring         | Log Analytics + Azure Monitor              |
| Security Posture   | Microsoft Defender for Cloud               |
| Access Control     | RBAC (Group-Based, Bicep-Assigned)         |
| Deployment Method  | Bicep (Infrastructure as Code)             |
