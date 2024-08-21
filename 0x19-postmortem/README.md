
Postmortem:      Web Server Outage Due to Misconfigured Firewall

  Issue Summary:  
  
  On August 22, 2024, from 09:00 to 09:45 PST (45 minutes), our primary web server was unreachable, leading to a complete outage of our web application. During this period, 100% of users were unable to access the service, resulting in significant disruption. The root cause was a misconfigured firewall rule that inadvertently blocked all inbound HTTP and HTTPS traffic.  
  Timeline:

       09:02 PST: Monitoring alert triggered for a 100% drop in HTTP traffic.     
       09:03 PST: On-call engineer starts investigating, initially suspects a network connectivity issue.     
       09:05 PST: Network logs and server connectivity checks performed, revealing no external access to the server.     
       09:10 PST: Firewall logs reviewed; no suspicious activity detected.     
       09:15 PST: Recent firewall configuration changes identified; misconfiguration suspected.     
       09:20 PST: Firewall configuration reviewed; erroneous rule identified that blocked all inbound web traffic.     
       09:25 PST: Incident escalated to the network security team for confirmation and resolution.     
       09:30 PST: Misconfigured firewall rule corrected, web server becomes reachable again.     
       09:45 PST: Full service restored, incident marked as resolved.

       Root Cause and Resolution:
       
         The root cause of the outage was a firewall rule misconfiguration that occurred during routine security updates. The update included a new rule intended to block certain malicious IP addresses. However, due to a syntax error, the rule was too broad and inadvertently blocked all inbound traffic on ports 80 (HTTP) and 443 (HTTPS), causing the web server to become inaccessible.
         
        
        To resolve the issue, the network security team corrected the misconfigured rule by narrowing its scope to only block the intended malicious IP addresses. Once the firewall rule was updated, inbound traffic to the web server resumed, and normal access to the web application was restored.  
        Corrective and Preventative Measures:      
        
        Configuration Validation: Implement a validation process for firewall rule changes to ensure they do not inadvertently block critical traffic.     
        Testing: Introduce a staging environment to test firewall rules before deploying them to production.     Monitoring: Enhance monitoring to detect and alert on sudden drops in web traffic that could indicate a firewall issue.     
        Access Control: Restrict firewall rule changes to a limited number of trained personnel to reduce the risk of human error.  
        TODO:
              Develop and integrate firewall rule validation scripts into the deployment process.     Set up a staging environment for testing network security changes.     Configure monitoring alerts for unusual drops in web server traffic.     Conduct training sessions for network security personnel on firewall management.     
              Review and update the firewall rule management policy.  