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
    - earliest=-7d@d latest=now
    - earliest=-7d@d latest=0d
    - host01 OR host09 earliest=02/01/2025:05:00:00 latest=02/01/2025:14:00:00

- **Events Timeline**
    - Bin size (scale) of the timeline is shown on the legend
    - Formatting timeline
        - Hidden - hids the timeline
        - Compact - no labels on axis
        - Full
        - Linear scale
        - Log scale 

    - Zoom options
        - Zoom out 
            - Increases the size of the time bin in the legend. Re-executes the search 
        - Zoom to selection
            - Select a few bars and click `zoom to selection` to zoom in.
            - Decreases the size of bin
            - Re-executes the search
        - Deselect 
            - Cancel a selection 
    - Exam tips
        - Function of events timeline
        - Using click and drag on timeline
        - Timeline controls: Format, zoom out, zoom to selection, Deselect

- **Manage Search Jobs**
    - Every search you run is a job and generates a job Id
    - Job menu 
        - Change job settings
        - Send job to background
        - Inspect job 
        - Delete job 
    - Pause/Resume job
        - Pause a job while it's running and resume to finalize 
    - Stop job 
        - Will generate partial results
    - Share job 
        - Provides a link to bookmark or copy/share job
        - Extend retention of results to 7 days from default of 10 mins.
        - Give read permissions to everyone.
    - Export job 
        - Export search results as raw events (text file), CSV, XML, json
        - After using a transforming command, you no longer have raw events. ONLY CSV, XML, JSON available
    - Print job 
        - Print results or save as PDF 

    - Edit Job settings
        - permissions
            - by default, only owner can view the job (private).
            - When you share job link, read access is provided to everyone 
        - lifetime 
            - default job lifetime is 10mins.
            - When you share job link, lifetime is automatically extended to 7 days.
            - To keep results longer, save job as a report. 
    - Access saved Jobs
        - Activity -> Jobs
        - Show jobs run within last 10 mins (default)
        - Show jobs with lifetime extended to 7 days
        - To view jobs results, click on job link 
    - Exam tips 
        - default time to retain search job - 10 mins 
        - how to keep search results longer than 7 days - save the job as report 
        - What can you configure with job settings menu?
            - permission, job lifetime
        - Job details on activity menu 
        - 

- **View Search History**
    - Contains a list of most recently run ad-hoc searches
    - Use filter to find specific previously run searches
    - By default, contains 20 searches per page
    - Use time filter to set the Timerange
    - Use Add to search to run a previously run search 


</details>

---

<details>
  <summary> Module 4 :  Using fields in Searches</summary>

- **What are fields?**
    - Fields are searchable name/value pairs in your event data.
    - Searches using fields are more efficient than searches using keywords or quoted phrases
    - Fields can be extracted from data at index time and at search time
        - Index-time extractions
            - metadata fields : host, source, sourcetype, index.
            - Internal fields : _time, _raw, etc.
            - Custom Fields
        - Search-time extractions
            - Field discovery
                - automatically discover fields based on sourcetype and name/value pairs in your data
                - Enabled by default
                - In Fast mode, field discovery is disabled. You will see fields that are extracted at index time.
            - Custom fields
            - Ad-hoc search
    - Most data vendors have documentation for field name/value mappings that can be used to define extractions in Splunk 

    - Demo 
        - Run the query ==> "index=web sourcetype=access_combined" for all time
        - Identify metadata fields host, source, sourcetype, index and internal fields _time, _raw
        - Change search mode to Fast to disable field discovery. Revert to re-enable field discovery 
        - Identify data-specific fields for clientip, categortyId, status
    - Exam Tips:
        - Describe field discovery
        - Understand index and search time fields
        - Metadata fields
        - Internal fields 

        ```
            index=web sourcetype=access_combined
            | table _time, _raw
        ```

