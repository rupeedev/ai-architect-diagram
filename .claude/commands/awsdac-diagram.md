---
description: Generate AWS architecture diagrams using awslabs/diagram-as-code (awsdac)
---

# AWS Diagram Generator (awsdac)

Generate professional AWS architecture diagrams using the official awslabs/diagram-as-code tool with YAML configuration.

## Input
$ARGUMENTS

## Instructions

### Step 1: Analyze Architecture Requirements

Parse the user input to understand:
- What type of architecture is requested
- Which AWS services are needed
- The relationships and data flow between components
- Any specific layout preferences

### Step 2: Create YAML Configuration

Generate an awsdac-compatible YAML file with this structure:

```yaml
# {Diagram Name}
# awsdac diagram - AWS Diagram as Code

Diagram:
  DefinitionFiles:
    - Type: URL
      Url: "https://raw.githubusercontent.com/awslabs/diagram-as-code/main/definitions/definition-for-aws-icons-light.yaml"

  Resources:
    # Canvas - Top level container
    Canvas:
      Type: AWS::Diagram::Canvas
      Direction: vertical
      Children:
        - AWSCloud

    # AWS Cloud container
    AWSCloud:
      Type: AWS::Diagram::Cloud
      Preset: AWSCloudNoLogo
      Direction: vertical
      Align: center
      Children:
        - Region

    # Region
    Region:
      Type: AWS::Region
      Title: {region-name}
      Direction: vertical
      Children:
        - {component-groups}

    # Add resources here...

  Links:
    - Source: {source-resource}
      SourcePosition: {N|S|E|W}
      Target: {target-resource}
      TargetPosition: {N|S|E|W}
      TargetArrowHead:
        Type: Open
```

### Step 3: AWS Resource Type Reference

**Containers & Layout:**
- `AWS::Diagram::Canvas` - Root container
- `AWS::Diagram::Cloud` - AWS Cloud (Preset: `AWSCloudNoLogo`)
- `AWS::Diagram::HorizontalStack` - Horizontal layout
- `AWS::Diagram::VerticalStack` - Vertical layout
- `AWS::Region` - AWS Region container
- `AWS::EC2::VPC` - VPC container
- `AWS::EC2::Subnet` - Subnet (Presets: `PublicSubnet`, `PrivateSubnet`)

**Compute:**
- `AWS::EC2::Instance` - EC2 Instance
- `AWS::Lambda::Function` - Lambda Function
- `AWS::ECS::Cluster` - ECS Cluster
- `AWS::Batch` - AWS Batch

**Networking:**
- `AWS::EC2::InternetGateway` - Internet Gateway
- `AWS::EC2::NatGateway` - NAT Gateway
- `AWS::EC2::TransitGateway` - Transit Gateway
- `AWS::ElasticLoadBalancingV2::LoadBalancer` - Load Balancer
  - Preset: `Application Load Balancer`
  - Preset: `Network Load Balancer`
- `AWS::ApiGateway` - API Gateway
- `AWS::Route53::HostedZone` - Route 53

**Storage:**
- `AWS::S3::Bucket` - S3 Bucket
- `AWS::EFS::FileSystem` → falls back to `AWS::EFS`

**Database:**
- `AWS::RDS::DBCluster` - Aurora/RDS Cluster
- `AWS::DynamoDB::Table` - DynamoDB Table
- `AWS::ElastiCache::CacheCluster` - ElastiCache

**Security:**
- `AWS::WAF::WebACL` - WAF
- `AWS::Shield` - Shield
- `AWS::NetworkFirewall` - Network Firewall
- `AWS::GuardDuty` - GuardDuty
- `AWS::SecurityHub` - Security Hub
- `AWS::KMS::Key` → falls back to `AWS::KMS`
- `AWS::SecretsManager::Secret` - Secrets Manager
- `AWS::IAM` - IAM
- `AWS::SSO` - IAM Identity Center
- `AWS::Macie` - Macie
- `AWS::Detective` - Detective
- `AWS::Inspector` - Inspector

**Monitoring & Management:**
- `AWS::CloudWatch` - CloudWatch
- `AWS::CloudTrail::Trail` - CloudTrail
- `AWS::Config` - Config
- `AWS::ControlTower` - Control Tower
- `AWS::Organizations::Account` - Organizations Account
- `AWS::Backup` - AWS Backup

**Integration:**
- `AWS::StepFunctions::StateMachine` → falls back to `AWS::StepFunctions`
- `AWS::SNS::Topic` - SNS Topic
- `AWS::SQS::Queue` - SQS Queue

**External:**
- `AWS::Diagram::Resource` with Preset: `Client` - External systems
- `AWS::Diagram::Resource` with Preset: `User` - Users

---

## CRITICAL: Professional Arrow Guidelines

### The Golden Rules

1. **LESS IS MORE** - Professional diagrams use MINIMAL arrows
2. **NEVER CROSS BOXES** - Arrows must NEVER pass through container boxes
3. **STRUCTURE TELLS THE STORY** - Vertical position implies hierarchy (top controls bottom)
4. **HORIZONTAL ONLY** - Within awsdac, use ONLY horizontal arrows (E→W or W→E)

