# Microsoft Fabric Pipeline Monitoring
Repository for programmatic monitoring of Microsoft Fabric Data Factory pipelines

Currently, monitoring of Fabric pipelines is online only through the Fabric portal. 
Workspace monitoring is coming soon and it is hoped that this will be used for programatic monitoring. 
https://learn.microsoft.com/en-us/fabric/release-plan/admin-governance#workspace-monitoring

However, you can implement your own programmatic monitoring by capturing the output of pipeline activities and sending this to a KQL database (Fabric Eventhouse) that you can build Power BI reports on as well as set Reflex alerts to notify you of pipeline failures. 

Using a simple pipeline with a copy activity as an example, we can take the On-Completion output of the activity and send it to a KQL Script activity for logging in a KQL database. We use the on-completion activity as it captures all exit states (fail, succeed, skip). The KQL database and the monitoring table have been pre-created. 

![image](https://github.com/user-attachments/assets/b3900f99-94d8-4eb5-a899-8175a60586ef)

After connecting to the KQL database we use the the pipeline expression builder to create the command. Using both System variables and Activity Outputs we can capture all the necessary information to monitor pipeline and activity execution. 

![image](https://github.com/user-attachments/assets/dc7a80ed-67a5-460e-a005-65d31344bd4d)

In this example I have chosen to send the data to a file in the database but your could equally send the information to a table. 

![image](https://github.com/user-attachments/assets/17674704-5925-411f-aa23-6e8ea3040bfe)

The KQL script I have used has been uploaded as kql.txt