- **Using the Fields sidebar** 
    - Fields sidebar displays fields discovered in your events.
    - Fields groupings
        - Selected Fields
        - Interesting fields
    - Selected fields
        - By default, selected fields are host, source and sourcetype 
        - Can be configured to add/remove fields
        - Listed under every event.
    - Interesting Fields
        - Fields that appears in at least 20% of your events.
        - Can making Interesting Field as a selected field and vice versa 
    - All fields
        - Use this to see all fields in events
        - Will also include fields that appear in less than 20% of Events
    - Field characteristics 
        - If starts with #, it is numeric fields
        - If starts with a, it is Alphanumeric fields
        - If you see numbers next to the fields, it counts the unique values 
    - To make any field as a selected field:
        - Click on "All Fields"
        - Click the checkbox to the left of the field you want
        - FIeld will now show up in Selected fields list 
    - Field Window Shows   
        - Top 10 values of the field by count and percentage
        - Reports 
            - top values
            - top values by time - timechart of top values 
            - rare values - stats and Visualizations of bottom 20 values
            - Events with field - all events containing this field 
        - If field is an interesting field, click "Yes" to make it a selected field 
    - Demo 
        - Run the query "index=web sourcetype=access_combined" for All time 
        - Identify selected fields and confirm they show up under each event
        - Change JSESSIONID field from an interesting field to a selected field
        - Revert JSESSIONID to an interesting field. Make it a selected field using the "All Fields" option.
        - Identify numeric and Alphanumeric fields on the fields sidebar 
        - Click on productid field to check top 10 values. Open each report associated with this field 
        - Click on the numeric field status and confirm/vertify the following 3 additional reports:
            - Average over time 
            - Maximum value over time 
            - Minimum value over time 
    - Exam Tips 
        - Add fields to the field sidebar
        - Numeric, Alphanumeric fields, count of unique values
        - Default selected fields
        - Reports in field window 

- **Using fields in searches**
    - Search syntax is <field_name>=<field_value>
    - Using fields to search is more efficient than using keywords and quoted strings 
        - Use quotation marks for field names with spaces
        - `index=web fullName="Jane Austin"`
        - Case Sensitivity
            - fields names are case sensitive
                - `index=web action=addtocart`
                - `index=web Action=addtocart`
            - fields values not NOT case sensitive
                - `index=web action=addtocart`
                - `index=web action=ADDTOCART`
        - You can use wildcards with fields
            - `index=web action=addtocart JSESSION=SD2*`
        - You can use Boolean operators AND, OR, NOT with Fields
            - spce between is NOT
            - `index=main sourcetype="eventgen" (nodeName=host05 OR nodeName=host06) NOT partner=Telco04`
        - !, !=, >, < , <=, >=
    - Wildcards 
        - Use wildcards to match an unlimited number of characters in a field value
        - Wildcards can be used at the start, Middle and end of a field value 
        - Best practices
            - Avoid using wildcards at the beginning - all events will be scanned causing performance issues
            - Avoid using wildcards in the middle - will cause inconsistent results 
    - For fields with IP addresses, you can search with CIDR format 
        - Specify network IP and subnet mask : userIPAddress="192.168.180.0/24"
        - `index=main sourcetype=eventgen userIPAddress="192.168.180.0/24"`
    - Exam tips
        - Case Sensitivity of field names and values 
    - Demo
        - Run this query `index=main sourcetype=eventgen partner=telco04` for last 60 mins
        - To verify case Sensitivity, search with 
            - PARTNER=telco04 - Notice no results generated.
            - partner=TELCO04 - Notice results generated 
        - Using wildcards, find all numbers starting with 710 and all response codes starting with 4
        - Narrow the search down to all /24 IP addresses starting with 192.168.143 using:
            - Wildcards 
            - CIDR notation 

- **Boolean Operators** 
    - AND operator is implied.
    - Boolean operators are always uppercase. Narrow down the searches and improve performance
        - `index=web sourcetype=access_combined (host=Webserver1 OR host=Webserver2) NOT action=remove`
        - `index=web AND sourcetype=access_combined AND (host=Webserver1 OR host=Webserver2) NOT action=remove`
    - Exam Tips 
        - Which boolean operator is implied
        - Case of boolean operators 
        - Searches using boolean operators 
    - Demo 
        - Run the query `index=web sourcetype=access_combined` for last ALL Time 
        - Retrieve only events from Webserver1 and Webserver2
        - Exclude events that have action field value equal remove 
        - Insert AND operator in the query and verify results are the same 

- **Comparison Operators** 
    - Demo 
        - Run the query `index=web sourcetype=access_combined` for last ALL time 
        - Retrieve only events from webserver1 and Webserver2
        - Events having number of bytes greater than or equal to 3000
        - Exclude events with action field value of remove 
        - Events with status > 200 < 500

- **Difference between != and NOT** 
    - Both operators can be used to exclude events from your search 
    - In practice, they can produce different results. Example:
        - NOT will search : 
            - All events where action field exists, and value is different from remove 
            - All events where action field does not exist 
        - != will only search 
            - All events where action field exists, and value is differen from remove 