### Why awsdac Requires Horizontal-Only Arrows

awsdac draws STRAIGHT LINES between connection points - it has NO smart routing.
- If you draw from top to bottom, arrows will CROSS THROUGH boxes
- This looks unprofessional and cluttered
- The ONLY safe arrows are horizontal within the same tier/box

### What NOT To Do (Common Mistakes)

```
FATAL: Arrows crossing through container boxes (awsdac can't route around)
BAD: Drawing arrows from every service to every related service
BAD: Vertical arrows crossing through multiple tiers/layers
BAD: Arrows from top-level services down to bottom services
BAD: Connecting every account to shared services with arrows
```

**Example of BAD diagram:**
```
┌─────────────────────────────────────┐
│  Service A ──┐                      │
│              │ ←── Crossing arrows  │
│  ┌───────────┼──────────────────┐   │
│  │ Tier 1    ↓    ↑             │   │
│  │  Box1 ←───┼────┼─── Box2     │   │
│  └───────────┼────┼─────────────┘   │
│              ↓    │                 │
│  ┌───────────┼────┼─────────────┐   │
│  │ Tier 2    ↓    │             │   │
│  │  Box3 ────┼────┘             │   │
│  └───────────┼──────────────────┘   │
│              ↓                      │
│  Service B ←─┘                      │
└─────────────────────────────────────┘
```

### What TO Do (Best Practices)

```
GOOD: Only horizontal arrows within the same tier/layer
GOOD: Show logical data flow, not every connection
GOOD: Let containment imply organizational hierarchy
GOOD: Maximum 1-2 arrows per row/tier
GOOD: Use vertical POSITION to imply control/data flow (top → bottom)
GOOD: Group related services in labeled boxes with clear purpose
GOOD: NEVER leave services as orphans - always put in a labeled container
```

### Use Structure to Tell the Story (No Arrows Needed)

```
┌─────────────────────────────────────────────┐
│  "Governance Layer"  │  "Identity Layer"   │  ← TOP = Controls everything
│   (Organizations)    │     (SSO, RAM)      │
├─────────────────────────────────────────────┤
│              OU / Account Structure          │  ← MIDDLE = Managed resources
│   ┌─────────────┐  ┌─────────────┐          │
│   │ Security OU │  │ Workload OU │          │
│   └─────────────┘  └─────────────┘          │
├─────────────────────────────────────────────┤
│  "Networking"  │  "Monitoring"  │ "Compliance"│  ← BOTTOM = Shared services
│  (TGW, AD)     │  (CloudTrail)  │ (Config)   │
└─────────────────────────────────────────────┘

The POSITION tells the story:
- TOP layer GOVERNS the middle
- BOTTOM layer SERVES the middle
- No arrows needed between layers!
```

**Example of GOOD diagram:**
```
┌─────────────────────────────────────┐
│  Service A    Service B    Service C│  (No arrows needed - same level)
│                                     │
│  ┌──────────────────────────────┐   │
│  │ Tier 1                       │   │
│  │  Box1 ──→ Box2 ──→ Box3      │   │  (Clean horizontal flow)
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ Tier 2                       │   │
│  │  BoxA ──→ BoxB               │   │  (Clean horizontal flow)
│  └──────────────────────────────┘   │
│                                     │
│  ServiceX    ServiceY    ServiceZ   │  (No arrows needed - same level)
└─────────────────────────────────────┘
```

### Arrow Decision Matrix

| Scenario | Draw Arrow? | Why |
|----------|-------------|-----|
| Components in same horizontal row showing data flow | YES | Shows processing sequence |
| Parent container to child | NO | Containment implies relationship |
| Service in Tier 1 to Service in Tier 3 | NO | Creates visual clutter |
| Cross-account relationships | NO | OU containment implies it |
| Every service to logging/monitoring | NO | Assumed - don't clutter |
| Pipeline stages (A → B → C) | YES | Shows clear data flow |
| Load balancer to multiple instances | MAYBE | Only if showing distribution |

### Recommended Arrow Count by Diagram Type

| Diagram Type | Max Arrows | Arrow Pattern |
|--------------|------------|---------------|
| Landing Zone (Multi-Account) | 5-8 | Horizontal within OUs only |
| 3-Tier Architecture | 3-5 | Vertical through main data path only |
| Data Pipeline | 5-10 | Linear flow through stages |
| Security Layers | 3-6 | Horizontal within layers |
| Network Diagram | 5-8 | Key traffic flows only |

### Per-Tier Arrow Rules

**Landing Zone / Multi-Account:**
- Draw horizontal arrows within Security OU (Log Archive → Audit → Security Tooling)
- Draw horizontal arrows within Workload OUs (Dev → Staging, Prod-A → Prod-B)
- Draw horizontal arrows in Shared Services layer
- NEVER draw vertical arrows from Governance to OUs to Shared Services

