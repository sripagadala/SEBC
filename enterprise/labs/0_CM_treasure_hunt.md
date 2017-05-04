1.What is ubertask optimization?
	Enabling it runs “sufficiently small” jobs sequentially within a single JVM. 
	This property can be changed in Performance category. Property name is mapreduce.job.ubertask.enable

2. Where in CM is the Kerberos Security Realm value displayed?

   The Kerberos default realm is configured in the libdefaults property in the /etc/krb5.conf file on every host in the cluster
   In the Cloudera Manager Admin Console, select Administration > Settings.
   Click the Security category, and enter the Kerberos realm for the cluster in the Kerberos Security Realm field (for example, YOUR-LOCAL-REALM.COM or YOUR-SUB-REALM.YOUR-LOCAL-REALM.COM) that you configured in the krb5.conf file.
   Click Save Changes
   
3.Which CDH service(s) host a property for enabling Kerberos authentication?
4.How do you upgrade the CM agents?
5.Give the tsquery statement used to chart Hue's CPU utilization?
6.Name all the roles that make up the Hive service
7.What steps must be completed before integrating Cloudera Manager with Kerberos?
