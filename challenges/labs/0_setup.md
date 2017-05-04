List the cloud provider you are using (AWS, GCE, Azure, other)-AWS

List the nodes you are using by IP address and name
		ip-172-31-8-38.ap-southeast-2.compute.internal          host1.example.com       host1
		ip-172-31-3-131.ap-southeast-2.compute.internal         host2.example.com       host2
		ip-172-31-15-230.ap-southeast-2.compute.internal        host3.example.com       host3
		ip-172-31-7-184.ap-southeast-2.compute.internal         host4.example.com       host4
		ip-172-31-13-109.ap-southeast-2.compute.internal        host5.example.com       host5

List the Linux release you are using

	NAME="Red Hat Enterprise Linux Server"
	VERSION="7.2 (Maipo)"

Demonstrate the disk capacity available on each node is >= 30 GB

		[root@ip-172-31-8-38 ec2-user]# df -h
		Filesystem      Size  Used Avail Use% Mounted on
		/dev/xvda2       30G  927M   30G   4% /
		devtmpfs        7.3G     0  7.3G   0% /dev
		tmpfs           7.2G     0  7.2G   0% /dev/shm
		tmpfs           7.2G   17M  7.2G   1% /run
		tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
		tmpfs           1.5G     0  1.5G   0% /run/user/1000



List the command and output for yum repolist enabled

		[root@ip-172-31-8-38 ec2-user]# yum repolist enabled
		Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
		rhui-REGION-client-config-server-7                                                                                                                                    | 2.9 kB  00:00:00
		rhui-REGION-rhel-server-releases                                                                                                                                      | 3.5 kB  00:00:00
		rhui-REGION-rhel-server-rh-common                                                                                                                                     | 3.8 kB  00:00:00
		(1/7): rhui-REGION-client-config-server-7/x86_64/primary_db                                                                                                           | 5.4 kB  00:00:00
		(2/7): rhui-REGION-rhel-server-releases/7Server/x86_64/updateinfo                                                                                                     | 1.9 MB  00:00:00
		(3/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/group                                                                                                         |  104 B  00:00:00
		(4/7): rhui-REGION-rhel-server-releases/7Server/x86_64/group                                                                                                          | 701 kB  00:00:00
		(5/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/primary_db                                                                                                    | 118 kB  00:00:00
		(6/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/updateinfo                                                                                                    |  33 kB  00:00:00
		(7/7): rhui-REGION-rhel-server-releases/7Server/x86_64/primary_db                                                                                                     |  35 MB  00:00:00
		repo id                                                                             repo name                                                                                          status
		rhui-REGION-client-config-server-7/x86_64                                           Red Hat Update Infrastructure 2.0 Client Configuration Server 7                                         6
		rhui-REGION-rhel-server-releases/7Server/x86_64                                     Red Hat Enterprise Linux Server 7 (RPMs)                                                           14,277
		rhui-REGION-rhel-server-rh-common/7Server/x86_64                                    Red Hat Enterprise Linux Server 7 RH Common (RPMs)                                                    228
		repolist: 14,511

List the /etc/passwd entries for neymar and ronaldo
	[root@ip-172-31-8-38 ec2-user]# cat /etc/passwd|grep -e "neymar" -e "renaldo"
	neymar:x:2010:2018::/home/neymar:/bin/bash
	renaldo:x:2016:2017::/home/renaldo:/bin/bash

List the /etc/group entries for barca and merengues
[root@ip-172-31-8-38 ec2-user]# cat /etc/group|grep -e merengues -e barca
	barca:x:2017:
	merengues:x:2018:

