---
description: Generate AWS architecture diagrams using PlantUML with official AWS icons
---

# AWS Diagram Generator (PlantUML)

Generate professional AWS architecture diagrams using PlantUML with the official AWS-PlantUML icon library.

**⚠️ REQUIRED:** All diagrams MUST follow the [Clear Flow Design Principles](#clear-flow-design-principles) and [Professional Diagram Design Standards](#professional-diagram-design-standards) sections, including:

**CLEAR FLOW (MANDATORY):**
- Sequential step numbering (1→2→3→4→5→6→7)
- Directional arrows between EVERY consecutive step
- Left-to-right flow within each row
- Curved arrows for row transitions
- Supporting services separated from main flow

**PROFESSIONAL STANDARDS:**
- Vertical dotted separator lines between sections
- Large, prominent curved arrows (strokeWidth=3-4)
- Spacious column layout with proper spacing
- Color-coded sections with consistent styling
- Professional header bar and legend

## Input
$ARGUMENTS

## Instructions

### Step 1: Analyze Architecture Requirements

Parse the user input to understand:
- What type of architecture is requested
- Which AWS services are needed
- The relationships and data flow between components
- Any specific layout preferences

### Step 2: Create PlantUML File

Generate a `.puml` file with this structure:

```plantuml
@startuml {diagram-name}
!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist
!include AWSPuml/AWSCommon.puml

' Include required service icons
!include AWSPuml/Compute/Lambda.puml
!include AWSPuml/Database/DynamoDB.puml
' ... add more as needed

' Layout settings
left to right direction
skinparam linetype ortho

' Define components
Lambda(myLambda, "My Function", "Node.js 18")
DynamoDB(myTable, "My Table", "On-demand")

' Define relationships
myLambda --> myTable : reads/writes

@enduml
```

### Step 3: AWS Icon Include Reference

**Compute:**
```
!include AWSPuml/Compute/EC2.puml
!include AWSPuml/Compute/Lambda.puml
!include AWSPuml/Compute/ECS.puml
!include AWSPuml/Compute/EKS.puml
!include AWSPuml/Compute/Fargate.puml
!include AWSPuml/Compute/Batch.puml
```

**Containers:**
```
!include AWSPuml/Containers/ECS.puml
!include AWSPuml/Containers/EKS.puml
!include AWSPuml/Containers/Fargate.puml
!include AWSPuml/Containers/ECR.puml
```

**Database:**
```
!include AWSPuml/Database/DynamoDB.puml
!include AWSPuml/Database/RDS.puml
!include AWSPuml/Database/Aurora.puml
!include AWSPuml/Database/ElastiCache.puml
!include AWSPuml/Database/Neptune.puml
!include AWSPuml/Database/Redshift.puml
```

**Storage:**
```
!include AWSPuml/Storage/S3.puml
!include AWSPuml/Storage/EFS.puml
!include AWSPuml/Storage/EBS.puml
!include AWSPuml/Storage/FSx.puml
```

**Networking:**
```
!include AWSPuml/NetworkingContentDelivery/VPC.puml
!include AWSPuml/NetworkingContentDelivery/CloudFront.puml
!include AWSPuml/NetworkingContentDelivery/Route53.puml
!include AWSPuml/NetworkingContentDelivery/APIGateway.puml
!include AWSPuml/NetworkingContentDelivery/ELB.puml
!include AWSPuml/NetworkingContentDelivery/ElasticLoadBalancingApplicationLoadBalancer.puml
!include AWSPuml/NetworkingContentDelivery/TransitGateway.puml
!include AWSPuml/NetworkingContentDelivery/DirectConnect.puml
```

**Security & Identity:**
```
!include AWSPuml/SecurityIdentityCompliance/IAM.puml
!include AWSPuml/SecurityIdentityCompliance/IdentityandAccessManagement.puml
!include AWSPuml/SecurityIdentityCompliance/IAMIdentityCenter.puml
!include AWSPuml/SecurityIdentityCompliance/Cognito.puml
!include AWSPuml/SecurityIdentityCompliance/WAF.puml
!include AWSPuml/SecurityIdentityCompliance/Shield.puml
!include AWSPuml/SecurityIdentityCompliance/KMS.puml
!include AWSPuml/SecurityIdentityCompliance/KeyManagementService.puml
!include AWSPuml/SecurityIdentityCompliance/SecretsManager.puml
!include AWSPuml/SecurityIdentityCompliance/GuardDuty.puml
!include AWSPuml/SecurityIdentityCompliance/SecurityHub.puml
!include AWSPuml/SecurityIdentityCompliance/Inspector.puml
!include AWSPuml/SecurityIdentityCompliance/DirectoryService.puml
!include AWSPuml/SecurityIdentityCompliance/ResourceAccessManager.puml
!include AWSPuml/SecurityIdentityCompliance/CertificateManager.puml
!include AWSPuml/SecurityIdentityCompliance/Macie.puml
!include AWSPuml/SecurityIdentityCompliance/Detective.puml
```

**Application Integration:**
```
!include AWSPuml/ApplicationIntegration/SNS.puml
!include AWSPuml/ApplicationIntegration/SQS.puml
!include AWSPuml/ApplicationIntegration/StepFunctions.puml
!include AWSPuml/ApplicationIntegration/EventBridge.puml
!include AWSPuml/ApplicationIntegration/AppSync.puml
```

**Management & Governance:**
```
!include AWSPuml/ManagementGovernance/CloudWatch.puml
!include AWSPuml/ManagementGovernance/CloudTrail.puml
!include AWSPuml/ManagementGovernance/Config.puml
!include AWSPuml/ManagementGovernance/Organizations.puml
!include AWSPuml/ManagementGovernance/ControlTower.puml
!include AWSPuml/ManagementGovernance/SystemsManager.puml
!include AWSPuml/ManagementGovernance/TrustedAdvisor.puml
!include AWSPuml/ManagementGovernance/ServiceCatalog.puml
!include AWSPuml/ManagementGovernance/WellArchitectedTool.puml
!include AWSPuml/ManagementGovernance/OpsWorks.puml
```

**Developer Tools:**
```
!include AWSPuml/DeveloperTools/CodePipeline.puml
!include AWSPuml/DeveloperTools/CodeBuild.puml
!include AWSPuml/DeveloperTools/CodeDeploy.puml
!include AWSPuml/DeveloperTools/CodeCommit.puml
!include AWSPuml/DeveloperTools/Cloud9.puml
!include AWSPuml/DeveloperTools/CloudShell.puml
!include AWSPuml/DeveloperTools/XRay.puml
```

**Cloud Financial Management:**
```
!include AWSPuml/CloudFinancialManagement/CostExplorer.puml
!include AWSPuml/CloudFinancialManagement/Budgets.puml
!include AWSPuml/CloudFinancialManagement/SavingsPlans.puml
```

**Analytics:**
```
!include AWSPuml/Analytics/Kinesis.puml
!include AWSPuml/Analytics/Athena.puml
!include AWSPuml/Analytics/Glue.puml
!include AWSPuml/Analytics/QuickSight.puml
!include AWSPuml/Analytics/EMR.puml
!include AWSPuml/Analytics/LakeFormation.puml
!include AWSPuml/Analytics/DataPipeline.puml
!include AWSPuml/Analytics/OpenSearchService.puml
!include AWSPuml/Analytics/ManagedStreamingforApacheKafka.puml
```

**Machine Learning:**
```
!include AWSPuml/MachineLearning/SageMaker.puml
!include AWSPuml/MachineLearning/Bedrock.puml
!include AWSPuml/MachineLearning/Rekognition.puml
!include AWSPuml/MachineLearning/Comprehend.puml
```

**General:**
```
!include AWSPuml/General/User.puml
!include AWSPuml/General/Users.puml
!include AWSPuml/General/Client.puml
!include AWSPuml/General/Internet.puml
```

### Step 3.5: Component-to-Icon Mapping (ALWAYS USE MOST RELEVANT)

**⚠️ CRITICAL:** When drawing any component, ALWAYS select the icon that best represents the PURPOSE/FUNCTION of that component, not just a generic service icon.

#### AWS Organization & Landing Zone Components

| Component/Account | Most Relevant Icon | Path |
|-------------------|-------------------|------|
| **Audit Account** | Trusted Advisor | `ManagementGovernance/TrustedAdvisor.png` |
| **Log Archive** | S3 (Simple Storage) | `Storage/SimpleStorageService.png` |
| **Identity Management** | IAM Identity Center | `SecurityIdentityCompliance/IAMIdentityCenter.png` |
| **Security/Breakglass** | IAM | `SecurityIdentityCompliance/IdentityandAccessManagement.png` |
| **Network Account** | VPC | `NetworkingContentDelivery/VirtualPrivateCloud.png` |
| **Directory Services** | Directory Service | `SecurityIdentityCompliance/DirectoryService.png` |
| **DNS Account** | Route 53 | `NetworkingContentDelivery/Route53.png` |
| **Shared Services** | Resource Access Manager | `SecurityIdentityCompliance/ResourceAccessManager.png` |
| **Operations (Ops)** | Systems Manager | `ManagementGovernance/SystemsManager.png` |
| **Development Account** | Cloud9 | `DeveloperTools/Cloud9.png` |
| **Pipeline/CI-CD** | CodePipeline | `DeveloperTools/CodePipeline.png` |
| **Reference Components** | Service Catalog | `ManagementGovernance/ServiceCatalog.png` |
| **CCoE (Cloud Center of Excellence)** | Well-Architected Tool | `ManagementGovernance/WellArchitectedTool.png` |
| **Finance Ops / FinOps** | Cost Explorer | `CloudFinancialManagement/CostExplorer.png` |
| **Marketing/Analytics** | QuickSight | `Analytics/QuickSight.png` |
| **Data Lake** | Lake Formation | `Analytics/LakeFormation.png` |
| **Management Account** | Organizations | `ManagementGovernance/Organizations.png` |
| **Control Tower** | Control Tower | `ManagementGovernance/ControlTower.png` |

#### Security & Compliance Components

| Component | Most Relevant Icon | Path |
|-----------|-------------------|------|
| **Security OU** | WAF | `SecurityIdentityCompliance/WAF.png` |
| **Encryption/Keys** | KMS | `SecurityIdentityCompliance/KeyManagementService.png` |
| **Secrets/Credentials** | Secrets Manager | `SecurityIdentityCompliance/SecretsManager.png` |
| **Threat Detection** | GuardDuty | `SecurityIdentityCompliance/GuardDuty.png` |
| **Security Posture** | Security Hub | `SecurityIdentityCompliance/SecurityHub.png` |
| **Vulnerability Scanning** | Inspector | `SecurityIdentityCompliance/Inspector.png` |
| **SSL/TLS Certificates** | Certificate Manager | `SecurityIdentityCompliance/CertificateManager.png` |
| **Data Discovery** | Macie | `SecurityIdentityCompliance/Macie.png` |
| **Investigation** | Detective | `SecurityIdentityCompliance/Detective.png` |
| **Compliance Audit** | Trusted Advisor | `ManagementGovernance/TrustedAdvisor.png` |

#### Infrastructure Components

| Component | Most Relevant Icon | Path |
|-----------|-------------------|------|
| **Infrastructure OU** | Systems Manager | `ManagementGovernance/SystemsManager.png` |
| **VPC/Network** | VPC | `NetworkingContentDelivery/VirtualPrivateCloud.png` |
| **Transit Gateway** | Transit Gateway | `NetworkingContentDelivery/TransitGateway.png` |
| **NAT Gateway** | NAT Gateway | `NetworkingContentDelivery/VPCNATGateway.png` |
| **Internet Gateway** | Internet Gateway | `NetworkingContentDelivery/VPCInternetGateway.png` |
| **Load Balancer (ALB)** | ALB | `NetworkingContentDelivery/ElasticLoadBalancingApplicationLoadBalancer.png` |
| **Load Balancer (NLB)** | NLB | `NetworkingContentDelivery/ElasticLoadBalancingNetworkLoadBalancer.png` |
| **CDN/Distribution** | CloudFront | `NetworkingContentDelivery/CloudFront.png` |

#### Workload/Application Components

| Component | Most Relevant Icon | Path |
|-----------|-------------------|------|
| **Generic Service** | EC2 | `Compute/EC2.png` |
| **Serverless Function** | Lambda | `Compute/Lambda.png` |
| **Container Service** | ECS | `Containers/ElasticContainerService.png` |
| **Kubernetes** | EKS | `Containers/ElasticKubernetesService.png` |
| **Serverless Containers** | Fargate | `Compute/Fargate.png` |
| **Container Registry** | ECR | `Containers/ElasticContainerRegistry.png` |
| **API Endpoint** | API Gateway | `NetworkingContentDelivery/APIGateway.png` |

#### Monitoring & Logging Components

| Component | Most Relevant Icon | Path |
|-----------|-------------------|------|
| **Monitoring** | CloudWatch | `ManagementGovernance/CloudWatch.png` |
| **Audit Logging** | CloudTrail | `ManagementGovernance/CloudTrail.png` |
| **Configuration** | Config | `ManagementGovernance/Config.png` |
| **Tracing** | X-Ray | `DeveloperTools/XRay.png` |

#### Icon Selection Rules

1. **ALWAYS match by PURPOSE** - If the component is for "Audit", use TrustedAdvisor, not a generic icon
2. **Account naming hints** - "network-account" → VPC, "security-breakglass" → IAM
3. **Function over service** - A "Pipeline" account uses CodePipeline, not EC2
4. **Data over compute** - "datalake-prod" → LakeFormation, not S3
5. **Never use placeholder icons** - Always find the most specific match

### Step 4: Component Syntax

**Basic Component:**
```plantuml
ServiceName(alias, "Label", "Description")
```

**Examples:**
```plantuml
Lambda(orderProcessor, "Order Processor", "Node.js 18")
DynamoDB(ordersTable, "Orders", "On-demand capacity")
S3(dataBucket, "Data Lake", "Standard storage")
EC2(webServer, "Web Server", "t3.medium")
```

### Step 5: Grouping with AWS Containers

**VPC Container:**
```plantuml
!include AWSPuml/Groups/VPC.puml

VPCGroup(myVpc, "Production VPC") {
  EC2(server1, "App Server", "")
  RDS(db, "Database", "")
}
```

**Region Container:**
```plantuml
!include AWSPuml/Groups/Region.puml

RegionGroup(usEast1, "us-east-1") {
  Lambda(fn, "Function", "")
}
```

**Available Group Types:**
```
!include AWSPuml/Groups/AWSCloud.puml
!include AWSPuml/Groups/Region.puml
!include AWSPuml/Groups/VPC.puml
!include AWSPuml/Groups/AvailabilityZone.puml
!include AWSPuml/Groups/PublicSubnet.puml
!include AWSPuml/Groups/PrivateSubnet.puml
!include AWSPuml/Groups/SecurityGroup.puml
!include AWSPuml/Groups/AutoScalingGroup.puml
!include AWSPuml/Groups/GenericGroup.puml
```

### Step 6: Relationship Arrows

**Arrow Types:**
```plantuml
' Solid arrow (default)
ComponentA --> ComponentB : label

' Dashed arrow
ComponentA ..> ComponentB : label

' Bidirectional
ComponentA <--> ComponentB : label

' No arrow head
ComponentA -- ComponentB : label
```

**Arrow Directions:**
```plantuml
' Use direction hints for layout
ComponentA -down-> ComponentB
ComponentA -right-> ComponentC
ComponentA -up-> ComponentD
ComponentA -left-> ComponentE
```

### Step 7: Layout Best Practices

**Horizontal Layout:**
```plantuml
left to right direction
```

**Orthogonal Lines (cleaner routing):**
```plantuml
skinparam linetype ortho
```

**Hide empty descriptions:**
```plantuml
hide stereotype
```

**Spacing:**
```plantuml
skinparam nodesep 50
skinparam ranksep 50
```

### Step 8: Generate Diagram

1. Save the file to the plantuml-diagrams folder:
   ```
   /Users/rupeshpanwar/Documents/AI-Projects/ai-architect-diagram/plantuml-diagrams/{name}.puml
   ```

2. Generate the PNG:
   ```bash
   plantuml /Users/rupeshpanwar/Documents/AI-Projects/ai-architect-diagram/plantuml-diagrams/{name}.puml -o ../diagrams/
   ```

3. Verify output at:
   ```
   /Users/rupeshpanwar/Documents/AI-Projects/ai-architect-diagram/diagrams/{name}.png
   ```

---

## Architecture Templates

### Serverless API
```plantuml
@startuml serverless-api
!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist
!include AWSPuml/AWSCommon.puml
!include AWSPuml/General/User.puml
!include AWSPuml/NetworkingContentDelivery/APIGateway.puml
!include AWSPuml/Compute/Lambda.puml
!include AWSPuml/Database/DynamoDB.puml

left to right direction

User(user, "Client", "")
APIGateway(api, "REST API", "")
Lambda(fn, "Handler", "Node.js")
DynamoDB(db, "Data", "")

user --> api
api --> fn
fn --> db
@enduml
```

### 3-Tier Web Application
```plantuml
@startuml three-tier
!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist
!include AWSPuml/AWSCommon.puml
!include AWSPuml/Groups/VPC.puml
!include AWSPuml/Groups/PublicSubnet.puml
!include AWSPuml/Groups/PrivateSubnet.puml
!include AWSPuml/NetworkingContentDelivery/ElasticLoadBalancingApplicationLoadBalancer.puml
!include AWSPuml/Compute/EC2.puml
!include AWSPuml/Database/Aurora.puml

VPCGroup(vpc, "Production VPC") {
  PublicSubnetGroup(public, "Public Subnet") {
    ElasticLoadBalancingApplicationLoadBalancer(alb, "ALB", "")
  }

  PrivateSubnetGroup(app, "App Subnet") {
    EC2(web1, "Web 1", "")
    EC2(web2, "Web 2", "")
  }

  PrivateSubnetGroup(data, "Data Subnet") {
    Aurora(db, "Aurora", "MySQL")
  }
}

alb --> web1
alb --> web2
web1 --> db
web2 --> db
@enduml
```

### Event-Driven Architecture
```plantuml
@startuml event-driven
!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist
!include AWSPuml/AWSCommon.puml
!include AWSPuml/ApplicationIntegration/EventBridge.puml
!include AWSPuml/ApplicationIntegration/SQS.puml
!include AWSPuml/Compute/Lambda.puml
!include AWSPuml/Storage/S3.puml

left to right direction

EventBridge(bus, "Event Bus", "")
SQS(queue, "Processing Queue", "")
Lambda(processor, "Processor", "")
Lambda(notifier, "Notifier", "")
S3(archive, "Archive", "")

bus --> queue
bus --> notifier
queue --> processor
processor --> archive
@enduml
```

---

## Central Logging Architecture Template

**Use Case:** Building centralized logging diagrams for AWS Landing Zones, multi-account environments, and compliance-focused architectures.

### Components Structure

A Central Logging Architecture diagram typically includes these component groups:

#### 1. Agency/Member Accounts (Stacked Visual)
Represents multiple AWS accounts sending logs to central location.

**Components:**
| # | Service | Icon Path | Purpose |
|---|---------|-----------|---------|
| 1 | CloudTrail | `ManagementGovernance/CloudTrail.png` | API audit logging |
| 2 | Config | `ManagementGovernance/Config.png` | Configuration compliance |
| 3 | GuardDuty | `SecurityIdentityCompliance/GuardDuty.png` | Threat detection |
| 4 | Security Hub | `SecurityIdentityCompliance/SecurityHub.png` | Security posture |

**Stacked Container Template (Draw.io):**
```xml
<!-- Agency Accounts - Stacked effect (3 boxes offset) -->
<mxCell id="agency-stack-3" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#607D8B;strokeWidth=2;shadow=1;" parent="1" vertex="1">
  <mxGeometry x="50" y="90" width="380" height="520" as="geometry" />
</mxCell>
<mxCell id="agency-stack-2" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#607D8B;strokeWidth=2;shadow=1;" parent="1" vertex="1">
  <mxGeometry x="60" y="100" width="380" height="520" as="geometry" />
</mxCell>
<mxCell id="agency-stack-1" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#607D8B;strokeWidth=2;shadow=1;" parent="1" vertex="1">
  <mxGeometry x="70" y="110" width="380" height="520" as="geometry" />
</mxCell>
<!-- Stacked headers -->
<mxCell id="agency-header-n" value="Agency n account k" style="text;html=1;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontSize=10;fontColor=#607D8B;fontStyle=2;" parent="1" vertex="1">
  <mxGeometry x="55" y="93" width="120" height="15" as="geometry" />
</mxCell>
```

#### 2. VPC Flow Logs & Custom Logs Section
Represents streaming log sources with subscription filters.

**Components:**
| # | Service | Icon Path | Purpose |
|---|---------|-----------|---------|
| 5 | CloudWatch Logs | `ManagementGovernance/CloudWatchLogs.png` | Log aggregation |
| 6 | Kinesis Data Firehose | `Analytics/KinesisDataFirehose.png` (v18.0) | Log streaming to S3 |

**Flow Pattern:**
```
VPC Flow Logs → CloudWatch Logs → Sub Filter ─┐
                                               ├→ Kinesis Firehose → S3
Custom Logs → CloudWatch Logs → Sub Filter ───┘
```

**Container Template:**
```xml
<!-- VPC Flow Logs Container -->
<mxCell id="vpcflow-container" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFF3E0;strokeColor=#FF9800;strokeWidth=2;" parent="1" vertex="1">
  <mxGeometry x="85" y="455" width="340" height="160" as="geometry" />
</mxCell>
<mxCell id="vpcflow-header" value="VPC Flow Logs" style="text;html=1;strokeColor=none;fillColor=#FF9800;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=1;fontSize=10;fontStyle=1;fontColor=#FFFFFF;spacingLeft=6;" parent="1" vertex="1">
  <mxGeometry x="90" y="458" width="90" height="20" as="geometry" />
</mxCell>
```

**Sub Filter Box Template:**
```xml
<!-- Subscription Filter Box -->
<mxCell id="subfilter" value="Sub&#xa;Filter" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#BF360C;strokeWidth=1;fontSize=9;" parent="1" vertex="1">
  <mxGeometry x="250" y="490" width="40" height="30" as="geometry" />
</mxCell>
```

#### 3. Core Security Account
Central security services aggregation.

**Components:**
- GuardDuty (central/delegated admin)
- Security Hub (central/delegated admin)

**Container Template:**
```xml
<!-- Core Security Account -->
<mxCell id="core-security-container" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFEBEE;strokeColor=#C62828;strokeWidth=2;" parent="1" vertex="1">
  <mxGeometry x="520" y="280" width="200" height="160" as="geometry" />
</mxCell>
<mxCell id="core-security-header" value="Core Security Account" style="text;html=1;strokeColor=none;fillColor=#C62828;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=1;fontSize=11;fontStyle=1;fontColor=#FFFFFF;spacingLeft=8;" parent="1" vertex="1">
  <mxGeometry x="530" y="290" width="160" height="25" as="geometry" />
</mxCell>
```

#### 4. Core Logging Account (Central)
Main logging account with S3 buckets and KMS.

**Components:**
| Service | Icon Path | S3 Bucket Naming |
|---------|-----------|------------------|
| KMS CMK | `SecurityIdentityCompliance/KeyManagementService.png` | N/A (encryption) |
| S3 Bucket | `Storage/SimpleStorageService.png` | tlz-cloudtrail-central-{account-id} |
| S3 Bucket | `Storage/SimpleStorageService.png` | tlz-config-central-{account-id} |
| S3 Bucket | `Storage/SimpleStorageService.png` | tlz-guardduty-central-{account-id} |
| S3 Bucket | `Storage/SimpleStorageService.png` | tlz-security-hub-central-{account-id} |
| S3 Bucket | `Storage/SimpleStorageService.png` | tlz-central-{account-id} |

**Container Template:**
```xml
<!-- Core Logging Account -->
<mxCell id="core-logging-container" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FBE9E7;strokeColor=#BF360C;strokeWidth=3;" parent="1" vertex="1">
  <mxGeometry x="780" y="110" width="500" height="600" as="geometry" />
</mxCell>
<mxCell id="core-logging-header" value="Core Logging Account" style="text;html=1;strokeColor=none;fillColor=#BF360C;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=1;fontSize=14;fontStyle=1;fontColor=#FFFFFF;spacingLeft=10;" parent="1" vertex="1">
  <mxGeometry x="795" y="120" width="200" height="30" as="geometry" />
</mxCell>

<!-- S3 Bucket Row Template -->
<mxCell id="s3-bucket-icon" value="" style="image;aspect=fixed;html=1;points=[];align=center;image=https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/SimpleStorageService.png;" parent="1" vertex="1">
  <mxGeometry x="820" y="180" width="44" height="44" as="geometry" />
</mxCell>
<mxCell id="s3-bucket-label" value="tlz-cloudtrail-central-876385073014" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#E8F5E9;strokeColor=#388E3C;strokeWidth=1;fontSize=9;" parent="1" vertex="1">
  <mxGeometry x="875" y="185" width="200" height="30" as="geometry" />
</mxCell>
```

#### 5. Log Consumer Section
External log processing/consumption.

**Components:**
- SQS (queue for S3 notifications)
- Lambda (consumer function)
- IAM Role (cross-account access)

**Container Template (Dashed border for external):**
```xml
<!-- Log Consumer Section (Dashed border) -->
<mxCell id="consumer-container" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#E8F5E9;strokeColor=#388E3C;strokeWidth=2;strokeDashArray=3 3;" parent="1" vertex="1">
  <mxGeometry x="1330" y="140" width="190" height="560" as="geometry" />
</mxCell>
<mxCell id="consumer-header-n" value="Log Consumer N" style="text;html=1;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontSize=10;fontColor=#388E3C;fontStyle=2;" parent="1" vertex="1">
  <mxGeometry x="1335" y="143" width="100" height="15" as="geometry" />
</mxCell>
<mxCell id="consumer-header-1" value="Log Consumer 1" style="text;html=1;strokeColor=none;fillColor=#388E3C;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=1;fontSize=11;fontStyle=1;fontColor=#FFFFFF;spacingLeft=6;" parent="1" vertex="1">
  <mxGeometry x="1350" y="165" width="110" height="22" as="geometry" />
</mxCell>
```

### Arrow Patterns for Logging Diagrams

**Member Account to Central Logging:**
```xml
<!-- Horizontal arrow from member service to central bucket -->
<mxCell id="arrow-service-central" value="" style="endArrow=classic;html=1;strokeWidth=2;strokeColor=#232F3E;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="335" y="168" as="sourcePoint" />
    <mxPoint x="780" y="168" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

**Multi-path converging arrows (S3 to SQS):**
```xml
<!-- Multiple S3 buckets to single SQS -->
<mxCell id="arrow-s3-sqs-1" value="" style="endArrow=classic;html=1;strokeWidth=2;strokeColor=#388E3C;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="1080" y="200" as="sourcePoint" />
    <mxPoint x="1330" y="350" as="targetPoint" />
    <Array as="points">
      <mxPoint x="1200" y="200" />
      <mxPoint x="1200" y="350" />
    </Array>
  </mxGeometry>
</mxCell>
```

**Dashed arrow (Lambda to Role):**
```xml
<mxCell id="arrow-lambda-role" value="" style="endArrow=classic;html=1;strokeWidth=1;strokeColor=#388E3C;dashed=1;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="1473" y="380" as="sourcePoint" />
    <mxPoint x="1473" y="440" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### Central Logging Color Palette

| Section | Background | Border | Badge |
|---------|------------|--------|-------|
| Agency Accounts | #FFFFFF | #607D8B | N/A |
| VPC Flow Logs | #FFF3E0 | #FF9800 | #BF360C |
| Core Security | #FFEBEE | #C62828 | #C62828 |
| Core Logging | #FBE9E7 | #BF360C | #BF360C |
| Log Consumer | #E8F5E9 | #388E3C (dashed) | #388E3C |
| S3 Buckets | #E8F5E9 | #388E3C | N/A |

### Badge Numbering for Logging Flow

Use numbered badges to indicate the log flow sequence:

| Badge # | Component | Purpose |
|---------|-----------|---------|
| 1 | CloudTrail | API audit logs |
| 2 | Config | Configuration snapshots |
| 3 | GuardDuty | Threat findings |
| 4 | Security Hub | Security findings |
| 5 | CloudWatch Logs | Log aggregation |
| 6 | Kinesis Data Firehose | Log streaming |
| 7 | S3 Central | Central storage |

### Legend Items for Logging Diagrams

```xml
<!-- Legend for Central Logging -->
<mxCell id="leg-agency" value="Agency Accounts" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#607D8B;fontSize=9;strokeWidth=2;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="80" y="785" width="110" height="35" as="geometry" />
</mxCell>
<mxCell id="leg-security-core" value="Core Security" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFEBEE;strokeColor=#C62828;fontSize=9;strokeWidth=2;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="200" y="785" width="100" height="35" as="geometry" />
</mxCell>
<mxCell id="leg-logging-core" value="Core Logging" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FBE9E7;strokeColor=#BF360C;fontSize=9;strokeWidth=2;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="310" y="785" width="100" height="35" as="geometry" />
</mxCell>
<mxCell id="leg-consumer" value="Log Consumer" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#E8F5E9;strokeColor=#388E3C;fontSize=9;strokeWidth=2;fontStyle=1;strokeDashArray=3 3;" parent="1" vertex="1">
  <mxGeometry x="420" y="785" width="100" height="35" as="geometry" />
</mxCell>
<mxCell id="leg-s3" value="S3 Buckets" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#E8F5E9;strokeColor=#388E3C;fontSize=9;strokeWidth=2;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="530" y="785" width="90" height="35" as="geometry" />
</mxCell>
<mxCell id="leg-flowlogs" value="VPC Flow/Custom" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFF3E0;strokeColor=#FF9800;fontSize=9;strokeWidth=2;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="630" y="785" width="120" height="35" as="geometry" />
</mxCell>
```

### Checklist for Central Logging Diagrams

- [ ] Stacked member account containers (3 offset boxes)
- [ ] Numbered badges (1-7) for log flow sequence
- [ ] CloudTrail, Config, GuardDuty, Security Hub in member accounts
- [ ] VPC Flow Logs section with CloudWatch Logs and Sub Filters
- [ ] Kinesis Data Firehose for log streaming (use v18.0 icon)
- [ ] Core Security Account with delegated admin services
- [ ] Core Logging Account with KMS-CMK and S3 buckets
- [ ] S3 bucket naming convention: tlz-{service}-central-{account-id}
- [ ] Log Consumer section with dashed border (external)
- [ ] SQS, Lambda, and IAM Role in consumer section
- [ ] Arrows connecting all log sources to central buckets
- [ ] Multi-path converging arrows from S3 to SQS
- [ ] Color-coded legend at bottom
- [ ] Version and source references in footer

---

## Clear Flow Design Principles

**⚠️ CRITICAL:** All diagrams MUST have a CLEAR, SEQUENTIAL FLOW that customers can follow at a glance. Viewers should immediately understand the order of operations.

### 1. Sequential Step Numbering (MANDATORY)

When depicting processes, implementation steps, or workflows, ALWAYS use numbered badges to show sequence:

```
Flow Pattern: 1 → 2 → 3 → 4 → 5 → 6 → 7
```

**Numbered Badge Template:**
```xml
<!-- Step Badge (Green Circle with Number) -->
<mxCell id="step{n}-badge" value="{n}" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#388E3C;strokeColor=#388E3C;fontColor=#FFFFFF;fontSize=12;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="{x}" y="{y}" width="28" height="28" as="geometry" />
</mxCell>
```

**Badge Colors by Purpose:**
| Purpose | Fill Color | Example |
|---------|------------|---------|
| Implementation Steps | #388E3C (Green) | Steps 1-7 for setup |
| Warning/Critical | #C62828 (Red) | Security checkpoints |
| Information | #1565C0 (Blue) | Optional steps |
| Highlight | #FF9800 (Orange) | Current step |

### 2. Directional Arrows Between Steps (MANDATORY)

Every numbered step MUST have an arrow pointing to the next step to show flow direction:

```
[Step 1] ──▶ [Step 2] ──▶ [Step 3] ──▶ [Step 4]
                                         │
                                         ▼ (row transition)
[Step 7] ◀── [Step 6] ◀── [Step 5] ◀────┘
```

**Horizontal Flow Arrow (Same Row):**
```xml
<!-- Arrow from Step N to Step N+1 -->
<mxCell id="arrow-{n}-{n+1}" value="" style="endArrow=classic;html=1;strokeWidth=2;strokeColor=#388E3C;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="{source-x}" y="{y}" as="sourcePoint" />
    <mxPoint x="{target-x}" y="{y}" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

**Curved Transition Arrow (Row Change):**
```xml
<!-- Arrow from Row 1 to Row 2 (curved down) -->
<mxCell id="arrow-{n}-{n+1}" value="" style="endArrow=classic;html=1;strokeWidth=2;strokeColor=#388E3C;curved=1;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="{source-x}" y="{row1-y}" as="sourcePoint" />
    <mxPoint x="{target-x}" y="{row2-y}" as="targetPoint" />
    <Array as="points">
      <mxPoint x="{mid-x}" y="{mid-y}" />
    </Array>
  </mxGeometry>
</mxCell>
```

### 3. Row-Based Sequential Layout

Arrange steps in rows with natural reading flow:

**Single Row (up to 4-5 steps):**
```
Row 1: [1] → [2] → [3] → [4] → [5]
```

**Multi-Row (6+ steps):**
```
Row 1: [1] → [2] → [3] → [4]
                          │
                          ↓ (curved arrow)
Row 2:       [5] → [6] → [7]
```

**Layout Guidelines:**
- **Row 1 Y-position:** y=175-180 (within Management Account box example)
- **Row 2 Y-position:** y=255-265 (below Row 1)
- **Horizontal spacing:** 135px between step centers
- **Arrow length:** 40px gap between icon and next badge

### 4. Step Component Structure

Each numbered step consists of THREE elements:
1. **Badge** (numbered circle)
2. **Icon** (AWS service icon)
3. **Label** (descriptive text)

**Positioning Pattern:**
```
┌─────────────────────────────────────────────────┐
│  [Badge]  [Icon]   →   [Badge]  [Icon]   →      │
│           Label               Label              │
│                                                  │
│  (x=70)   (x=102)      (x=205)  (x=237)          │
│  Badge    Icon         Badge    Icon             │
│  28x28    44x44        28x28    44x44            │
└─────────────────────────────────────────────────┘

Badge X = Step Start X
Icon X = Badge X + 32 (badge width + 4px gap)
Label X = Icon X - 7 (centered under icon)
Label Y = Icon Y + 45 (below icon)
```

### 5. Complete Sequential Flow Example

**Management Account Setup (7 Steps):**
```xml
<!-- ============================================= -->
<!-- ROW 1: Steps 1→2→3→4 in sequence with arrows -->
<!-- ============================================= -->

<!-- Step 1: Create Account -->
<mxCell id="step1-badge" value="1" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#388E3C;strokeColor=#388E3C;fontColor=#FFFFFF;fontSize=12;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="70" y="178" width="28" height="28" as="geometry" />
</mxCell>
<mxCell id="org-icon-mgmt" value="" style="image;aspect=fixed;html=1;points=[];align=center;image=https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/Organizations.png;" parent="1" vertex="1">
  <mxGeometry x="102" y="173" width="44" height="44" as="geometry" />
</mxCell>
<mxCell id="org-label-mgmt" value="Create&#xa;Account" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=top;whiteSpace=wrap;rounded=0;fontSize=9;fontColor=#232F3E;" vertex="1" parent="1">
  <mxGeometry x="95" y="218" width="60" height="30" as="geometry" />
</mxCell>

<!-- Arrow 1→2 -->
<mxCell id="arrow-1-2" value="" style="endArrow=classic;html=1;strokeWidth=2;strokeColor=#388E3C;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="155" y="195" as="sourcePoint" />
    <mxPoint x="195" y="195" as="targetPoint" />
  </mxGeometry>
</mxCell>

<!-- Step 2: Configure SSO -->
<mxCell id="step2-badge" value="2" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#388E3C;strokeColor=#388E3C;fontColor=#FFFFFF;fontSize=12;fontStyle=1;" parent="1" vertex="1">
  <mxGeometry x="205" y="178" width="28" height="28" as="geometry" />
</mxCell>
<!-- ... icon and label ... -->

<!-- Arrow 2→3 -->
<mxCell id="arrow-2-3" value="" style="endArrow=classic;html=1;strokeWidth=2;strokeColor=#388E3C;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="290" y="195" as="sourcePoint" />
    <mxPoint x="330" y="195" as="targetPoint" />
  </mxGeometry>
</mxCell>

<!-- Continue pattern for remaining steps... -->

<!-- Arrow 4→5 (curved down to row 2) -->
<mxCell id="arrow-4-5" value="" style="endArrow=classic;html=1;strokeWidth=2;strokeColor=#388E3C;curved=1;" parent="1" edge="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="560" y="195" as="sourcePoint" />
    <mxPoint x="600" y="275" as="targetPoint" />
    <Array as="points">
      <mxPoint x="580" y="235" />
    </Array>
  </mxGeometry>
</mxCell>

<!-- ============================================= -->
<!-- ROW 2: Steps 5→6→7 in sequence with arrows   -->
<!-- ============================================= -->
<!-- Continue with same pattern... -->
```

### 6. Supporting Services (Non-Sequential)

Services that are enabled as part of various steps but don't have their own step number should be grouped separately:

```xml
<!-- SUPPORTING SERVICES (No step numbers) -->
<mxCell id="support-label" value="Supporting Services:" style="text;html=1;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontSize=9;fontStyle=2;fontColor=#666666;" vertex="1" parent="1">
  <mxGeometry x="1020" y="165" width="110" height="20" as="geometry" />
</mxCell>
```

**Supporting Services Layout:**
- Position to the right of main sequential flow
- Use smaller icons (32x32px vs 44x44px)
- Gray color scheme (#666666) to differentiate from main flow
- Arrange in a 2x3 or 3x2 grid
- No step numbers or connecting arrows

### 7. Clear Flow Checklist

Before finalizing any diagram, verify:

- [ ] **All process steps are numbered** (1, 2, 3, 4, 5, 6, 7...)
- [ ] **Arrows connect EVERY consecutive step** (1→2, 2→3, 3→4...)
- [ ] **Flow direction is LEFT-TO-RIGHT** within each row
- [ ] **Row transitions use curved arrows** (down from Row 1 to Row 2)
- [ ] **Badge, Icon, Label are properly aligned** for each step
- [ ] **Supporting services are separated** from main flow
- [ ] **Arrow color matches badge color** (typically green #388E3C)
- [ ] **Final arrow points to next section** (down arrow to OUs, etc.)

### 8. Anti-Patterns (AVOID)

**❌ WRONG - Scattered numbering:**
```
[1] [4] [KMS] [CloudTrail] [3] [CUR] [RAM]
[2] [6] [7] [CloudWatch] [Config] [5]
```

**✅ CORRECT - Sequential flow:**
```
[1] → [2] → [3] → [4]
                    ↓
      [5] → [6] → [7] → [OUs]

Supporting: KMS, CloudTrail, CloudWatch, CUR, RAM, Config
```

---

## Professional Diagram Design Standards

**IMPORTANT:** All diagrams MUST follow these design guidelines for professional, publication-ready output.

### 1. Vertical Dotted Separator Lines

Add thin vertical dashed lines between each major column/section to create clear visual boundaries:

```xml
<!-- Vertical Separator Line Template (THIN) -->
<mxCell id="separator-{n}" value="" style="endArrow=none;dashed=1;html=1;dashPattern=4 4;strokeWidth=1;strokeColor=#BDBDBD;" edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="{x}" y="100" as="sourcePoint" />
    <mxPoint x="{x}" y="640" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

**Usage:**
- Place separator lines between each architectural zone (External → Border → Ingress → Application → Data → Security → Compliance → Logging → Outputs)
- Use consistent gray color (#9E9E9E) with dashed pattern
- Extend from header to bottom of main diagram area

### 2. Live Flow Arrows (Source-to-Target Connected)

Arrows MUST connect directly from source to target elements using `source=` and `target=` attributes for proper live connections:

```xml
<!-- Main Flow Arrow (Live Connected, Curved) -->
<mxCell id="flow-{source}-{target}" edge="1" parent="1" source="{source-id}" target="{target-id}" style="edgeStyle=orthogonalEdgeStyle;curved=1;html=1;rounded=1;strokeWidth=3;strokeColor=#FF9900;endArrow=blockThin;endFill=1;endSize=8;shadow=0;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" value="">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Dashed Arrow (for secondary/support flows) -->
<mxCell id="flow-dashed-{n}" edge="1" parent="1" source="{source-id}" target="{target-id}" style="edgeStyle=orthogonalEdgeStyle;curved=1;html=1;rounded=1;strokeWidth=2;strokeColor=#303F9F;endArrow=blockThin;endFill=1;endSize=6;dashed=1;dashPattern=8 4;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" value="">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Large Curved Data Flow Arrow (wraps around at bottom) -->
<mxCell id="flow-data-outputs-main" edge="1" parent="1" style="edgeStyle=orthogonalEdgeStyle;curved=1;html=1;rounded=1;strokeWidth=4;strokeColor=#F57F17;endArrow=blockThin;endFill=1;endSize=10;shadow=1;" value="">
  <mxGeometry relative="1" as="geometry">
    <Array as="points">
      <mxPoint x="{mid-x}" y="{bottom-y}" />
      <mxPoint x="{end-x}" y="{bottom-y}" />
    </Array>
    <mxPoint x="{source-x}" y="{source-y}" as="sourcePoint" />
    <mxPoint x="{target-x}" y="{target-y}" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

**Arrow Style Guidelines:**
- **CRITICAL:** Use `source=` and `target=` attributes to connect arrows to actual elements for live flow
- Use `exitX=1;exitY=0.5` for right-side exit and `entryX=0;entryY=0.5` for left-side entry
- Main flow arrows: strokeWidth=3, curved=1, no shadow for cleaner look
- Dashed arrows: strokeWidth=2 for secondary flows (security, compliance)
- Use `blockThin` arrowheads with endSize=6-10
- Color-code by source section color
- Add waypoints (`<Array as="points">`) only for wrap-around paths

### 3. Spacious Layout

Columns should be narrow with adequate spacing between them:

**Column Width Guidelines:**
- External Sources: 220px
- Border Control: 140px
- Ingress: 120px
- Application: 110px
- Data: 120px
- Security: 120px
- Compliance: 110px
- Central Logging: 200px
- Outputs & Integration: 320px

**Spacing:**
- Minimum 60-80px gap between columns
- Allow room for arrows to flow through separator lines
- Icons should be 64x64px for visibility
- Vertical spacing between icons: 85-95px

### 4. Visual Flow Best Practices

- Data flows LEFT to RIGHT
- Use curved orthogonal arrows (`edgeStyle=orthogonalEdgeStyle;curved=1`)
- Arrows should pass through separator lines cleanly
- Create one prominent "main data flow" arrow that wraps around at the bottom
- Color-code arrows to match their source section
- Use shadows on main arrows for depth

### 5. Professional Polish Checklist

- [ ] Dark header bar with title (fillColor=#232F3E)
- [ ] "Built on AWS" badge in top-right (fillColor=#FF9900)
- [ ] Color-coded section headers with rounded corners
- [ ] Section subtitles below headers (e.g., "Managed by Synapxe", "Private Subnet")
- [ ] Consistent icon sizes (64x64px)
- [ ] Vertical icon stacking within columns
- [ ] Legend section at bottom
- [ ] SCP/Policy callout box
- [ ] Version and date in footer
- [ ] Source references

### Professional Color Palette

| Section | Background | Border | Header |
|---------|------------|--------|--------|
| External | #F5F5F5 | #546E7A | #546E7A |
| Border Control | #FFEBEE | #C62828 | #C62828 |
| Ingress | #E8F5E9 | #2E7D32 | #2E7D32 |
| Application | #E3F2FD | #1565C0 | #1565C0 |
| Data (RSH) | #FCE4EC | #AD1457 | #AD1457 |
| Security | #E8EAF6 | #303F9F | #303F9F |
| Compliance | #F3E5F5 | #7B1FA2 | #7B1FA2 |
| Central Logging | #FBE9E7 | #BF360C | #BF360C |
| Outputs | #FFF8E1 | #F57F17 | #F57F17 |
| Pipeline | #E0F2F1 | #00695C | #00695C |

### Section Container Template

```xml
<!-- Section Container with Header -->
<mxCell id="section-{name}" parent="1" style="rounded=1;whiteSpace=wrap;html=1;fillColor={bg-color};strokeColor={border-color};strokeWidth=3;shadow=1;" value="" vertex="1">
  <mxGeometry height="520" width="{width}" x="{x}" y="110" as="geometry" />
</mxCell>
<mxCell id="section-{name}-header" parent="1" style="text;html=1;strokeColor=none;fillColor={header-color};align=center;verticalAlign=middle;whiteSpace=wrap;rounded=1;fontSize=13;fontStyle=1;fontColor=#FFFFFF;" value="{SECTION NAME}" vertex="1">
  <mxGeometry height="30" width="{header-width}" x="{header-x}" y="120" as="geometry" />
</mxCell>
<mxCell id="section-{name}-subtitle" parent="1" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontSize=10;fontColor={header-color};" value="{subtitle}" vertex="1">
  <mxGeometry height="20" width="180" x="{subtitle-x}" y="150" as="geometry" />
</mxCell>
```

---

## Draw.io Editable Output (Optional)

If the user requests an **editable** diagram, generate a `.drawio` file with embedded AWS icon images.

### Draw.io AWS Icon URL Reference

Use these official AWS Architecture Icon URLs for proper rendering:

```
Base URL: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist

Compute:
- EC2: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Compute/EC2.png
- Lambda: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Compute/Lambda.png
- Fargate: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Compute/Fargate.png
- Batch: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Compute/Batch.png

Containers:
- ECS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Containers/ElasticContainerService.png
- EKS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Containers/ElasticKubernetesService.png
- ECR: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Containers/ElasticContainerRegistry.png

Database:
- Aurora: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/Aurora.png
- RDS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/RDS.png
- DynamoDB: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/DynamoDB.png
- ElastiCache: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/ElastiCache.png
- Redshift: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/Redshift.png

Networking:
- ALB: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/ElasticLoadBalancingApplicationLoadBalancer.png
- NLB: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/ElasticLoadBalancingNetworkLoadBalancer.png
- API Gateway: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/APIGateway.png
- CloudFront: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/CloudFront.png
- Route53: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/Route53.png
- VPC: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/VirtualPrivateCloud.png
- Internet Gateway: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/VPCInternetGateway.png
- NAT Gateway: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/VPCNATGateway.png
- Transit Gateway: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/TransitGateway.png
- Direct Connect: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/NetworkingContentDelivery/DirectConnect.png

Storage:
- S3: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/SimpleStorageService.png
- EFS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/ElasticFileSystem.png
- EBS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/ElasticBlockStore.png
- FSx: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/FSx.png

Security & Identity (CRITICAL - Use most relevant):
- IAM: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/IdentityandAccessManagement.png
- IAM Identity Center: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/IAMIdentityCenter.png
- WAF: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/WAF.png
- Shield: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/Shield.png
- KMS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/KeyManagementService.png
- Secrets Manager: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/SecretsManager.png
- Cognito: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/Cognito.png
- Directory Service: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/DirectoryService.png
- Resource Access Manager: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/ResourceAccessManager.png
- Certificate Manager: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/CertificateManager.png
- GuardDuty: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/GuardDuty.png
- Security Hub: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/SecurityHub.png
- Inspector: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/Inspector.png
- Macie: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/Macie.png
- Detective: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/Detective.png

Management & Governance (CRITICAL for Landing Zone diagrams):
- Organizations: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/Organizations.png
- Control Tower: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/ControlTower.png
- CloudWatch: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/CloudWatch.png
- CloudTrail: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/CloudTrail.png
- Config: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/Config.png
- Systems Manager: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/SystemsManager.png
- Trusted Advisor: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v18.0/dist/ManagementGovernance/TrustedAdvisor.png
- Service Catalog: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/ServiceCatalog.png
- Well-Architected Tool: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/WellArchitectedTool.png
- OpsWorks: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ManagementGovernance/OpsWorks.png

Developer Tools (CRITICAL for CI/CD diagrams):
- CodePipeline: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/DeveloperTools/CodePipeline.png
- CodeBuild: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/DeveloperTools/CodeBuild.png
- CodeDeploy: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/DeveloperTools/CodeDeploy.png
- CodeCommit: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/DeveloperTools/CodeCommit.png
- Cloud9: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/DeveloperTools/Cloud9.png
- CloudShell: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/DeveloperTools/CloudShell.png
- X-Ray: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/DeveloperTools/XRay.png

Cloud Financial Management:
- Cost Explorer: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/CloudFinancialManagement/CostExplorer.png
- Budgets: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v18.0/dist/CloudFinancialManagement/Budgets.png
- Savings Plans: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/CloudFinancialManagement/SavingsPlans.png

Analytics:
- QuickSight: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/QuickSight.png
- Lake Formation: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/LakeFormation.png
- Athena: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/Athena.png
- Glue: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/Glue.png
- Kinesis: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/Kinesis.png
- Kinesis Data Firehose: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v18.0/dist/Analytics/KinesisDataFirehose.png
- EMR: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/EMR.png
- OpenSearch: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/OpenSearchService.png
- MSK (Kafka): https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Analytics/ManagedStreamingforApacheKafka.png

Integration:
- SQS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/SimpleQueueService.png
- SNS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/SimpleNotificationService.png
- EventBridge: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/EventBridge.png
- Step Functions: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/StepFunctions.png
- AppSync: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/AppSync.png

Machine Learning:
- SageMaker: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/MachineLearning/SageMaker.png
- Bedrock: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/MachineLearning/Bedrock.png
- Rekognition: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/MachineLearning/Rekognition.png
- Comprehend: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/MachineLearning/Comprehend.png

General:
- Users: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/General/Users.png
- User: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/General/User.png
- Internet: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/General/Internet.png
- Client: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/General/Client.png
```

### Icon Selection Quick Reference (Draw.io)

**⚠️ ALWAYS use the most relevant icon based on component PURPOSE:**

| Account/Component | Use This Icon | NOT This |
|-------------------|---------------|----------|
| Audit Account | TrustedAdvisor | CloudWatch |
| Log Archive | SimpleStorageService | CloudTrail |
| Identity Mgmt | IAMIdentityCenter | IAM |
| Security Breakglass | IAM | SecurityHub |
| Network Account | VirtualPrivateCloud | EC2 |
| Directory | DirectoryService | IAM |
| DNS Account | Route53 | VPC |
| Ops Account | SystemsManager | EC2 |
| Dev Account | Cloud9 | EC2 |
| Pipeline | CodePipeline | Lambda |
| Ref Components | ServiceCatalog | S3 |
| CCoE | WellArchitectedTool | Organizations |
| FinOps | CostExplorer | CloudWatch |
| Marketing | QuickSight | S3 |
| Data Lake | LakeFormation | S3 |

### Icon-Label Spacing Guidelines (CRITICAL for Customer Presentations)

**⚠️ IMPORTANT:** Proper spacing between icons and labels is essential for professional, customer-ready diagrams.

#### Account Box Icon Placement

When placing icons inside account boxes, follow these spacing rules:

| Box Size | Icon Size | Icon Position | Label Spacing |
|----------|-----------|---------------|---------------|
| Width 300px, Height 35px | 24x24px | x+8, y+6 (centered vertically) | `spacingLeft=36` in style |
| Width 160-170px, Height 30px | 20x20px | x+6, y+5 (centered vertically) | `spacingLeft=28` in style |
| Width 160-170px, Height 28px | 20x20px | x+6, y+4 (centered vertically) | `spacingLeft=28` in style |

#### Style Template for Account Box with Icon

**Large Account Box (300px wide):**
```xml
<!-- Account box with left-aligned text and icon space -->
<mxCell id="account-box" value="        Account Name" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#C62828;strokeWidth=1;fontSize=11;align=left;spacingLeft=36;" parent="1" vertex="1">
  <mxGeometry x="80" y="445" width="300" height="35" as="geometry" />
</mxCell>
<!-- Icon positioned inside box with 8px left margin, vertically centered -->
<mxCell id="account-icon" value="" style="image;aspect=fixed;html=1;points=[];align=center;image={icon-url};" parent="1" vertex="1">
  <mxGeometry x="88" y="451" width="24" height="24" as="geometry" />
</mxCell>
```

**Small Account Box (160-170px wide):**
```xml
<!-- Smaller account box -->
<mxCell id="account-box" value="      Account Name" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#7B1FA2;strokeWidth=1;fontSize=10;align=left;spacingLeft=28;" parent="1" vertex="1">
  <mxGeometry x="460" y="445" width="160" height="30" as="geometry" />
</mxCell>
<!-- Smaller icon (20x20) with 6px margin -->
<mxCell id="account-icon" value="" style="image;aspect=fixed;html=1;points=[];align=center;image={icon-url};" parent="1" vertex="1">
  <mxGeometry x="466" y="450" width="20" height="20" as="geometry" />
</mxCell>
```

#### Spacing Formula

```
Icon X position = Box X + 8px (left margin)
Icon Y position = Box Y + ((Box Height - Icon Height) / 2)  (vertical center)
Label spacingLeft = Icon Width + 12px (comfortable gap between icon and text)
```

#### Visual Spacing Reference

```
┌─────────────────────────────────────────────────────────────┐
│  ┌──────┐                                                   │
│  │ ICON │   [12px gap]   Label Text                        │
│  └──────┘                                                   │
│                                                             │
│  ←8px→  ←24px→  ←12px→                                      │
│         icon    gap                                         │
└─────────────────────────────────────────────────────────────┘

For Large Boxes (300px): spacingLeft=36 (8 + 24 icon + 4 extra padding)
For Small Boxes (160px): spacingLeft=28 (6 + 20 icon + 2 extra padding)
```

#### Key Principles

1. **Consistent margins** - Use 8px margin from box edge to icon
2. **Vertical centering** - Icons should be vertically centered in the box
3. **Clear gap** - Minimum 8px gap between icon right edge and label text
4. **Text alignment** - Use `align=left;spacingLeft=X` to push text right of icon
5. **Leading spaces** - Add spaces in the value string for fine-tuning: `value="      Label"`

### Draw.io Icon Cell Template

Use this mxCell style for AWS icons with embedded images:

```xml
<mxCell id="{id}" value="{label}" style="image;aspect=fixed;html=1;points=[];align=center;fontSize=12;image={icon-url};labelPosition=center;verticalLabelPosition=bottom;verticalAlign=top;" vertex="1" parent="{parent-id}">
  <mxGeometry x="{x}" y="{y}" width="60" height="60" as="geometry" />
</mxCell>
```

### Draw.io Container Templates

**AWS Cloud:**
```xml
<mxCell id="aws-cloud" value="AWS Cloud" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=0;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_aws_cloud_alt;strokeColor=#232F3E;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#232F3E;dashed=0;" vertex="1" parent="1">
  <mxGeometry x="40" y="100" width="900" height="600" as="geometry" />
</mxCell>
```

**Region:**
```xml
<mxCell id="region" value="us-east-1" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=0;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_region;strokeColor=#00A4A6;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=1;" vertex="1" parent="aws-cloud">
  <mxGeometry x="20" y="40" width="860" height="540" as="geometry" />
</mxCell>
```

**VPC:**
```xml
<mxCell id="vpc" value="VPC (10.0.0.0/16)" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=0;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_vpc2;strokeColor=#8C4FFF;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#AAB7B8;dashed=0;" vertex="1" parent="region">
  <mxGeometry x="20" y="40" width="820" height="480" as="geometry" />
</mxCell>
```

**Availability Zone:**
```xml
<mxCell id="az-a" value="Availability Zone A" style="fillColor=none;strokeColor=#147EBA;dashed=1;verticalAlign=top;fontStyle=0;fontColor=#147EBA;whiteSpace=wrap;html=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;" vertex="1" parent="vpc">
  <mxGeometry x="20" y="40" width="380" height="400" as="geometry" />
</mxCell>
```

**Public Subnet (green):**
```xml
<mxCell id="public-subnet" value="Public Subnet&#xa;10.0.1.0/24" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=0;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_security_group;grStroke=0;strokeColor=#7AA116;fillColor=#F2F6E8;verticalAlign=top;align=left;spacingLeft=30;fontColor=#248814;dashed=0;" vertex="1" parent="az-a">
  <mxGeometry x="20" y="30" width="340" height="110" as="geometry" />
</mxCell>
```

**Private Subnet (blue):**
```xml
<mxCell id="private-subnet" value="Private Subnet&#xa;10.0.10.0/24" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=0;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_security_group;grStroke=0;strokeColor=#00A4A6;fillColor=#E6F6F7;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=0;" vertex="1" parent="az-a">
  <mxGeometry x="20" y="160" width="340" height="110" as="geometry" />
</mxCell>
```

### Draw.io Arrow Template (Live Connected)

**Main Flow Arrow (Connected to Source/Target elements):**
```xml
<mxCell id="flow-{source}-{target}" edge="1" parent="1" source="{source-id}" target="{target-id}" style="edgeStyle=orthogonalEdgeStyle;curved=1;html=1;rounded=1;strokeWidth=3;strokeColor=#FF9900;endArrow=blockThin;endFill=1;endSize=8;shadow=0;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" value="">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Secondary Flow Arrow (Dashed, Thinner):**
```xml
<mxCell id="flow-dashed-{n}" edge="1" parent="1" source="{source-id}" target="{target-id}" style="edgeStyle=orthogonalEdgeStyle;curved=1;html=1;rounded=1;strokeWidth=2;strokeColor=#303F9F;endArrow=blockThin;endFill=1;endSize=6;dashed=1;dashPattern=8 4;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" value="">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Large Wrap-Around Arrow (for main data flow):**
```xml
<mxCell id="flow-data-outputs-main" edge="1" parent="1" style="edgeStyle=orthogonalEdgeStyle;curved=1;html=1;rounded=1;strokeWidth=4;strokeColor=#F57F17;endArrow=blockThin;endFill=1;endSize=10;shadow=1;" value="">
  <mxGeometry relative="1" as="geometry">
    <Array as="points">
      <mxPoint x="{mid-x}" y="{bottom-y}" />
      <mxPoint x="{target-x}" y="{bottom-y}" />
    </Array>
    <mxPoint x="{source-x}" y="{source-y}" as="sourcePoint" />
    <mxPoint x="{target-x}" y="{target-y}" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### Draw.io Vertical Separator Line Template (Thin)

```xml
<mxCell id="sep-{n}" value="" style="endArrow=none;dashed=1;html=1;dashPattern=4 4;strokeWidth=1;strokeColor=#BDBDBD;" edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="{x}" y="100" as="sourcePoint" />
    <mxPoint x="{x}" y="640" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### Draw.io File Structure

```xml
<mxfile host="app.diagrams.net">
  <diagram name="{diagram-name}" id="{diagram-id}">
    <mxGraphModel dx="1434" dy="836" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1100" pageHeight="850" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Add containers and icons here -->

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Generate Draw.io Output

When user requests editable diagram:
1. Save to: `diagrams/{name}.drawio`
2. Use embedded image URLs for all AWS service icons
3. Use AWS4 group shapes for containers (VPC, Region, Subnets)
4. Test by opening in https://app.diagrams.net

---

## Example Usage

```bash
/plantuml-aws-diagram serverless API with API Gateway, Lambda, and DynamoDB
/plantuml-aws-diagram 3-tier web app with ALB, EC2, and Aurora
/plantuml-aws-diagram event-driven architecture with EventBridge and Lambda
/plantuml-aws-diagram data pipeline with Kinesis, Lambda, and S3
/plantuml-aws-diagram multi-region DR setup
/plantuml-aws-diagram 3-tier web app --editable   # generates .drawio file
```

## Output

**For PlantUML (default):**
1. PlantUML file path: `plantuml-diagrams/{name}.puml`
2. PNG file path: `diagrams/{name}.png`
3. Command to regenerate: `plantuml plantuml-diagrams/{name}.puml -o diagrams/`

**For Draw.io (when --editable or "editable" requested):**
1. Draw.io file path: `diagrams/{name}.drawio`
2. Open in: https://app.diagrams.net or VS Code with Draw.io extension
3. All icons render as embedded images (no shape library needed)

**⚠️ MANDATORY Clear Flow Checklist:**
- [ ] **All process steps are numbered** (1, 2, 3, 4, 5, 6, 7...)
- [ ] **Arrows connect EVERY consecutive step** (1→2, 2→3, 3→4...)
- [ ] **Flow direction is LEFT-TO-RIGHT** within each row
- [ ] **Row transitions use curved arrows** (down from Row 1 to Row 2)
- [ ] **Badge, Icon, Label are properly aligned** for each step
- [ ] **Supporting services are separated** from main flow (smaller icons, gray)
- [ ] **Arrow color matches badge color** (typically green #388E3C)
- [ ] **Final arrow points to next section** (down arrow to OUs, etc.)

**⚠️ MANDATORY Professional Standards Checklist:**
- [ ] Thin vertical dashed separator lines (strokeWidth=1, #BDBDBD) between ALL sections
- [ ] Live flow arrows using `source=` and `target=` attributes (strokeWidth=3)
- [ ] Arrows connect from right edge of source to left edge of target (exitX=1, entryX=0)
- [ ] Large wrap-around data flow arrow at bottom (strokeWidth=4, orange #F57F17)
- [ ] Dashed arrows (strokeWidth=2) for secondary flows (security, compliance)
- [ ] Spacious column layout with 60-80px gaps between sections
- [ ] Icons stacked vertically within columns (64x64px)
- [ ] Color-coded sections matching the Professional Color Palette
- [ ] Dark header bar (#232F3E) with "Built on AWS" badge (#FF9900)
- [ ] Legend section at bottom
- [ ] Version/date footer

---

## Quality Notes

All production-ready AWS architecture diagrams MUST include the following quality elements:

### 1. Official AWS Icons
- Use official AWS icons from aws-icons-for-plantuml **v19.0** (latest stable)
- Base URL: `https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist`
- Icon size: 64x64px for optimal visibility
- Consistent icon styling throughout the diagram

### 2. Flow Animations on Connectors
- Enable `flowAnimation=1` on main data flow arrows for dynamic presentation
- Use on primary flow paths (left-to-right data movement)
- Apply to pipeline step connections
- Example: `style="...;flowAnimation=1;"`

```xml
<mxCell id="flow-main" edge="1" parent="1" source="src" target="tgt"
  style="edgeStyle=orthogonalEdgeStyle;curved=1;html=1;rounded=1;strokeWidth=3;strokeColor=#00695C;endArrow=blockThin;endFill=1;flowAnimation=1;" value="">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 3. Proper Color-Coded Legend
- Include a legend section at the bottom of every diagram
- Each architectural zone must have a corresponding legend entry
- Use the same fill and border colors as the main sections
- Legend items should be 40px height, 90px width
- Include labels with fontStyle=1 (bold)

```xml
<!-- Legend Item Template -->
<mxCell id="legend-{name}" parent="1" style="rounded=1;whiteSpace=wrap;html=1;fillColor={bg-color};strokeColor={border-color};fontSize=10;strokeWidth=2;fontStyle=1;" value="{Label}" vertex="1">
  <mxGeometry height="40" width="90" x="{x}" y="925" as="geometry" />
</mxCell>
```

### 4. SCPs Documented
- Include a Service Control Policies (SCPs) callout box in the legend area
- Document key organizational policies applied to the architecture
- Use warning/highlight color (yellow: #FFF9C4 with #F57F17 border)
- Common SCPs to document:
  - `DenyNonSingaporeRegions` (or applicable region restriction)
  - `RequireEncryption` (encryption at rest/transit)
  - `RequireCloudTrail` (audit logging)
  - `DenyPublicS3` (S3 bucket security)
  - `EnforceIMDSv2` (EC2 metadata security)

```xml
<mxCell id="scp-callout" parent="1" style="text;html=1;strokeColor=#F57F17;fillColor=#FFF9C4;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=1;fontSize=11;fontColor=#5D4037;strokeWidth=2;" value="&lt;b&gt;SCPs:&lt;/b&gt; DenyNonSingaporeRegions | RequireEncryption | RequireCloudTrail | DenyPublicS3 | EnforceIMDSv2" vertex="1">
  <mxGeometry height="45" width="550" x="1400" y="920" as="geometry" />
</mxCell>
```

### 5. Source References
- Include source/reference documentation in the footer area
- Cite compliance frameworks, AWS guides, or internal standards
- Use subtle gray text (#757575) aligned to the right
- Examples:
  - `Sources: HIM-CS v1.1 | AWS Partner Guide HCC | Multi-Account Strategy`
  - `Based on: AWS Well-Architected Framework | SOC2 Requirements`

```xml
<mxCell id="sources" parent="1" style="text;html=1;strokeColor=none;fillColor=none;align=right;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontSize=10;fontColor=#757575;" value="Sources: {framework} | {guide} | {standard}" vertex="1">
  <mxGeometry height="20" width="180" x="1820" y="880" as="geometry" />
</mxCell>
```

### 6. Version and Date Footer
- Always include version number and date in bottom-right corner
- Format: `v{major}.{minor} | {Month} {Year}`
- Use bold font style for visibility

```xml
<mxCell id="version" parent="1" style="text;html=1;strokeColor=none;fillColor=none;align=right;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontSize=10;fontColor=#757575;fontStyle=1;" value="v3.0 | January 2026" vertex="1">
  <mxGeometry height="15" width="110" x="1860" y="970" as="geometry" />
</mxCell>
```

### Quality Checklist Summary

| Element | Required | Notes |
|---------|----------|-------|
| AWS Icons v19.0 | ✅ | Official icons only |
| Flow Animations | ✅ | On main data paths |
| Color-Coded Legend | ✅ | Match section colors |
| SCPs Documented | ✅ | Key policies listed |
| Source References | ✅ | Compliance/framework citations |
| Version/Date | ✅ | Bottom-right footer |
