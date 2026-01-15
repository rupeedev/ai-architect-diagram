---
description: Generate AWS architecture diagrams using PlantUML with official AWS icons
---

# AWS Diagram Generator (PlantUML)

Generate professional AWS architecture diagrams using PlantUML with the official AWS-PlantUML icon library.

**⚠️ REQUIRED:** All diagrams MUST follow the [Professional Diagram Design Standards](#professional-diagram-design-standards) section, including:
- Vertical dotted separator lines between sections
- Large, prominent curved arrows (strokeWidth=5-6)
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

**Security:**
```
!include AWSPuml/SecurityIdentityCompliance/IAM.puml
!include AWSPuml/SecurityIdentityCompliance/Cognito.puml
!include AWSPuml/SecurityIdentityCompliance/WAF.puml
!include AWSPuml/SecurityIdentityCompliance/Shield.puml
!include AWSPuml/SecurityIdentityCompliance/KMS.puml
!include AWSPuml/SecurityIdentityCompliance/SecretsManager.puml
!include AWSPuml/SecurityIdentityCompliance/GuardDuty.puml
!include AWSPuml/SecurityIdentityCompliance/SecurityHub.puml
!include AWSPuml/SecurityIdentityCompliance/Inspector.puml
```

**Application Integration:**
```
!include AWSPuml/ApplicationIntegration/SNS.puml
!include AWSPuml/ApplicationIntegration/SQS.puml
!include AWSPuml/ApplicationIntegration/StepFunctions.puml
!include AWSPuml/ApplicationIntegration/EventBridge.puml
!include AWSPuml/ApplicationIntegration/AppSync.puml
```

**Management:**
```
!include AWSPuml/ManagementGovernance/CloudWatch.puml
!include AWSPuml/ManagementGovernance/CloudTrail.puml
!include AWSPuml/ManagementGovernance/Config.puml
!include AWSPuml/ManagementGovernance/Organizations.puml
!include AWSPuml/ManagementGovernance/ControlTower.puml
!include AWSPuml/ManagementGovernance/SystemsManager.puml
```

**Analytics:**
```
!include AWSPuml/Analytics/Kinesis.puml
!include AWSPuml/Analytics/Athena.puml
!include AWSPuml/Analytics/Glue.puml
!include AWSPuml/Analytics/QuickSight.puml
!include AWSPuml/Analytics/EMR.puml
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
- ECS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Containers/ElasticContainerService.png
- EKS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Containers/ElasticKubernetesService.png
- Fargate: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Compute/Fargate.png

Database:
- Aurora: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/Aurora.png
- RDS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/RDS.png
- DynamoDB: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/DynamoDB.png
- ElastiCache: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Database/ElastiCache.png

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

Storage:
- S3: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/SimpleStorageService.png
- EFS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/ElasticFileSystem.png
- EBS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/Storage/ElasticBlockStore.png

Security:
- IAM: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/IdentityandAccessManagement.png
- WAF: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/WAF.png
- KMS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/KeyManagementService.png
- Secrets Manager: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/SecretsManager.png
- Cognito: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/SecurityIdentityCompliance/Cognito.png

Integration:
- SQS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/SimpleQueueService.png
- SNS: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/SimpleNotificationService.png
- EventBridge: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/EventBridge.png
- Step Functions: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/ApplicationIntegration/StepFunctions.png

General:
- Users: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/General/Users.png
- User: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/General/User.png
- Internet: https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist/General/Internet.png
```

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
