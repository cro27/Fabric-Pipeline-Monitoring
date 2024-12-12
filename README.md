# Microsoft Fabric Pipeline Monitoring
## Repository for programmatic monitoring of Microsoft Fabric Data Factory pipelines

Currently, monitoring of Fabric pipelines is online only, through the Fabric portal. 
Workspace monitoring feature is coming soon and it is hoped that this will be used for programatic monitoring. 
https://learn.microsoft.com/en-us/fabric/release-plan/admin-governance#workspace-monitoring

However, you can implement your own programmatic monitoring by capturing the output of pipeline activities and sending this to a KQL database (Fabric Eventhouse) that you can build Power BI reports on as well as set Reflex alerts to notify you of pipeline failures. 

Using a simple pipeline with a copy activity as an example, we can take the On-Completion output of the activity and send it to a KQL Script activity for logging in a KQL database. We use the on-completion activity as it captures all exit states (fail, succeed, skip). The KQL database and the monitoring table have been pre-created. 

![image](https://github.com/user-attachments/assets/59b6ce64-e439-4be4-a0b2-484a54b4ceee)

After connecting to the KQL database we use the the pipeline expression builder to create the command. Using both System variables and Activity Outputs we can capture all the necessary information to monitor pipeline and activity execution. 

![image](https://github.com/user-attachments/assets/452d89ac-3300-43be-895c-1651c845e9f5)

In this example I have chosen to send the data to a table called DFPipelineDetails in the database. 

![image](https://github.com/user-attachments/assets/79eb4f2c-f938-4087-8594-38f271bc4ee9)

The KQL script I have used has been uploaded as kql.txt

The next step is to setup monitoring alerts. 
Creating a queryset that filters pipeline activities on their activity status we can setup alerts when they have failed, skipped or succeeded. In this example I am filtering on Failed activities. 
You can adjust your sampling frequency and type of alert action to suit your needs. 

![image](https://github.com/user-attachments/assets/b67e926d-eaad-439e-8cb9-32ad3f931623)

We can also setup a Power BI report on the table so that we have a monitoring dashboard for our Fabric Data Factory Pipelines. 

![image](https://github.com/user-attachments/assets/bcfcdfbf-83be-4349-a084-e788ec3ed80b)

This report is rudimentary but shows the basic information collected.  

![image](https://github.com/user-attachments/assets/a2291d2b-af07-42f2-899e-8cb9c5247966)

### Limitations
Activity Name can't be paramerterised yet so you must configure this in the expression builder for each activity being monitored. 



