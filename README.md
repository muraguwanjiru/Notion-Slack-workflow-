 # Notion-to-Slack Task Reminder Automation (n8n Workflow)

An automated, serverless-ready workflow built on n8n that queries a Notion task database and pushes dynamic daily notifications straight to a target Slack workspace. This system ensures actionable visibility over outstanding items without requiring users to log into their project management dashboard manually.


##  Project Overview

Managing operational tracking systems often breaks down when team members forget to check active project boards. This pipeline resolves manual notification gaps by introducing an automated orchestration layer between **Notion** and **Slack**. 

Every morning at a designated hour, the engine triggers, fetches uncompleted rows, maps relational properties, and relays personalized messaging items down the communication delivery pipe.

### Key Architecture Components
* **Polling & Orchestration Platform:** n8n Cloud
* **Data Source Layer:** Notion API (Custom Internal Integration)
* **Delivery Endpoint:** Slack 


##  Detailed Workflow Architecture

The automation relies on an explicit sequence of structured node operations to handle formatting maps and prevent application memory leaks:

1. Schedule Trigger (Daily 08:00 AM):
   Acts as the system heartbeat. Fires an immediate downstream signal exactly at 8:00 AM local time daily to kick off the query lifecycle.
2. Notion Node (Get Many Database Pages): 
   Authenticates securely using a server-side Access Token. Connects to the primary **To Do List** workspace view to retrieve live data arrays.
3. Array Processing Loop (Implicit Automation): 
   n8n handles multiple data items out-of-the-box by splitting the structural payload into individual row streams, running the remaining nodes consecutively for every discovered task.
4. Slack Node (Post a message):
   Extracts dynamic values from the item array using structured syntax layouts and directly publishes target payloads into a localized private user workspace or team communication channel.


## Canvas Blueprint

Data streams sequentially through the canvas components as displayed below:

 Schedule Trigger  --->     Notion Node     --->  Slack Node     (Every Day 8AM  Get Task Pages) ----->Post Message 

##  Technical Configuration & Property Mapping

### Notion Database Schema
The workflow looks for specific underlying metadata columns. Ensure your data workspace contains the following parameters:
* Primary Key Target:** Task name (Title Property Class)

### n8n Dynamic Expression Syntax
To ensure messages don't output abstract static string indicators, the Slack message body parameters leverage JavaScript bracket-notation object keys to cleanly query multi-layered JSON responses from Notion:


Task Reminder: {{ \$json.properties['Task name'].title.plain_text }}

