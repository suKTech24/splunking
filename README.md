# Splunk Core Certified User


---
<details>
  <summary> Module 1 : Splunk Basics </summary>

- What is Splunk?
- Basic Splunk Components
    - Processing Components
        - Forwarders, Indexers, Search Heads
    - Management Components 
        - Deployment server
        - Indexer Cluser Manager
        - Search head cluster deployer
        - License Manager
        - Monitoring Console

- Splunk Components
    - Splunk Forwarders
        - Universal forwarders ( for prods)
            - Separate executable with reduced functionality
            - Main function is to collect and send data
        - Heavy forwarders
            - Configure from full Splunk enterprise installation.
            - Can parse and filter data before forwarding.

    - Splunk Indexers (Search Peer)
        - It is a splunk enterprise instance that processes and writes data into repositories as events
        - Indexers can do processing
            - Transform raw data into events (parsing)
            - NOTE: Heavy forwarders can also parse data as well.
            - Assign metada - source, sourcetype (json, csv, etc), host (host machine that is actually sending the data to the Splunk)
            - Identify or create timestamps
            - After all the processing is done, indexers will write data to data repositories known as indexes in disk.
            - Default indexes
                - Main
                - _internal - Splunk own logs
            - Repositories containing files with index data are called buckets.
            - Example index structure

            ```
            Repositories
            Home Path
                Hot Bucket - data is actively ingested into hot bucket. Write only happen in Hot Bucket.
                Warm Bucket
            Cold Path
                Cold Bucket - Retention. If reach over the retention period, data will be frozen. 
            Thawed Path
                Frozen to thawed buckets
            ```
        - Indexer Cluster
            - Group indexers together to provide data replication
            - Cluster Manager coordinates replication activities and manages the Cluster
    - **Exam Tips**
        - Splunk components that transforms raw data into events.
            - Indexers
            - Heavy forwarders
        - Splunk components that saves data into disk
            - ONLY indexers can write to Hot Bucket disk
        - Licensing meter runs during indexing

 - Search Head
    - Allow users to write search queries (SPL) to search the indexed data
    - Distributes search requests to the indexers and merges the result back to the user
    - Extract fields and create other knowledge objects such as 
        - Reports
        - Alerts
        - Visualizations
        - Dashboards
    
    - Search Head Cluster
        - Group search heads with identical configuration
        - Search requests from users are balanced across Search Head (SH) group - load balancing
        - Managed by a Cluster Captain
            - Coordinates job scheduling among SH members
            - Coordinates replication activities
        - Cluster Deployer
            - This is a management component that distributes apps and other configurations to Cluster members
            - Distributes content, configuration, apps to other groups of Splunk instances (deployment clients)
            - Distributed content is known as deployment apps
            - Used mostly distribute apps to Splunk Forwarders
    - **Exam Tips**
        - Splunk component that let users write SPL queries ==> Search Head

- Forwarder Management
    - Deployment server GUI accessible within Splunk Web
    - Provides a way to configure deployment server and monitor updates
- License Manager
    - Hosts licenses and assigns license volumne to other Splunk Components (License peers) in a distributed deployment
    - License meter runs during indexing
    - License Types:
        - Volumne based
        - Infrastructure based
        - Access to Splunk features
- Monitoring Console
    - Used to view topology and performance information about your Splunk deployment
    - Monitor dashboards, use data from Splunk internal logs

- Splunk Web User Interface 
    - Access Splunk Web UI using a browser
    - Default Splunk Enterprise port is 8000
    - Local Machine : http://localhost:8000
    - Remote Instance (VM) : http://<instanceIP address>:8000
    - Provides access to Splunk features
        - Available features depend on role of user
        - Three main out of the box roles
            - User
            - Power
            - Admin 
    - Includes apps to extend functionality
        - Default App examples:
            - Home App
            - Search & Reporting App
        - Create Custom apps
        - Download apps from Splunkbase

    - **Exam Tips**
        - Default port of Splunk web ==> 8000
        - Splunk default app examples 
            - Home App
            - Search & Reporting App

- Splunk Apps
    - Splunk Apps are custom solutions that allow you to extend the functionality of the Splunk platform
    - What can Splunk app do?
        - Separate workspaces for different use cases to co-exist on single Splunk instance
            - Alerts
            - Reports
            - Dashboards
        - Custom configurations to ingest data
        - Collections of 
            - Data inputs
            - UI elements
            - Knowledge objects - fields extraction
    - Where to find apps?
        - Browse to find apps within Splunk Enterprise
        - Splunkbase, https://splunkbase.splunk.com/
    - **Exam Tips**
        - What are the use cases of Splunk apps?
        - Access Splunk apps in Splunkbase