- **Search modes**
    - Fast mode
        - Best performance, speed over completeness
        - Field discovery disabled
        - No event list when using transforming commands 
    - Smart mode (default)
        - Balance speed and completeness
        - Field discovery is enabled
        - Behaves like fast mode when using transforming commands
    - Verbose Mode 
        - More data, least performance, completeness over speed
        - FIeld discovery is enabled
        - Shows event list when using tranforming commands

- **Search best practices** 
    - Specify indexes at the beginning of the search string 
        - can search without indexes but it is more efficient when specify them 
        - Examples 
            - index=main 
            - `index=web or index=security`
    - Avoid using wildcards at the beginning or middle of your search string, use * at the end
    - Use OR instead of wildcards when possible 
        - `process=su OR process=sudo`
    - Better to use inclusion than exclusion 
        - Inclusion : action=addtocart
        - Exclusion : NOT action=addtocart
    - Include as many search terms as possible to narrow down your results
    - Specify time to narrow down the results of your search. This is the most efficient filter 
    - Make your search terms as specific as possible
        - search for `Jane Austin`, inseat of `Jane`
    - Use filters as early as possible, eg. index=, sourcetype=, etc

</details>

---

<details>
  <summary> Module 5 : Search Language Fundamentals </summary>

- **Search language components, syntax and pipeline**
    - Search terms - basic search 
    - Apply search terms to retrieve data from the index(s)
        - keywrods, phrases, wildcards, booleans, etc.
    - Apply commands to events retrieved by Search Terms
        - Commands 
            - specifies what to do with results retrieved
            - Calculat statistics, generate charts, evaluate new fields, etc.
        - functions
            - Defines how to perform a task required by the command
            - Function arguments provide the variables needed for the function to work 
        - arguments
            - variables needed for the command to work 
            - Example: Command arguments can limit the number of results 
        - Clauses
            - Group or rename fields in your results 
    - A series of commands can be applied to data retrieved from the index 
        - Commands separated by pipe | character 
        - Next command applied to intermediate results by previous command
        - This is known as the search pipeline 
    - Example 
        - `index=main sourcetype=eventgen | eval callResult=if(responseCode==200, "Success", "Failure") | stats count BY callResult | rename callResult AS finalResult`
        - Clauses
            - BY callResult 
            - AS finalResult
        - Function arguments
            - responseCode == 200, "Success", "Failure"
        
- **Search pipeline readability**
    - Change the search bar theme - Preferences -> SPL Editor -> Themes 
        - Light Theme 
        - Dark theme 
        - Black on White
    - Activate search auto-format 
        - When enabled, each pipe character appears on a Separate line. This improves readability.
    - Add line numbers 
        - Line numbers will show next to each line in the search pipeline
    - Commands are in BLUE - eval, top, rename
    - Functions are in Purple - if, count 
    - Booleans and Clauses (command modifiers) are in Orange - AND, OR, NOT 
    - Command arguments are in Green - limit , span 

    ```
        index=main sourcetype=eventgen (nodeName=host01 OR nodeName=host02) NOT partner=Telco07 
        | eval CallResult=if(responseCode==200, "Success", "Failure")
        | top limit=0 CallResult
        | rename CallResult AS finalResult
    ```
- **Fields command**
    - Use the fields command to filter list of fields returned in search results
    - NOte that internal fields _raw and _time (timestamp) are returned by default
        - To include fields: 
            - Use fields ( or fields +) - default behaviour 
            - Only the specified fields are extracted.
            - Performance improvement on field extractions
        - To exclude fields 
            - Use fields - 
            - Happens after field extractions - no performance improvement 
- **Table and rename commands**
    - Table command creates a statistics table of the specified fields
    - Each row of the table represents an event, and the columns represent field names 
    - Columns are displayed in the order given in the command 
    - Use rename command to change the name of a field 
        - `rename method as "HTTP method", status as "HTTP status", clientip as Client_IPAddress`
        - Use double quotes when field names include spaces or special characters 
    ```
        index=web sourcetype=access_combined
        | table clientip, bytes, status, method, productId
        | rename method as "HTTP method", status as "HTTP status", clientip As CLient_IPAddress
    ```
- **Sort command**
    - Sort search results by specified fields
    - To sort in ascending order:
        - Use sort + <fieldname>
    - TO sort in descending order:
        - Use sort - <fieldname>
    - Use the limit argument to limit the number of results 
        - sort 20 - "HttP method"
    - To sort on multiple fields, use a space after a sort sign as per the fields order you want to sort
        - `sort -Client_IPAddress, "HTTP Method"`
        - `sort - Client_IPAddress, "HTTP Method"`
    ```
        index=web sourcetype=access_combined
        | table clientip, bytes, status, method, productId
        | rename method as "HTTP method", status as "HTTP status", clientip As CLient_IPAddress
        | sort - CLient_IPAddress, "HTTP status" limit 10
    ```
