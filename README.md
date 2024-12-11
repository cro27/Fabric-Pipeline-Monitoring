# Fabric-Pipeline-Monitoring
Repository for programmatic monitoring of Fabric Data Factory pipelines

Currently, monitoring of Fabric pipelines is online only through the Fabric portal. 
Workspace monitoring is coming soon and it is hoped that this will be used for programatic monitoring. 
https://learn.microsoft.com/en-us/fabric/release-plan/admin-governance#workspace-monitoring

However, you can implement your own programmatic monitoring by capturing the output of pipeline activities and sending this to a KQL database (Fabric Eventhouse) that you can build Power BI reports on as well as set Reflex alerts to notify you of pipeline failures. 