- Splunkbase
    - Download eventgen

- Settings
    - Knowledge
        - Create and manage knowledge objects
        - Major menu items available to user and power roles
    - System
        - System settings
        - Licensing
        - Restart Splunk from GUI
    - Data
        - Create indexes and configure data inputs
        - Configure data forwarding and receiving
    - Distributed environment
        - Indexer clustering
        - Forwarder management
        - Data Fabric
        - Federated search
        - Distributed search 
    - Exam tip
        - What can be changed using account settings and preferences?
            - full name, email, password, timezone, background screen, etc.

- Search & Reporting App
    - Default app that provides an interface to search, analyze and vistualize data in Splunk
    - Search Bar - 
    - App Navigation Bar
    - Timerange
    - Search modes
        - fast mode
        - smart mode
        - verbose mode - least performance
    - Search history
    - Data summary
        - Use the Data Summary tab to quickly learn about the data present in your Splunk deployment
            - View count of events by :
                - Hosts
                - Sources
                - SourceTypes
    - Exam Tips
        - Quick way to understand your data in your deployment.
        - Fields present under data summary 
- Splunk Roles and Users
    - Roles 
        - admin
            - Access to all settings
            - can_delete
        - power
            - Have limited access to settings
            - Create and publish (share) knowledge objects
            - Assign to power users
        - splunk_system_role
        - user
            - Limited access to settings
            - Create private knowledge objects
            - Assign to basic users
    - Exam Tips
        - Role permissions. Which roles have minimum and maximum permissions
        - How many main roles in Splunk by default
            - min roles are user, power, admin
    - Question
        - Q1: Which of the following Splunk components typically resides on machines where data originates?
            - Forwarders are installed on host machines to collect data and send to Splunk for indexing.
        - Q2: Which Splunk component transforms raw data into events and distributes the results to an index?
            -  Indexer is the Splunk component that processes and writes data into repositories (indexes) as events.
        - Q3: Which component of Splunk is primarily responsible for saving data?
            - Indexer is the Splunk component that processes and writes data (saves data) into repositories (indexes) as events.
        - Q4: Three basic components of Splunk are?
            - Basic components are the processing components - Forwarder, Indexer, Search Head
        - Q5: What is Splunk?
            - Splunk is a software platform to search, analyze and vistualize the machine-generated data
        - Q6: Which component of Splunk let us write SPL query to find the required data?
            -  The Search Head allows users to write search queries using Splunk Search Processing Language (SPL) to search indexed data.
        - Q7: Which of the following Splunk Components can perform log filtering/parsing?
            - While universal forwarders can only collect and send data, heavy forwarders can parse and filter data.
        - Q8: Which of the following is true about user account settings and preferences?
            - You can configure Full name, Time zone and Default app under account settings and preferences in the account menu.
        - Q9: A collection of items containing things such as data inputs, UI elements, and knowledge objects is known as what?
            - Apps are collections of data inputs, UI elements, and knowledge objects.
        - Q10: Splunk Apps are used for the following:
            - 
        - Q11: Which is a default app for Splunk Enterprise?
            - Splunk comes out-of-the box with default apps such as Home App, Search & Reporting App.
        - Q12: How many main roles do you have in Splunk?
            - Splunk comes out-of-the box with 3 main roles: User, Power, Admin
        - Q13: What is the default web port used by Splunk?
            - Default port to access Splunk Web UI is 8000.

- Useful references
    - https://www.aplura.com/splunk-best-practices/
    - https://medium.com/@byanalytixlabs/understanding-the-splunk-architecture-key-components-and-best-practices-7f6161762328
</details>

---

<details>
  <summary> Module 2 : Getting Data into Splunk </summary>