- **Dedup command**
    - Removes deuplicates from your results 
    - `dedup CLIent_IPAddress`
    - Uses identical combinations of field values 
        - `dedup Client_IPAddress, "HTTP Method"`
</details>

---

<details>
  <summary> Module 6 : Basic Transforming commands </summary>

- **What are transforming commands?**
    - Transforming commands are used to order search results into a table 
    - The transformed data can be used to create vistualizations.
    - Splunk Enterprise ships with multiple visualization types :
        - Charts - Line, Area, Column, Bar, Pie, Scatter, Bubble 
        - Gauges : Radial, Filler, Marker
        - Maps - Cluster, Choropleth
        - Single Value 
    - Transforming command examples : 
        - table, stats, top, rare, chart, timechart 
- **Using the stats command**
    - Use the stats command to perform statistical calculations on the data retrieved by search 
    - It's a requirement to use the stats command with statistics functions 
    - Statistics function examples : 
        - count 
            - counts the number of events 
            - use count() to count the number of events matching the argument
        - distinct_count, dc - count the number of unique values for a specified field 
        - sum - calculate the sum of values in a numeric field 
        - avg - calculate average of values in a numeric field 
        - list - list all values of a given field 
        - values - list all unique values of a given field 
        - max 
        - min - min value of a numeric field 

    - Exam tips 
        - Identify functions used with stats command 

- **Stats count function** 
    - Use the count function to return the number of events for current search 
    - Associates the number of results to count field by default 
    - To rename the count field, use the `AS` clause 
    - Passing field name as argument - count(fieldname)
        - Counts the number of events containing fieldname 
        - Example : count(zipCode)
    ```
        index=main sourcetype=eventgen
        | stats count(zipCode) as "Total Events with ZipCode"
    ```
    - Use the `BY` clause to return the count for different field combinations
    - Can use any number of fields in your events 
    ```
        index=main sourcetype=eventgen
        | stats count as "Total Events" by nodeName
    ```
    - Sort and give top 20 values 
    ```
        index=main sourcetype=eventgen
        | stats count(failureCode) as "Total Failure Code Counts" by nodeName, partner
        | sort 20 - "Total Failure Code Counts"
    ```
- **stats discint_count function** 
    - Use discint_count or dc() to get the unique values for a given field.
    - Example : How many different zip codes exist in the result set.
    ```
        index=main sourcetype=eventgen
        | stats distinct_count(zipCode) as "Number of zip codes", distinct_count(failureCode) as "Number of failure code"
    ```
    - Exam tips : 
        - Which command provides count of unique values?
        - Syntax of stats command with distinct_count function
- **stats sum and avg functions** 
    - Use sum() function to get the sum of values in a numeric field 
    - Use avg() function to get the average of values in a numeric field 
    - Demo 
        - Calculate the total duration of calls (in seconds) by partner, for calls with responseCode=200, in last 4 hours.
            - Round to seconds by removing millisection fraction. 
            - Convert the total time to Hours:Mins:Secs using the tostring function 
        - Calculate the average duration of calls (in seconds) by partner, for calls with responseCode=200, in last 24 hours.
            - Round to a precision of 2.
            - Convert the average time to Hours:Mins:Secs using the tostring function 
    ```
        index=main sourcetype=eventgen
        | stats sum(duration) as TotalCallTime by partner
        | eval TotalCallTime=round(TotalCallTime)
        | eval "Duration by partner"=tostring(TotalCallTime, "duration")
    ```
    - tostring() function - https://docs.splunk.com/Documentation/SCS/current/SearchReference/ConversionFunctions?#tostring.28.26lt.3Bvalue.26gt.3B.2C_.26lt.3Bformat.26gt.3B.29

    ```
        index=main sourcetype=eventgen responseCode=200
        | stats avg(duration) as AvgCallTime By partner
        | eval AvgCallTime=round(AvgCallTime,2)
        | eval "Avg Duration by Partner"=tostring(AvgCallTime, "duration")
    ```

- **stats list and values functions** 

- **combining functions** 

- **using the top command** 

- **using the rare command**

- **formatting statistics tables** 

- **Formatting visualisations** 


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

