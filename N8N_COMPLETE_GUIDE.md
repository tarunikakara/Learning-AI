# n8n Complete Guide - From Beginner to Advanced

## Table of Contents
1. [What is n8n?](#what-is-n8n)
2. [Why Choose n8n?](#why-choose-n8n)
3. [Installation & Setup](#installation--setup)
4. [n8n Interface Walkthrough](#n8n-interface-walkthrough)
5. [Understanding Nodes](#understanding-nodes)
6. [Workflow Basics](#workflow-basics)
7. [Sample Flow #1: Simple Email Workflow](#sample-flow-1-simple-email-workflow)
8. [Sample Flow #2: Customer Data Processing](#sample-flow-2-customer-data-processing)
9. [Sample Flow #3: Multi-Step Automation with Logic](#sample-flow-3-multi-step-automation-with-logic)
10. [Adding Memory to Workflows](#adding-memory-to-workflows)
11. [Memory Implementation Patterns](#memory-implementation-patterns)
12. [Sample Flow #4: Agent with Memory](#sample-flow-4-agent-with-memory)
13. [Error Handling & Advanced Features](#error-handling--advanced-features)
14. [Best Practices](#best-practices)
15. [Troubleshooting Guide](#troubleshooting-guide)

---

## What is n8n?

### Definition

**n8n** (pronounced "nodin") is a **free, open-source workflow automation platform** that lets you create complex automation workflows visually without writing code.

```
n8n = "Nodes and connections"
      A visual programming language for automation
```

### Key Features

```
┌────────────────────────────────────────────────────┐
│              n8n KEY FEATURES                      │
├────────────────────────────────────────────────────┤
│                                                    │
│ ✓ 400+ Pre-built Integrations                     │
│   (Google, Slack, Salesforce, GitHub, etc.)       │
│                                                    │
│ ✓ Visual Workflow Editor                          │
│   (Drag-and-drop interface)                        │
│                                                    │
│ ✓ No Coding Required                              │
│   (Anyone can build workflows)                     │
│                                                    │
│ ✓ Open Source & Free                              │
│   (Community-driven, self-hosted option)           │
│                                                    │
│ ✓ Powerful Node Library                           │
│   (HTTP, Database, Conditions, Loops, etc.)       │
│                                                    │
│ ✓ Webhook Support                                 │
│   (Trigger workflows from external systems)       │
│                                                    │
│ ✓ Scheduling & Cron                               │
│   (Run workflows at specific times)                │
│                                                    │
│ ✓ Error Handling                                  │
│   (Gracefully handle failures)                     │
│                                                    │
│ ✓ Data Persistence                                │
│   (Store and retrieve workflow data)               │
│                                                    │
│ ✓ Active Community                                │
│   (Support, templates, documentation)             │
│                                                    │
└────────────────────────────────────────────────────┘
```

### n8n vs Other Tools

```
┌──────────────┬─────────┬────────┬─────────┬──────────┐
│ Feature      │ n8n     │ Zapier │ Make    │ IFTTT    │
├──────────────┼─────────┼────────┼─────────┼──────────┤
│ Cost         │ FREE    │ $25-   │ $9.99-  │ FREE     │
│ Open Source  │ YES     │ NO     │ NO      │ NO       │
│ Self-Hosted  │ YES     │ NO     │ NO      │ NO       │
│ Integrations │ 400+    │ 3000+  │ 1000+   │ 500+     │
│ Complexity   │ Medium  │ Simple │ Simple  │ Very     │
│ Learning     │ Easy    │ Very   │ Very    │ Very     │
│ Customization│ High    │ Medium │ Low     │ Low      │
│ Community    │ Active  │ Large  │ Growing │ Large    │
│ Database     │ Built-in│ Limited│ Limited │ NO       │
│ API Required │ Some    │ All    │ All     │ All      │
└──────────────┴─────────┴────────┴─────────┴──────────┘
```

---

## Why Choose n8n?

### Advantages

```
COST EFFECTIVE:
✓ Free to use (open-source)
✓ No per-action charges
✓ Self-hosted option saves money
✓ Perfect for startups and enterprises

POWERFUL:
✓ Handle complex workflows
✓ Advanced conditional logic
✓ Looping and batch processing
✓ Error handling and recovery

FLEXIBLE:
✓ 400+ integrations
✓ Custom code support (JavaScript, Python)
✓ webhooks for infinite possibilities
✓ API output for connecting anything

DEVELOPER-FRIENDLY:
✓ Open source code
✓ Extensible with plugins
✓ Well-documented
✓ Active community

PRIVACY & CONTROL:
✓ Self-hosted option (your server)
✓ No data sent to external services
✓ Complete data control
✓ Compliance-friendly
```

---

## Installation & Setup

### Option 1: Cloud (Easiest)

```
Step 1: Visit https://app.n8n.cloud
Step 2: Sign up with email or GitHub
Step 3: Create first organization
Step 4: Start building workflows

Time: 5 minutes
Cost: FREE tier available
Maintenance: n8n handles everything
```

### Option 2: Self-Hosted with Docker (Recommended)

```
Prerequisites:
✓ Docker installed (https://www.docker.com)
✓ Docker compose

Installation:
1. Create docker-compose.yml file
2. Add n8n configuration:

version: '3'
services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=password123
    volumes:
      - n8n_data:/home/node/.n8n
      
volumes:
  n8n_data:

3. Run: docker-compose up

Access: http://localhost:5678
Username: admin
Password: password123

Benefits:
✓ Complete control
✓ No cloud dependency
✓ Better data privacy
✓ Cost-effective for production
```

### Option 3: Local Installation

```
Prerequisites:
✓ Node.js 14+ installed
✓ npm or yarn

Installation:
1. npm install -g n8n
2. n8n start
3. Open: http://localhost:5678

Pros: Simple, local development
Cons: Not ideal for production
```

---

## n8n Interface Walkthrough

### Main Dashboard

```
┌─────────────────────────────────────────────────────────┐
│                    n8n DASHBOARD                        │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────┐  ┌──────────────────────────┐            │
│  │  n8n     │  │ Workflows (List view)    │            │
│  │ Logo     │  │                          │            │
│  └──────────┘  │ • Welcome Email          │            │
│                │ • Process Orders         │            │
│  Sidebar:      │ • Customer Sync          │            │
│  ├─ Workflows │ • Data Pipeline          │            │
│  ├─ Templates │                          │            │
│  ├─ Executions│ [+ New Workflow]          │            │
│  ├─ Settings │                          │            │
│  └─ Help     │                          │            │
│                │                          │            │
│                └──────────────────────────┘            │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Workflow Editor

```
┌──────────────────────────────────────────────────────────┐
│                  WORKFLOW EDITOR                        │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Top Bar:                                               │
│  [Workflow Name] [Save] [Activate] [Execute] [Help]    │
│                                                          │
│  ┌────────────────────────────────────────────────┐    │
│  │                                                │    │
│  │   [Webhook]                                    │    │
│  │     ↓                                          │    │
│  │   [Parse JSON]                                 │    │
│  │     ↓                                          │    │
│  │   [IF/ELSE]  ──→ [Send Email Y]              │    │
│  │     ↓         \→ [Send Email N]              │    │
│  │   [Send Slack]                                │    │
│  │                                                │    │
│  │   CANVAS - Where you build workflows           │    │
│  │   Zoom: Ctrl/Cmd + Scroll to zoom             │    │
│  │   Pan: Click and drag to move around          │    │
│  │                                                │    │
│  └────────────────────────────────────────────────┘    │
│                                                          │
│  Node Panel (Right):                                    │
│  ┌─────────────────────┐                               │
│  │ [Settings] [Logs]   │                               │
│  │                     │                               │
│  │ Node1 Settings:     │                               │
│  │ ├─ Resource         │                               │
│  │ ├─ Method           │                               │
│  │ ├─ URL              │                               │
│  │ └─ Headers          │                               │
│  │                     │                               │
│  └─────────────────────┘                               │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

### Adding Nodes

```
STEP 1: Click the "+" button
        (between nodes or on canvas)

STEP 2: Search for node type
        Example: "Gmail"
        
        Search results:
        • Gmail
        • Google Calendar
        • Google Sheets
        • Google Forms
        
STEP 3: Click to add node

STEP 4: Configure node settings
        • Select resources
        • Enter parameters
        • Map data from previous nodes
        
STEP 5: Connect nodes
        Click output → Click input of next node
        Automatic connection created
```

### Node Connections

```
Node Output → Node Input

Each node has:
• Inputs (left side) - receives data from previous nodes
• Outputs (right side) - sends data to next nodes

Connection Rules:
✓ Output of one node → Input of another
✓ One output can connect to multiple inputs
✓ One input usually takes one output
✓ Data flows left to right, top to bottom
```

---

## Understanding Nodes

### Node Categories

```
┌────────────────────────────────────────────────────────┐
│              NODE CATEGORIES IN n8n                   │
├────────────────────────────────────────────────────────┤
│                                                        │
│ 1. TRIGGER NODES (Start workflow)                     │
│    • Webhook                                          │
│    • Cron (Schedule)                                  │
│    • Manual                                           │
│    • Event-based                                      │
│                                                        │
│ 2. ACTION NODES (Perform actions)                     │
│    • HTTP Request                                     │
│    • Gmail, Slack, Teams                              │
│    • Google Sheets, Docs                              │
│    • Salesforce, HubSpot                              │
│    • Database operations                              │
│                                                        │
│ 3. LOGIC NODES (Control flow)                         │
│    • IF/ELSE (Conditional)                            │
│    • Loop                                             │
│    • Switch                                           │
│    • Merge                                            │
│    • Wait (Delay)                                     │
│                                                        │
│ 4. DATA NODES (Transform data)                        │
│    • Set (Assign values)                              │
│    • Function                                         │
│    • Code (JavaScript/Python)                         │
│    • Aggregate                                        │
│    • Split (Array)                                    │
│                                                        │
│ 5. OUTPUT NODES (Send results)                        │
│    • Respond to Webhook                               │
│    • Return data to trigger                           │
│                                                        │
└────────────────────────────────────────────────────────┘
```

### Common Node Types with Examples

#### Webhook Node (Trigger)
```
PURPOSE: Listen for incoming HTTP requests

CONFIGURATION:
• HTTP Method: POST, GET, PUT, etc.
• URL: Auto-generated (e.g., https://n8n.io/webhook/abc123)
• Authentication: None, Basic Auth, or Header Auth

USAGE:
External system sends data to webhook URL
↓
n8n receives and starts workflow

EXAMPLE CONFIG:
├─ Method: POST
├─ URL: https://n8n.io/webhook/customer-signup
├─ Authentication: Header Auth (X-API-Key: secret123)
└─ Response: Return JSON

INCOMING DATA (from external system):
{
  "customer_name": "John Doe",
  "email": "john@example.com",
  "phone": "+1234567890"
}
```

#### HTTP Request Node (Action)
```
PURPOSE: Make API calls to external services

CONFIGURATION:
• Method: GET, POST, PUT, DELETE, PATCH
• URL: https://api.example.com/endpoint
• Headers: Authorization, Content-Type, etc.
• Body: Data to send
• Authentication: API Key, OAuth, Basic Auth

EXAMPLE - GET Request:
├─ Method: GET
├─ URL: https://api.weatherapi.com/v1/current.json
├─ Query Parameters:
│  ├─ key: YOUR_API_KEY
│  └─ q: {{ $json.city }}
└─ Returns: Weather data

EXAMPLE - POST Request:
├─ Method: POST
├─ URL: https://api.sendgrid.com/v3/mail/send
├─ Headers:
│  ├─ Authorization: Bearer SG.xxxxx
│  └─ Content-Type: application/json
├─ Body:
│  {
│    "personalizations": [{
│      "to": [{"email": "john@example.com"}]
│    }],
│    "from": {"email": "noreply@mycompany.com"},
│    "subject": "Welcome!",
│    "content": [{"type": "text/plain", "value": "Hi John"}]
│  }
└─ Returns: Success response
```

#### Set Node (Data Transformation)
```
PURPOSE: Create or modify data structure

CONFIGURATION:
• Key/Value pairs to set
• Can reference data from previous nodes

EXAMPLE 1 - Create new data:
ASSIGN:
├─ full_name: John Doe
├─ email: john@example.com
├─ timestamp: {{ $now.toISOString() }}
└─ status: active

OUTPUT:
{
  "full_name": "John Doe",
  "email": "john@example.com",
  "timestamp": "2026-03-27T10:00:00Z",
  "status": "active"
}

EXAMPLE 2 - Map data from previous node:
INPUT: { user_id: 123, first_name: John }

ASSIGN:
├─ id: {{ $json.user_id }}
├─ name: {{ $json.first_name }}
└─ created_at: {{ new Date().toISOString() }}

OUTPUT:
{
  "id": 123,
  "name": "John",
  "created_at": "2026-03-27T10:00:00Z"
}
```

#### IF/ELSE Node (Conditional Logic)
```
PURPOSE: Branch workflow based on conditions

CONFIGURATION:
• Set condition(s) to check
• Define IF TRUE path
• Define IF FALSE path (optional)

EXAMPLE:
Condition: {{ $json.amount > 1000 }}

IF TRUE:
  ├─ Send high-value alert
  ├─ Apply premium discount
  └─ Escalate to manager

IF FALSE:
  ├─ Send normal confirmation
  ├─ Apply standard discount
  └─ Log transaction

CONDITION TYPES:
• String equals: {{ $json.status }} === "pending"
• Number comparison: {{ $json.price }} > 100
• Array check: {{ $json.tags }}.includes("urgent")
• Date comparison: {{ $json.date }} > "2026-01-01"
• Multiple conditions:
  {{ $json.status }} === "active" && 
  {{ $json.age }} >= 18 && 
  {{ $json.verified }} === true
```

#### Loop Node (Iteration)
```
PURPOSE: Repeat action for each item in array

CONFIGURATION:
• Input: Array of items
• Items execute the same nodes inside loop

EXAMPLE:
Array of customers: [Customer1, Customer2, Customer3]

LOOP:
For each customer:
  ├─ Get customer details
  ├─ Send email
  ├─ Update database
  └─ Log activity

ITERATIONS:
Iteration 1: Process Customer1
  ├─ Get: customer_id = 101
  ├─ Send email to john@example.com
  ├─ Update: last_email_sent = 2026-03-27
  └─ Log: Customer 101 processed

Iteration 2: Process Customer2
  ├─ Get: customer_id = 102
  ├─ Send email to jane@example.com
  ├─ Update: last_email_sent = 2026-03-27
  └─ Log: Customer 102 processed

Iteration 3: Process Customer3
  └─ (same pattern)

OUTPUT: 3 completed iterations
```

#### Cron Node (Schedule)
```
PURPOSE: Trigger workflow at specific times

CONFIGURATION:
• Cron expression or simplified settings

SIMPLIFIED SETTINGS:
• Every 5 minutes
• Every hour
• Every day at 9 AM
• Every Monday at 8 AM
• Every 1st of month

CRON EXPRESSIONS:
0 0 * * * = Every day at midnight
0 9 * * * = Every day at 9 AM
*/5 * * * * = Every 5 minutes
0 */6 * * * = Every 6 hours
0 8 * * MON = Every Monday at 8 AM
0 0 1 * * = Every 1st of month at midnight

TYPICAL USE CASES:
• Daily report generation
• Scheduled backups
• Regular data sync
• Automated cleanup
```

---

## Workflow Basics

### Workflow Anatomy

```
┌─────────────────────────────────────────────────────┐
│             BASIC WORKFLOW STRUCTURE                │
├─────────────────────────────────────────────────────┤
│                                                     │
│  TRIGGER:
│  ├─ Webhook
│  ├─ Cron (Schedule)
│  └─ Manual
│       ↓
│  DATA INTAKE:
│  ├─ Parse input
│  ├─ Validate data
│  └─ Extract fields
│       ↓
│  PROCESSING:
│  ├─ Conditional logic (IF/ELSE)
│  ├─ Transform data (Set node)
│  ├─ Make external calls (HTTP)
│  ├─ Query database
│  └─ Loop through items
│       ↓
│  ACTION:
│  ├─ Send email/message
│  ├─ Update database
│  ├─ Create record
│  └─ Call API
│       ↓
│  OUTPUT:
│  ├─ Return response
│  ├─ Send notification
│  └─ Store result
│                                                     │
└─────────────────────────────────────────────────────┘
```

### Data Flow Through Nodes

```
NODE REFERENCE SYNTAX:
{{ $json.field_name }}

EXAMPLE FLOW:

Node 1 (Webhook):
Receives: {
  "email": "john@example.com",
  "subject": "Hello"
}

Node 2 (Set):
Uses: {{ $json.email }}
Creates: { email: "john@example.com", status: "active" }

Node 3 (IF/ELSE):
Checks: {{ $json.status }} === "active"
Decides: TRUE → Send email

Node 4 (Gmail):
Uses: {{ $json.email }}
Sends email to: john@example.com with subject: {{ $json.subject }}

All nodes have data accessible via $json variable
```

### Node Output Names

```
When connecting nodes, n8n creates "items" (outputs)

Example:
Node 1 output: item[0] = { id: 1, name: "John" }
Node 2 receives: {{ $json.id }}, {{ $json.name }}

Access nested data:
{{ $json.user.profile.email }}

Access array items:
{{ $json.items[0] }}
{{ $json.items[1] }}

Access from previous nodes in chain:
{{ $node["Node Name"].json.fieldName }}
```

---

## Sample Flow #1: Simple Email Workflow

### Scenario
When someone submits a form, send them a welcome email automatically.

### Visual Workflow

```
┌──────────┐
│ Webhook  │ (Receives form submission)
└─────┬────┘
      │ Data: { name, email, company }
      ▼
┌──────────────┐
│ Set Values   │ (Prepare email data)
└─────┬────────┘
      │ Creates: { fromEmail, toEmail, subject, body }
      ▼
┌──────────┐
│ Gmail    │ (Send email)
└─────┬────┘
      │ Sends welcome email
      ▼
┌──────────────────┐
│ Response Node    │ (Return confirmation)
└──────────────────┘
```

### Step-by-Step Setup

#### Step 1: Create Webhook Trigger
```
1. Click "+" → Search "Webhook" → Select Webhook
2. Configure:
   • HTTP Method: POST
   • URL: Generated automatically (Copy & save this)
   • Authentication: None (for now)
3. Click "Test the node"
4. Copy the webhook URL for testing
```

#### Step 2: Add Set Node
```
1. Click "+" → Search "Set" → Select Set
2. Connect Webhook → Set (drag connector)
3. Configure Values:
   ├─ fromEmail: noreply@mycompany.com
   ├─ toEmail: {{ $json.email }}
   ├─ subject: Welcome to our service, {{ $json.name }}!
   ├─ body: Hi {{ $json.name }}, thanks for signing up!
   └─ signature: Best regards, MyCompany Team
```

#### Step 3: Add Gmail Node
```
1. Click "+" → Search "Gmail" → Select Gmail
2. Connect Set → Gmail
3. Configure:
   ├─ Gmail account: [Connect your Gmail]
   ├─ To: {{ $json.toEmail }}
   ├─ Subject: {{ $json.subject }}
   ├─ Text: {{ $json.body }}\n\n{{ $json.signature }}
   └─ Save
```

#### Step 4: Add Response Node
```
1. Click "+" → Search "Respond" → Select "Respond to Webhook"
2. Connect Gmail → Respond
3. Configure:
   ├─ Status Code: 200
   ├─ Response Body:
   │  {
   │    "success": true,
   │    "message": "Welcome email sent to {{ $json.email }}",
   │    "timestamp": {{ Date.now() }}
   │  }
   └─ Save
```

#### Step 5: Activate & Test
```
SAVE WORKFLOW:
1. Click "Save" button (top left)
2. Name it: "Welcome Email Workflow"

ACTIVATE:
1. Toggle "Active" switch (top right)
   Status changes to: Active

TEST:
Use curl or Postman to send test data:

curl -X POST https://n8n.io/webhook/abc123def456 \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "company": "Acme Corp"
  }'

Expected Response:
{
  "success": true,
  "message": "Welcome email sent to john@example.com",
  "timestamp": 1711529400000
}

CHECK RESULTS:
1. Open n8n dashboard
2. Click "Executions" tab
3. See successful execution ✓
4. Check Gmail inbox for welcome email ✓
```

---

## Sample Flow #2: Customer Data Processing

### Scenario
When a new customer is added to a database, enrich their data with external APIs and store the complete profile.

### Visual Workflow

```
┌──────────────────┐
│ Database         │ (Triggers on new customer)
│ (New record)     │
└────────┬─────────┘
         │ Data: { name, email, zipcode }
         ▼
┌──────────────────┐
│ HTTP Request     │ (Get location from zipcode)
│ (GeoAPI)         │
└────────┬─────────┘
         │ Returns: { city, state, country }
         ▼
┌──────────────────┐
│ Set Values       │ (Merge all data)
└────────┬─────────┘
         │ Complete profile ready
         ▼
┌──────────────────┐
│ Database         │ (Save enriched profile)
│ (Update record)  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Slack Message    │ (Notify team)
└──────────────────┘
```

### Detailed Setup

#### Step 1: Database Trigger (PostgreSQL)
```
1. Add Node → Search "PostgreSQL" → Select PostgreSQL
2. Configure:
   ├─ Connection: [Setup your DB connection]
   ├─ Query Type: "Listen for table changes"
   ├─ Table: "customers"
   ├─ Listen to: "INSERT"
   └─ Save

TRIGGER CONFIG:
When: A new row is inserted in customers table
Data received: { id, name, email, zipcode, created_at }
```

#### Step 2: HTTP Request for Geo Data
```
1. Add Node → Search "HTTP" → Select "HTTP Request"
2. Configure:
   ├─ Method: GET
   ├─ URL: https://api.zippopotam.us/us/{{ $json.zipcode }}
   ├─ Headers:
   │  └─ Content-Type: application/json
   └─ Save

REQUEST:
GET https://api.zippopotam.us/us/10001

RESPONSE:
{
  "post code": "10001",
  "country": "United States",
  "country abbreviation": "US",
  "places": [
    {
      "place name": "New York",
      "longitude": "-74.0097",
      "state": "NY",
      "state abbreviation": "NY",
      "latitude": "40.7143"
    }
  ]
}
```

#### Step 3: Set Node (Data Enrichment)
```
1. Add Node → Search "Set" → Select Set
2. Configure extraction from previous nodes:
   ├─ customer_id: {{ $json.id }}
   ├─ customer_name: {{ $json.name }}
   ├─ customer_email: {{ $json.email }}
   ├─ zipcode: {{ $json.zipcode }}
   ├─ city: {{ $node["HTTP Request"].json.places[0]["place name"] }}
   ├─ state: {{ $node["HTTP Request"].json.places[0]["state"] }}
   ├─ country: {{ $node["HTTP Request"].json.country }}
   ├─ enriched_at: {{ Date.now() }}
   └─ data_quality: "complete"

OUTPUT:
{
  "customer_id": 12345,
  "customer_name": "John Doe",
  "customer_email": "john@example.com",
  "zipcode": "10001",
  "city": "New York",
  "state": "NY",
  "country": "United States",
  "enriched_at": 1711529400000,
  "data_quality": "complete"
}
```

#### Step 4: Database Update
```
1. Add Node → Search "PostgreSQL" → Select PostgreSQL
2. Configure:
   ├─ Query Type: "Execute query"
   ├─ Query: 
   │  UPDATE customers
   │  SET 
   │    city = '{{ $json.city }}',
   │    state = '{{ $json.state }}',
   │    country = '{{ $json.country }}',
   │    enriched_at = NOW(),
   │    data_quality = '{{ $json.data_quality }}'
   │  WHERE id = {{ $json.customer_id }}
   └─ Save

RESULT: Customer record updated with enriched data
```

#### Step 5: Slack Notification
```
1. Add Node → Search "Slack" → Select "Slack"
2. Configure:
   ├─ Slack channel: #new-customers
   ├─ Message:
   │  🎉 New customer added!
   │  Name: {{ $json.customer_name }}
   │  Email: {{ $json.customer_email }}
   │  Location: {{ $json.city }}, {{ $json.state }}
   │  Data Quality: {{ $json.data_quality }}
   └─ Save
```

---

## Sample Flow #3: Multi-Step Automation with Logic

### Scenario
Complex workflow: When customer makes purchase, validate order, check inventory, apply discounts, and send confirmation.

### Visual Workflow

```
           ┌────────────────────┐
           │ Webhook Trigger    │
           │ (Purchase received)│
           └─────────┬──────────┘
                     │
                     ▼
           ┌────────────────────┐
           │ Set Node           │
           │ (Initialize data)  │
           └─────────┬──────────┘
                     │
                     ▼
        ┌────────────────────────┐
        │ IF/ELSE Condition #1   │
        │ Is amount > $100?      │
        └──┬─────────────────────┘
           │                  │
        YES│                  │NO
           │                  │
           ▼                  ▼
    ┌────────────┐    ┌──────────────┐
    │ Premium    │    │ Regular      │
    │ Discount   │    │ Discount     │
    │ (20%)      │    │ (5%)         │
    └─────┬──────┘    └────────┬─────┘
           │                   │
           └─────────┬─────────┘
                     │
                     ▼
        ┌────────────────────────┐
        │ Database Query         │
        │ Check inventory        │
        └──┬─────────────────────┘
           │
           ▼
        ┌────────────────────────┐
        │ IF/ELSE Condition #2   │
        │ Stock available?       │
        └──┬─────────────────────┘
           │                  │
        YES│                  │NO
           │                  │
           ▼                  ▼
    ┌────────────┐    ┌──────────────┐
    │ Create     │    │ Send Out of  │
    │ Order      │    │ Stock Email  │
    │ (confirmed)│    │              │
    └─────┬──────┘    └────────┬─────┘
           │                   │
           ├───────────┬───────┤
           │           │       │
           ▼           ▼       ▼
        ┌────────────────────────┐
        │ Loop through items     │
        │ (For each product)     │
        └──┬─────────────────────┘
           │
           ├─ Update inventory
           ├─ Send thank you email
           └─ Send tracking info
           
           ▼
        ┌────────────────────────┐
        │ Slack Notification     │
        │ (Team notified)        │
        └────────────────────────┘
```

### Detailed Implementation

#### Step 1: Webhook Trigger
```
Configuration:
├─ Method: POST
├─ URL: https://n8n.io/webhook/purchase-order
└─ Returns: Data structured for next nodes

Sample Input Data:
{
  "order_id": "ORD-2026-001",
  "customer_id": 12345,
  "email": "john@example.com",
  "items": [
    {
      "product_id": "SKU-001",
      "product_name": "Laptop",
      "quantity": 1,
      "price": 599.99
    },
    {
      "product_id": "SKU-002",
      "product_name": "Mouse",
      "quantity": 2,
      "price": 19.99
    }
  ],
  "total_amount": 639.97,
  "shipping_address": "123 Main St, NY 10001"
}
```

#### Step 2: Set Node (Initialize)
```
Configuration:
├─ order_id: {{ $json.order_id }}
├─ customer_id: {{ $json.customer_id }}
├─ total_before_discount: {{ $json.total_amount }}
├─ discount_percentage: 0  (will be updated in next step)
├─ discount_amount: 0
├─ final_total: {{ $json.total_amount }}
├─ order_status: "pending_validation"
└─ created_at: {{ Date.now() }}
```

#### Step 3: Conditional - Discount Level
```
IF/ELSE Node Configuration:

Condition: {{ $json.total_before_discount }} > 100

IF TRUE (Order > $100):
├─ Action: Set discount to 20%
├─ discount_percentage: 20
├─ discount_amount: {{ $json.total_before_discount * 0.20 }}
├─ final_total: {{ $json.total_before_discount - ($json.total_before_discount * 0.20) }}
└─ customer_type: "premium"

IF FALSE (Order ≤ $100):
├─ Action: Set discount to 5%
├─ discount_percentage: 5
├─ discount_amount: {{ $json.total_before_discount * 0.05 }}
├─ final_total: {{ $json.total_before_discount - ($json.total_before_discount * 0.05) }}
└─ customer_type: "regular"
```

#### Step 4: Database Query - Check Inventory
```
PostgreSQL Query Node:

SELECT 
  product_id,
  product_name,
  quantity_in_stock,
  quantity_requested,
  (quantity_in_stock >= quantity_requested) as available
FROM inventory_check
WHERE product_id = ANY('{{ $json.items.map(item => item.product_id).join(",") }}')

Returns inventory status for each product
```

#### Step 5: Conditional - Stock Availability
```
IF/ELSE Node Configuration:

Condition: {{ $json.available === true }}

IF TRUE (Stock Available):
  ├─ Action: Proceed with order
  ├─ order_status: "confirmed"
  └─ Next nodes: Create order, send confirmations

IF FALSE (Out of Stock):
  ├─ Action: Cancel order
  ├─ order_status: "out_of_stock"
  └─ Next nodes: Send apology email, offer alternatives
```

#### Step 6: Loop Node (Process Line Items)
```
Loop Configuration:
├─ Loop over: Items array [[Product1], [Product2], ...]
├─ For each item:
│  ├─ Node: Update Inventory
│  │  └─ UPDATE inventory
│  │     SET quantity = quantity - {{ $json.quantity }}
│  │     WHERE product_id = {{ $json.product_id }}
│  │
│  ├─ Node: Send Thank You Email
│  │  └─ Subject: Thank you for {{ $json.product_name }}
│  │
│  └─ Node: Send Tracking Email
│     └─ Tracking info with estimated delivery
└─ After loop: Continue to next nodes
```

#### Step 7: Slack Notification
```
Send to Slack Channel: #orders

Message:
✅ Order #{{ $json.order_id }} Confirmed!

Customer: John Doe (ID: {{ $json.customer_id }})
Items: {{ $json.items.length }} product(s)
Subtotal: ${{ $json.total_before_discount }}
Discount: -${{ $json.discount_amount }} ({{ $json.discount_percentage }}%)
Final Total: ${{ $json.final_total }}

Status: {{ $json.order_status }}
Time: {{ Date.now() }}
```

---

## Adding Memory to Workflows

### What is Memory in n8n?

```
Memory = Persistent data storage
        Used to remember information between workflow executions

Use Cases:
✓ User preferences (remember favorite color, language)
✓ Customer history (track past purchases, interactions)
✓ Learning patterns (AI learns from past decisions)
✓ Session data (maintain state across executions)
✓ Analytics tracking (accumulate metrics over time)
```

### Storage Options in n8n

```
┌─────────────────────────────────────────┐
│     MEMORY STORAGE OPTIONS              │
├─────────────────────────────────────────┤
│                                         │
│ 1. DATABASE (Best for production)       │
│    • PostgreSQL                         │
│    • MySQL                              │
│    • MongoDB                            │
│    • Pros: Persistent, scalable, fast   │
│    • Cons: Requires DB setup            │
│                                         │
│ 2. FILE SYSTEM (Good for local)         │
│    • JSON files                         │
│    • CSV files                          │
│    • Pros: Simple, no DB needed         │
│    • Cons: Not scalable                 │
│                                         │
│ 3. EXTERNAL API (Cloud-based)           │
│    • Firebase/Firestore                 │
│    • AWS DynamoDB                       │
│    • MongoDB Atlas                      │
│    • Pros: Fully managed, global access │
│    • Cons: Requires API key, costs      │
│                                         │
│ 4. WEBHOOK STATE (Temporary)            │
│    • Store in intermediate nodes        │
│    • Pros: Quick, no external services  │
│    • Cons: Lost if workflow fails       │
│                                         │
└─────────────────────────────────────────┘
```

### Memory Implementation Patterns

#### Pattern 1: Simple User Profile Cache

```
GOAL: Remember user preferences after first interaction

WORKFLOW:

1. User sends first message:
   Input: { user_id: 123, language_preference: "Spanish" }

2. Check if user exists in database:
   Query: SELECT * FROM user_cache WHERE user_id = 123
   Result: Not found (first time)

3. Store user data:
   INSERT INTO user_cache VALUES:
   ├─ user_id: 123
   ├─ language_preference: Spanish
   ├─ first_seen: 2026-03-27
   └─ last_seen: 2026-03-27

4. Return confirmation:
   { status: "user_created", language: "Spanish" }

---

NEXT TIME - User sends second message:

1. Query user cache:
   SELECT * FROM user_cache WHERE user_id = 123
   Result: Found!

2. Retrieve preferences:
   ├─ language_preference: Spanish
   ├─ first_seen: 2026-03-27 (remember this customer!)
   └─ last_seen: 2026-03-27

3. Use preferences:
   ├─ Format response in Spanish
   ├─ Use familiar greetings
   └─ Suggest based on history

4. Update last_seen:
   UPDATE user_cache SET last_seen = NOW()
```

#### Pattern 2: Interaction History Tracking

```
GOAL: Learn from customer interactions

ARCHITECTURE:

┌─────────────────────────────────────────┐
│ INTERACTION_EVENTS TABLE                │
├─────────────────────────────────────────┤
│ id│ user_id│ event_type │ data   │date │
├─────────────────────────────────────────┤
│1  │101    │purchased   │laptop  │3/15 │
│2  │101    │purchased   │mouse   │3/16 │
│3  │101    │viewed      │phone   │3/17 │
│4  │101    │viewed      │tablet  │3/18 │
│5  │101    │clicked_ad  │laptop  │3/19 │
└─────────────────────────────────────────┘

ANALYSIS QUERY:
SELECT 
  user_id,
  COUNT(*) as interaction_count,
  AVG(event_type) as preferred_category,
  MAX(date) as last_interaction
FROM interaction_events
WHERE user_id = 101
GROUP BY user_id

LEARNING OUTPUT:
User 101 habits:
├─ Has 5 interactions (engaged customer)
├─ Interested in: Tech products (laptop, mouse, phone, tablet)
├─ Recently active (last: 3/19)
└─ Likely to purchase again

WORKFLOW ACTION:
├─ Show tech product recommendations
├─ Offer tech bundle discount
└─ Send email: "New laptops just arrived!"
```

#### Pattern 3: Conversation History (AI Memory)

```
GOAL: AI agent remembers conversation history

TABLE STRUCTURE:

CONVERSATIONS TABLE:
├─ conversation_id
├─ user_id
├─ message
├─ response
├─ timestamp

EXAMPLE DATA:

1. User: "I like hiking"
   Agent: "Great! I'll remember that."
   ├─ Stored: user_preference = "hiking"

2. User: "What should I do this weekend?"
   Query: SELECT * FROM conversations WHERE user_id = X ORDER BY timestamp DESC LIMIT 10
   Result: User likes hiking

   Agent: "Based on your love for hiking, I recommend..."
   Uses: Past conversation memory

3. User: "Tell me more about mountain trails"
   Query: User_preference: "hiking"
         Previous suggestion: Mountain trails
   
   Agent: "About mountain trails... (continuing from memory)"

WORKFLOW:

User Input → 
  ├─ Retrieve last 10 messages for context
  ├─ Pass to AI with history
  ├─ AI generates response with context
  ├─ Save new message pair
  └─ Return response

Result: Conversational AI that remembers!
```

---

## Sample Flow #4: Agent with Memory

### Scenario
Customer support agent that remembers customer history and personalizes responses.

### Complete Workflow with Memory

```
┌────────────────────┐
│ Webhook            │
│ (Customer message) │
└─────┬──────────────┘
      │
      ▼
┌────────────────────────────┐
│ Set - Extract data         │
│ from message               │
└─────┬──────────────────────┘
      │ { user_id, message, channel }
      ▼
┌────────────────────────────┐
│ Database Query #1          │
│ Get customer history       │
└─────┬──────────────────────┘
      │ Returns: { name, email, tier, purchase_history }
      ▼
┌────────────────────────────┐
│ Set - Prepare context      │
│ for AI model               │
└─────┬──────────────────────┘
      │ Combines: New message + history
      ▼
┌────────────────────────────┐
│ OpenAI / LLM Node          │
│ Generate response          │
└─────┬──────────────────────┘
      │ Uses prompt + memory context
      ▼
┌────────────────────────────┐
│ Database Query #2          │
│ Save conversation          │
│ to history                 │
└─────┬──────────────────────┘
      │
      ▼
┌────────────────────────────┐
│ Send Response              │
│ (Via email/chat)           │
└────────────────────────────┘
```

### Step-by-Step Implementation

#### Step 1: Webhook Trigger
```
Receives: {
  "user_id": 12345,
  "message": "I have an issue with my recent purchase",
  "channel": "email"
}
```

#### Step 2: Query Customer Memory (Database)
```
SQL Query:
SELECT 
  user_id,
  first_name,
  last_name,
  email,
  customer_tier,
  total_purchases,
  last_purchase_id,
  last_purchase_date,
  previous_issues,
  total_issues_resolved
FROM customers
WHERE user_id = '{{ $json.user_id }}'

RESPONSE:
{
  "user_id": 12345,
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "customer_tier": "Gold",
  "total_purchases": 15,
  "last_purchase_id": "ORD-2026-456",
  "last_purchase_date": "2026-03-20",
  "previous_issues": 3,
  "total_issues_resolved": 3
}
```

#### Step 3: Get Conversation History
```
SQL Query:
SELECT 
  message,
  response,
  resolution_time,
  satisfaction_score
FROM conversation_history
WHERE user_id = '{{ $json.user_id }}'
ORDER BY timestamp DESC
LIMIT 5

RESPONSE (Last 5 interactions):
[
  {
    "message": "Shipping took too long",
    "response": "We improve shipping time",
    "resolution_time": "2 hours",
    "satisfaction": 4.5
  },
  {
    "message": "Product quality issue",
    "resolution_time": "1 hour",
    "satisfaction": 5
  },
  ... (3 more)
]
```

#### Step 4: Create LLM Context
```
Set Node - Build context for AI:

system_prompt = """
You are a helpful customer support agent.
You have access to customer history and purchase data.
Personalize your responses using this information.
Your goal: Solve the issue and maintain customer satisfaction.
"""

customer_context = `
Customer Profile:
- Name: John Doe
- Tier: Gold (Loyal customer, 15 purchases)
- Email: john@example.com
- Last Purchase: Order #ORD-2026-456 on 2026-03-20

Previous Issues:
- 3 issues previously reported
- All 3 resolved to satisfaction
- Average resolution time: 1.5 hours
- Customer satisfaction: 4.8/5

Conversation History:
(Last 5 messages from customer)
1. Shipping took too long → Resolved
2. Product quality issue → Resolved
... (more context)

Current Issue:
"{{ $json.message }}"
`

final_prompt = system_prompt + customer_context
```

#### Step 5: Call AI Model (OpenAI)
```
OpenAI Node Configuration:

Model: gpt-3.5-turbo or gpt-4
Temperature: 0.7 (balanced)
Max Tokens: 300

Prompt:
{{ $json.final_prompt }}

SAMPLE RESPONSE:
"Hi John,

Thank you for reaching out, and I appreciate your continued loyalty as a Gold member!

I see your recent order #ORD-2026-456 from March 20th. I'm sorry you're experiencing an issue with this purchase.

Based on your previous interactions with us, we've always been able to resolve issues quickly. Could you please provide more details about the specific issue?

Rest assured, I'll prioritize your issue and we'll have you taken care of right away.

Best regards,
Support Team"
```

#### Step 6: Save to Conversation History
```
Database Insert Node:

INSERT INTO conversation_history (
  user_id,
  message,
  response,
  timestamp,
  status,
  resolution_time_started
) VALUES (
  '{{ $json.user_id }}',
  '{{ $json.message }}',
  '{{ $node["OpenAI"].json.choices[0].message.content }}',
  NOW(),
  'pending',
  NOW()
)

Also update:
UPDATE customers
SET 
  last_interaction_date = NOW(),
  interaction_count = interaction_count + 1
WHERE user_id = '{{ $json.user_id }}'
```

#### Step 7: Send Response
```
Gmail/Email Node:

To: john@example.com
From: support@mycompany.com
Subject: Re: Your Recent Issue - Order #ORD-2026-456

Body: {{ $node["OpenAI"].json.choices[0].message.content }}

CC: support@mycompany.com

Also log to Slack:
Slack Message:
📧 New support ticket from Gold customer John Doe
Issue: {{ $json.message }}
Response sent with personalization
Links to conversation history included
```

---

## Error Handling & Advanced Features

### Try-Catch Pattern

```
WORKFLOW:

Risky operation (e.g., API call)
   ↓
IF successful:
   └─ Continue normal flow
   ELSE (if error):
   └─ Catch error node
   └─ Log error details
   └─ Send alert
   └─ Retry or escalate
```

### Example Error Handling

```
Node: HTTP Request (external API)

Configuration:
├─ URL: https://api.unreliable-service.com/data
├─ Timeout: 10 seconds
└─ Retry: 3 times

If fails:

1. First try fail:
   └─ Wait 5 seconds
   └─ Retry (2nd attempt)

2. Second try fail:
   └─ Wait 10 seconds
   └─ Retry (3rd attempt)

3. Third try fail:
   └─ Error node triggered
   ├─ Log error: "Service unreachable after 3 attempts"
   ├─ Send Slack alert: "API Down"
   ├─ Save to database: "Failed request timestamp"
   └─ Send automated email to customer:
      "Currently experiencing issues, will retry soon"

If success before timeout:
   └─ Continue normal flow
   └─ Log: "Success on attempt #X"
```

### Logging & Debugging

```
VIEW EXECUTIONS:
1. n8n Dashboard
2. Click "Executions" tab
3. See all past runs
4. Click any execution to see details

EXECUTION DETAILS:
├─ Execution status: Success / Failed / Running
├─ Start time
├─ End time
├─ Duration
├─ Node-by-node breakdown
│  ├─ Node name
│  ├─ Status
│  ├─ Input data
│  ├─ Output data
│  └─ Error message (if failed)
└─ Full logs

DEBUGGING TIPS:
1. Check each node output:
   └─ Click node → See input/output data
   
2. Add Set nodes to inspect data:
   └─ Pass through data to verify structure
   
3. Use Test button:
   └─ Test individual nodes without running whole workflow
   
4. Check error messages:
   └─ Specific details about what failed
```

---

## Best Practices

### ✅ DO:

1. **Name your nodes clearly**
   ```
   Good:   "Get Customer Data from DB"
   Bad:    "Node1"
   ```

2. **Use Set nodes for data transformation**
   ```
   Instead of complex expressions everywhere,
   use Set nodes to prepare clean data
   ```

3. **Add error handling**
   ```
   Every API call should have error handling:
   ├─ IF success → Continue
   └─ IF error → Log & alert
   ```

4. **Test with real data**
   ```
   Use the Test button to verify with actual data
   before activating workflows
   ```

5. **Document your workflows**
   ```
   Add workflow notes:
   - What it does
   - When it triggers
   - Expected results
   - Contact person for support
   ```

6. **Use environment variables**
   ```
   Store sensitive data as environment variables:
   - API keys
   - Database credentials
   - Email addresses
   
   Reference: $env.VARIABLE_NAME
   ```

7. **Monitor costs**
   ```
   For cloud services (email, API calls):
   - Track execution counts
   - Estimate monthly costs
   - Optimize unnecessary executions
   ```

### ❌ DON'T:

1. **Don't hardcode secrets**
   ```
   Never put API keys directly in nodes
   Use environment variables instead
   ```

2. **Don't ignore errors**
   ```
   Always add error handling
   Log failures for debugging
   ```

3. **Don't create infinite loops**
   ```
   Be careful with loops:
   - Set exit conditions
   - Limit iterations
   - Test before activating
   ```

4. **Don't over-complicate workflows**
   ```
   If a workflow gets too complex:
   - Break into multiple workflows
   - Use clearer node names
   - Add intermediate Set nodes
   ```

5. **Don't forget to save**
   ```
   Save frequently while building
   Use version control if available
   ```

---

## Troubleshooting Guide

### Common Issues & Solutions

#### Issue: Webhook Not Receiving Data

```
Problem: Form submission → n8n webhook not triggering

Cause: Usually incorrect URL or CORS issues

Solutions:
1. Verify webhook URL matches exactly
   └─ Compare character by character
   
2. Test with curl:
   curl -X POST https://n8n.io/webhook/abc123 \
     -H "Content-Type: application/json" \
     -d '{"test":"data"}'
   
3. Check n8n logs:
   └─ Look for incoming requests
   
4. Verify webhook is active:
   └─ Toggle off/on

If still not working:
├─ Check firewall rules
├─ Verify external system can reach n8n
└─ Contact hosting provider if n8n is behind firewall
```

#### Issue: Data Disappeared Between Nodes

```
Problem: Data from Node A not available in Node B

Cause: Data reference issue or node not connected

Solutions:
1. Verify nodes are connected:
   └─ Check connection line exists
   
2. Check data structure:
   └─ Click previous node → See output data
   └─ Verify field names match
   
3. Use correct reference syntax:
   └─ {{ $json.fieldname }}  (Current node)
   └─ {{ $node["Node Name"].json.fieldname }}  (Other node)
   
4. Add Set node to debug:
   └─ Extract fields explicitly
   └─ See if data flows through
```

#### Issue: "Authorization Failed" Error

```
Problem: API calls failing with auth error

Causes:
• API key expired
• API key has wrong permissions
• Wrong authentication type
• Headers missing

Solutions:
1. Verify API key is correct:
   └─ Copy from service provider
   └─ Check expiration date
   
2. Check authentication method:
   └─ Is it Bearer token, API key, or Basic auth?
   └─ Verify format matches API docs
   
3. Test API key directly:
   curl -H "Authorization: Bearer YOUR_KEY" \
        https://api.example.com/test
   
4. Check permissions:
   └─ Does key have required scopes?
   └─ Generate new key with full permissions
```

#### Issue: Workflow Runs but No Output

```
Problem: Workflow executes successfully but no result

Cause: Usually node not configured to send output

Solutions:
1. Add Response node:
   └─ If using webhook, must have Response node
   
2. Check last node is output:
   └─ Email, Slack, Response node, etc.
   
3. Verify Response node configuration:
   └─ Status code should be 200
   └─ Response body should be populated
   
4. Add debug Set node:
   └─ Before Response node
   └─ Verify data is flowing through
```

---

## Quick Reference

### Common Node Configurations

**Webhook (Trigger)**
```
HTTP Method: POST
URL: [Auto-generated]
Auth: None (or add as needed)
```

**HTTP Request (API Call)**
```
Method: GET/POST/PUT/DELETE
URL: https://api.example.com/endpoint
Headers: Content-Type, Authorization
Body: JSON data (if POST)
```

**Gmail (Send Email)**
```
To: recipient@example.com
Subject: Email subject
Text: Email body (can use {{ $json.field }})
```

**Set (Transform Data)**
```
key1: value1
key2: {{ $json.sourceField }}
key3: {{ $node["NodeName"].json.data }}
```

**IF/ELSE (Conditional)**
```
Condition: {{ $json.amount }} > 100
[TRUE path]
[FALSE path]
```

**Loop (Iterate)**
```
Input: Array of items
Process: Same nodes for each item
Output: All items processed
```

---

## Conclusion

You now have a complete understanding of **n8n**:

✅ What it is and why to use it
✅ How to set it up
✅ Understand all node types
✅ Build simple to complex workflows
✅ Implement memory and learning
✅ Handle errors gracefully
✅ Best practices and troubleshooting

### Next Steps:

1. Set up n8n (cloud or self-hosted)
2. Build first simple workflow
3. Test with real data
4. Gradually add complexity
5. Deploy to production
6. Monitor and optimize

**Start building automation today!** 🚀

---

Document Version: 1.0
Last Updated: March 27, 2026
Difficulty Level: Beginner to Intermediate
Total Reading Time: 90-120 minutes
Hands-On Examples: 4 complete workflows + 4 patterns