- Ways to ingest data into Splunk
    - What data to ingest into Splunk?
        - Get data from files and directories
            - Monitor files and directories
            - Upload static files
        - Get data from network sources
            - Data that come over a network port
            - Both TCP and UDP protocols are supported
        - Get data from window sources
            - Window event logs
            - windows registry
            - Windows management instrumentation (WMI)
            - Active directory
            - Performance Monitoring
        - Get data from other sources
            - API
            - DB
            - Metrics
            - FIFO queues

    - How to ingest data into splunk
        - Use existing apps and add-ons: First check, if there is an existing add-ons
            - e.g. Splunk add-on for windows
            - Splunk add-on for AWS
            - Splunk DB connect
            - Splunk Stream
        - Find apps and add-ons on Splunkbase
        - Use forwarders to get data
            - install forwarders on the sources generating data.
            - Use Heavy Forwarders if more processing is needed before ingestion
        - Use HTTP event collector (HEC)
            - Use HEC to get data from source via HTTP or HTTPs protocol
        - For custom data, use scripted or module inputs

- Splunk index time process - end of end process consisting of three phases
    - Input Phase
        - Handled at the data source
            - Universal forwarder
            - HF
        - data sources are open and read
        - COnfigurations are applied to entire streams
        - data sent out for indexing
    - Parsing Phase
        - Handled at :
            - indexer
            - heavy forwarder
        - data is broken up into events
        - Extract defaul metadata fields
            - host
            - source
            - sourcetype
            - index ( defaults to main )
        - Identify and create timestamps
        - Identify line termination
    - Indexing Phase
        - Handled at : 
            - indexer
        - Run license meter
        - Build index data structures
        - Write data to disk

- Configuring data inputs
    - Add data inputs using one of the followin methods
        - Splunk Web
        - CLI
        - Config files - edit inputs.conf
        - Apps and add-ons from Splunkbase
    - Add data inputs using Splunk Web
        - Upload
            - Upload local files from your computer
            - Only get indexed once
        - Monitor
            - Monitor files and directories, network ports, etc.
            - Data located on Splunk enterprise instances
            - Useful for testing
        - Forward
            - Get data from remote machines over receiving port
            - Remote machines have forwarders installed
            - Mostly used in production environments
    
- Configuring data inputs - upload
    - select data source - file containing data to index
    - select a matching sourcetype from list of pretrained sourcetypes
        - sourcetype determined automatically but you can choose a different one from the dropdown.
        - you can also create a new sourcetype name
    
    - Input settings
        - Assing metadata values
        - Pick an index you want to place the data in
        - Review 
    - Data sources are from splunk
        - webserver 1, 2, 3
            - access.log, secure.log
        - localhost
            - Eventgen app, eventgen.conf
        - local host

- Adding training data - generate events

|Operating System| Default Splunk installation directory | Directory for app config files |
|---|---|---|
|Windows|C:\Program Files|Splunk|C:\Program files|Splunk\etc\apps|
|Linux|/opt/splunk|/opt/splunk/etc/apps|
|Mac OS|/Application/Splunk|/Application/Splunk/etc/apps|
- Adding training data - Overview
- Adding Training data - upload files
- Adding training data - Generating events

- **Quiz** - TB Added

</details>

---

<details>
  <summary> Module 3 :  Basic Searching in Splunk</summary>

- **Overview of Search & Reporting App**
    - New Search, fields, mode, job, etc.
- **Search with Keywords and Phrases**
    - Use keywords and phrases to retrieve matched events from the index
    - `index=main sourcetype=eventgen`
    - Match is performed against raw events in the _raw field.
    - To search matching phrases, use "double quotes" , "user ubuntu"
    - Scenario 1: Search events that match the following keywords for all time. Check which index(es) these events belong to.
        - invalid
        - amanda
        - Macintosh
        - telco01
    
    - Scenario 2 : Search events that match the following quoted phrase for all time. Check which index(es) these events belog to.
        - "user ubuntu"
        - "failed password"
        - "like gecko"
        - "Mac OS"
- **Use Wildcards**
  - Best practice, use Wildcards at the end of a term, e.g. pass*, fail*
  - Avoid using wildcards in the following situations:
    - Beginning of a string - *fail, *word
        - ==> search will look at every string, i.e., scan all events.
        - ==> can cause performance issues
    - Middle of a string - http*buttercupgames.com
        - ==> might cause inconsistent results especially in strings containing punctuation.

    - Scenario:
        - Search events that match the following terms with wildcards for all time. Compare execution times.
            - fail* with *fail
            - pass* with *word
            - http://www.buttercupgames.com with http*buttercupgames.com
        - Check for time taken --> Job --> Inspect Job
    - Exam tips : placement of wildcards in the search terms
