# Microsoft Fabric Pipeline Monitoring
Repository for programmatic monitoring of Microsoft Fabric Data Factory pipelines

Currently, monitoring of Fabric pipelines is online only through the Fabric portal. 
Workspace monitoring is coming soon and it is hoped that this will be used for programatic monitoring. 
https://learn.microsoft.com/en-us/fabric/release-plan/admin-governance#workspace-monitoring

However, you can implement your own programmatic monitoring by capturing the output of pipeline activities and sending this to a KQL database (Fabric Eventhouse) that you can build Power BI reports on as well as set Reflex alerts to notify you of pipeline failures. 

Using a simple pipeline with a copy activity as an example, we can take the On-Completion output of the activity and send it to a KQL Script activity for logging in a KQL database. We use the on-completion activity as it captures all exit states (fail, succeed, skip). The KQL database and the monitoring table have been pre-created. 

![image](https://github.com/user-attachments/assets/2b72cd93-9b91-4eb3-9b00-7e9826d88fcd)


After connecting to the KQL database we use the the pipeline expression builder to create the command. Using both System variables and Activity Outputs we can capture all the necessary information to monitor pipeline and activity execution. 

![image](https://github.com/user-attachments/assets/bf165477-d475-4120-9f99-193596ee10bb)

In this example I have chosen to send the data to a table called DFPipelineDetails in the database. 

![image](https://github.com/user-attachments/assets/79eb4f2c-f938-4087-8594-38f271bc4ee9)


The KQL script I have used has been uploaded as kql.txt

The next step is to setup monitoring alerts. 
Creating a queryset that filters pipeline activities on their activity status we can setup alerts when they have failed. 
You can adjust your sampling frequency and type of alert action to suit your needs. 

![image](https://github.com/user-attachments/assets/b67e926d-eaad-439e-8cb9-32ad3f931623)


We can also setup a Power BI report on the table so that we have a monitoring dashboard for our Fabric Data Factory Pipelines. 

![image](https://github.com/user-attachments/assets/bcfcdfbf-83be-4349-a084-e788ec3ed80b)

This one is rather rudimentary but you get the idea

![image](https://github.com/user-attachments/assets/5a56b1d3-e497-4a30-b2de-6550744fc2da)




