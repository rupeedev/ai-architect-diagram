# PlantUML Setup Guide for Beginners

Welcome! This guide will help you install PlantUML on your Mac and create cool AWS architecture diagrams. Think of PlantUML as a magic tool that turns simple text into professional pictures!

---

## What is PlantUML?

PlantUML is like a drawing robot. You write simple instructions in a text file, and it creates beautiful diagrams for you. No need to drag and drop boxes - just type and let PlantUML do the drawing!

---

## Step 1: Install Java (The Engine)

PlantUML needs Java to run - think of Java as the engine that powers our drawing robot.

Open your **Terminal** app (you can find it in Applications > Utilities > Terminal) and type:

```bash
brew install openjdk
```

Wait for it to finish. You'll see some text scrolling - that's normal!

**What if `brew` doesn't work?**
If you see "command not found", you need to install Homebrew first:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

## Step 2: Install PlantUML (The Drawing Robot)

Now let's install PlantUML itself:

```bash
brew install plantuml
```

Wait for it to finish. Once done, you have PlantUML installed!

---

## Step 3: Check if It Works

Let's make sure everything is working:

```bash
plantuml -version
```

You should see something like "PlantUML version 1.2024..." - that means it's working!

---

## Step 4: Create Your First Diagram

### 4.1 Create a New File

Create a new file called `my-first-diagram.puml` in your project folder. You can use any text editor (VS Code, TextEdit, etc.)

### 4.2 Write Your Diagram Code

Copy and paste this into your file:

```plantuml
@startuml my-first-diagram

' This tells PlantUML where to find AWS icons
!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist
!include AWSPuml/AWSCommon.puml

' Include the icons we want to use
!include AWSPuml/Compute/Lambda.puml
!include AWSPuml/Database/DynamoDB.puml
!include AWSPuml/Storage/SimpleStorageService.puml

' Set the direction (left to right)
left to right direction

' Create our components
Lambda(myFunction, "My App", "Processes data")
DynamoDB(myDatabase, "My Database", "Stores info")
SimpleStorageService(myBucket, "My Storage", "Keeps files")

' Connect them with arrows
myFunction --> myDatabase : saves data
myFunction --> myBucket : uploads files

@enduml
```

### 4.3 Generate the Picture

In Terminal, navigate to your folder and run:

```bash
plantuml my-first-diagram.puml
```

A new file called `my-first-diagram.png` will appear in the same folder. Open it to see your diagram!

---

## Step 5: Understanding the Code

Let's break down what each part does:

| Code | What It Does |
|------|-------------|
| `@startuml` | Starts the diagram |
| `@enduml` | Ends the diagram |
| `!include` | Brings in AWS icons |
| `Lambda(...)` | Creates a Lambda icon |
| `-->` | Draws an arrow |
| `' comment` | Notes for yourself (PlantUML ignores these) |

---

## Step 6: Try More AWS Icons

Here are some popular AWS icons you can use:

### Compute (Servers and Functions)
```plantuml
!include AWSPuml/Compute/EC2.puml
!include AWSPuml/Compute/Lambda.puml
```

### Database (Where Data Lives)
```plantuml
!include AWSPuml/Database/DynamoDB.puml
!include AWSPuml/Database/RDS.puml
```

### Storage (File Storage)
```plantuml
!include AWSPuml/Storage/SimpleStorageService.puml
```

### Networking (Internet Stuff)
```plantuml
!include AWSPuml/NetworkingContentDelivery/CloudFront.puml
!include AWSPuml/NetworkingContentDelivery/APIGateway.puml
```

---

## Step 7: A Complete Example

Here's a more complete example showing a simple web app:

```plantuml
@startuml simple-web-app

!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v19.0/dist
!include AWSPuml/AWSCommon.puml

!include AWSPuml/General/User.puml
!include AWSPuml/NetworkingContentDelivery/CloudFront.puml
!include AWSPuml/Storage/SimpleStorageService.puml
!include AWSPuml/NetworkingContentDelivery/APIGateway.puml
!include AWSPuml/Compute/Lambda.puml
!include AWSPuml/Database/DynamoDB.puml

left to right direction

' A user visits the website
User(user, "Visitor", "Uses the app")

' The website components
CloudFront(cdn, "CloudFront", "Fast delivery")
SimpleStorageService(website, "S3 Bucket", "Website files")
APIGateway(api, "API Gateway", "Handles requests")
Lambda(backend, "Lambda", "Runs code")
DynamoDB(database, "DynamoDB", "Stores data")

' Connect everything
user --> cdn : visits
cdn --> website : gets pages
user --> api : sends requests
api --> backend : triggers
backend --> database : reads/writes

@enduml
```

Save this as `simple-web-app.puml` and run:

```bash
plantuml simple-web-app.puml
```

---

## Quick Reference Commands

| What You Want | Command |
|---------------|---------|
| Create diagram | `plantuml filename.puml` |
| Save to different folder | `plantuml filename.puml -o output-folder/` |
| Check PlantUML version | `plantuml -version` |

---

## Troubleshooting

### "Command not found"
Make sure you installed both Java and PlantUML using the commands above.

### Diagram looks weird
- Check your arrows: use `-->` not `->>`
- Make sure every `@startuml` has a matching `@enduml`
- Check that your icon names are spelled correctly

### Icons not showing
Make sure you have internet connection - PlantUML downloads icons from the web.

---

## What's Next?

Now that you can create basic diagrams, try:
1. Adding more AWS services
2. Grouping things in boxes (use `rectangle "Name" { ... }`)
3. Changing arrow colors with `#FF0000` (that's red!)

Have fun creating diagrams!

---

## Useful Links

- PlantUML Website: https://plantuml.com/
- AWS Icons for PlantUML: https://github.com/awslabs/aws-icons-for-plantuml
- All AWS Icon Names: https://github.com/awslabs/aws-icons-for-plantuml/blob/main/AWSSymbols.md