- **Use boolean expressions (AND, OR, NOT operators)**
    - Boolean operators must be in uppercase
    - AND operator is implied between terms. Do not need to be explicitly specified.
        - Search for **failed passord** is the same as **failed AND password**
        - Not operators applies tot he term immediately following NOT
            - **user NOT administrator** ==> Search events that contain the word user and does not contain the word administrator
    - Scenario
        - Search events that match the following terms with Boolean operators for all time
            - failed password == failed AND password
            - invalid or macintosh
            - (www1 or www2) user amanda == (www1 or www2) AND user AND amanda
    - Exam tips
        - Which boolean operator is implied.
        - How to combine search terms with Boolean operators
        - Booleans in uppercase
    - Use Search Assistant - helps with writing searches by providing selections to complete search strings:
        - Marching terms in indexed data
        - Matching searches based on recent search history
        - Shows list of commands after first pipe (|)
        - You can select a term from the list to add to the search
        - Mouse over a command to get more info about the command
        - Search assistant also provides guidance to match parenthesis as you type.
            - When end parenthesis is typed, correspoinding beginning parenthesis is highlighted.
        - Search assistant is enabled by default, but can be disabled. Three modes:
            - full mode
                - Additionally displays count of how many times a term appears in indexed data.
                - Can be toggled using "Auto Open" option
            - compact mode - default
            - None (disable)
    - Scenario
        - Verify that the default search assistant mode is Compact.
        - Type the following keywords on the search bar to vertify search assistant:
            - Use - check for matching terms in indexed data.
            - (www1 - check for matching searches run rcently
                - select a recent search with parenthesis. Verify matching start parenthesis
            - telco01 | ==> check for commands after the pipe.
                - Mouse over a command to get information.
        - Change the search assistant mode to Full and verify that count of terms for search above.
        - Use the Auto Open option to toggle Full mode
        - Disable search assistant and verify that there are no selections provided for searches.

- **Use Search Assistant**
    - Search assistant helps with writing searches by providing selections to complete search strings.
    - You can select a term from the list to add to the search.
    - Mouse over a command to get more info about the command.
    - Search assistant is enabled by default but can be disabled. Three modes : 
        - Compact (default)
        - Full - get more info than compact mode.
        - None (disable)
    - Pipe character ==> you want command right after | 
    - e.g. `telco01 | stats count`

- **Identify Contents of search results**
    - timestamp
    - Splunk also extracts metadata fields at index time
        - host
        - source
        - sourcetype
        - index
    - Selected fields 
    - Terms that match the search are highlighted in search results.
    - When you click an item in the search results, you can drilldown to the following:
        - Add to search
        - Exclude from search
        - New search
    - Exam tips
        - Order of search results is reverse chronological order
        - Actions when clicking item on search results
        - Search result display options ==> raw, list, table
        - Metadata fields
- **Setting search time range**
    - Presets
        - real time
        - relative (historical)
        - other
    - Default time picker selection is last 24 hours
    - Time modifiers
        - earliest - `-24@h`
        - latest - `now`
        - It will overwrites the time range picker value
    - Relative time examples
        - earliest =-24h latest=now
        - earliest=-24h@h latest=now
    - Absolute time example
        - earliest=09/03/2024:00:00:00 latest=09/04/2023:23:00:00
        - s seconds
        - m minutes
        - d days
        - h hours
        - w weeks
        - mon months
        - y years
    - Snapping always rounds down to the nearest time unit specified 
        - If current time is 10:42:07, -4hr@h looks back to 06:00:00
        - If current time is 15:38:12, -30m@h looks back to 15:00:00 
    - Exam Tips
        - What UI component that allows for time selection - time range picker
        - setting time range using earliest and latest
        - time range picker options
            - presets, relative, real time, date range, date and time range, advanced
        - time unit abbreviations
            - s, m, d, h, w, mon, y
        - Difference between real-time and relative time   
            - real time vs historial 

- **Events Timeline**
    - 

- **Manage Search Jobs**
    - 

- **View Search History**
    - 

</details>

---

<details>
  <summary> Module 4 :  </summary>


</details>

---

<details>
  <summary> Module 5 :  </summary>


</details>

---

<details>
  <summary> Module 6 :  </summary>


</details>

---

<details>
  <summary> Module 7 :  </summary>


</details>

---

<details>
  <summary> Module 8 :  </summary>


</details>

---

<details>
  <summary> Module 9 :  </summary>


</details>

---