**3-Tier Web Architecture:**
- Draw: User → ALB → App → Database (main data path)
- DON'T draw: Every component to CloudWatch, every component to KMS

**Data Pipeline:**
- Draw: Linear flow through processing stages
- DON'T draw: Every Lambda to S3, every service to logging

---

### Step 4: Link Configuration

**CRITICAL: Always specify explicit positions for all links**

```yaml
Links:
  - Source: ComponentA
    SourcePosition: S    # Required: N, S, E, W
    Target: ComponentB
    TargetPosition: N    # Required: N, S, E, W
    TargetArrowHead:
      Type: Open
```

**Position Guide:**
- `N` - North (top)
- `S` - South (bottom)
- `E` - East (right)
- `W` - West (left)

**Common Link Patterns:**
- Horizontal flow (left to right): Source `E` → Target `W` (PREFERRED)
- Vertical flow (top to bottom): Source `S` → Target `N` (USE SPARINGLY)
- Reverse horizontal: Source `W` → Target `E`
- Reverse vertical: Source `N` → Target `S`

### Step 5: Generate Diagram

1. Save the YAML file:
   ```
   {diagram-name}.yaml
   ```

2. Generate the PNG:
   ```bash
   awsdac {diagram-name}.yaml -o {diagram-name}.png -f
   ```

3. Verify the output file was created successfully

### Step 6: Handle Common Errors

**Type not defined errors:**
- If a type is not defined, awsdac falls back to the service icon
- Some types (like `AWS::CloudHSM`, `AWS::CostExplorer`) are not available
- Use alternative types when errors occur

**Position errors:**
- Always include `SourcePosition` and `TargetPosition` in all links
- Valid values: `N`, `S`, `E`, `W` only

**Child not found errors:**
- Ensure all Children references exist as Resources
- Check spelling matches exactly

---

## Architecture Templates

### Multi-Account Landing Zone
```yaml
# Arrow strategy: HORIZONTAL ONLY within same tier
Links:
  # Security OU - audit chain (horizontal)
  - Source: LogArchive
    SourcePosition: E
    Target: Audit
    TargetPosition: W

  # Workloads - deployment flow (horizontal)
  - Source: Dev
    SourcePosition: E
    Target: Staging
    TargetPosition: W

  # Shared Services (horizontal)
  - Source: TransitGateway
    SourcePosition: E
    Target: DirectoryService
    TargetPosition: W

# NO vertical arrows crossing OUs!
```

### 3-Tier Web Application
```yaml
# Arrow strategy: Main data path only
Links:
  # Public → App tier (vertical - main flow)
  - Source: ALB
    SourcePosition: S
    Target: AppServer
    TargetPosition: N

  # App → Database (vertical - main flow)
  - Source: AppServer
    SourcePosition: S
    Target: Database
    TargetPosition: N

  # Horizontal within App tier
  - Source: AppServer1
    SourcePosition: E
    Target: AppServer2
    TargetPosition: W

# NO arrows to CloudWatch, KMS, etc. - implied!
```

### Data Pipeline
```yaml
# Arrow strategy: Linear processing flow
Links:
  # Stage 1 → Stage 2 (horizontal pipeline)
  - Source: Ingest
    SourcePosition: E
    Target: Transform
    TargetPosition: W

  - Source: Transform
    SourcePosition: E
    Target: Enrich
    TargetPosition: W

  - Source: Enrich
    SourcePosition: E
    Target: Store
    TargetPosition: W

# NO arrows from every stage to S3 - implied!
```

### 5-Layer Security
```yaml
# Arrow strategy: Horizontal within each layer
Links:
  # Layer 4: Detection flow (horizontal)
  - Source: GuardDuty
    SourcePosition: E
    Target: SecurityHub
    TargetPosition: W

  - Source: SecurityHub
    SourcePosition: E
    Target: Detective
    TargetPosition: W

  # Layer 5: Compliance flow (horizontal)
  - Source: Config
    SourcePosition: E
    Target: AuditManager
    TargetPosition: W

# NO vertical arrows between layers!
```

---

## Pre-Generation Checklist

Before generating, verify:

- [ ] Total arrows < 10 for most diagrams
- [ ] No vertical arrows crossing multiple tiers
- [ ] Horizontal arrows only within same tier/layer
- [ ] No arrows from top services to bottom services
- [ ] Containment used instead of arrows for hierarchy
- [ ] Each row/tier has maximum 2-3 arrows
- [ ] Main data flow is clear without excessive detail

---

## Example Usage

```bash
/awsdac-diagram 3-tier web application with ALB, ECS, and Aurora
/awsdac-diagram serverless API with Lambda and DynamoDB
/awsdac-diagram multi-account landing zone with 5 accounts
/awsdac-diagram data pipeline with S3, Batch, and Step Functions
/awsdac-diagram 5-layer security architecture
```

## Output

Provide the user with:
1. YAML file path: `{name}.yaml`
2. PNG file path: `{name}.png`
3. File size confirmation
4. Arrow count and strategy used
5. Command to regenerate: `awsdac {name}.yaml -o {name}.png -f`
