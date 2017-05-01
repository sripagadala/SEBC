1. Check vm.swappiness on all your nodes
				Set the value to 1 if necessary
				cat /proc/sys/vm/swappiness

				echo 1 > /proc/sys/vm/swappiness
	
2.Show the mount attributes of your volume(s)

				[root@ip-172-31-6-38 etc]# mount -v
				sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
				proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
				devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=15340256k,nr_inodes=3835064,mode=755)
				securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
				tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
				devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
				tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
				tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
				cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
				pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
				cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
				cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
				cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
				cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
				cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
				cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
				cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
				cgroup on /sys/fs/cgroup/net_cls type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls)
				cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
				configfs on /sys/kernel/config type configfs (rw,relatime)
				/dev/xvda2 on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
				selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
				systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=27,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
				debugfs on /sys/kernel/debug type debugfs (rw,relatime)
				mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
				hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
				tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=3045488k,mode=700,uid=1000,gid=1000)


		[root@ip-172-31-6-38 etc]# df -h
		Filesystem      Size  Used Avail Use% Mounted on
		/dev/xvda2       10G  928M  9.1G  10% /
		devtmpfs         15G     0   15G   0% /dev
		tmpfs            15G     0   15G   0% /dev/shm
		tmpfs            15G   17M   15G   1% /run
		tmpfs            15G     0   15G   0% /sys/fs/cgroup
		tmpfs           3.0G     0  3.0G   0% /run/user/1000

3.If you have ext-based volumes, list the reserve space setting
   XFS volumes do not support reserve space
   

				[root@ip-172-31-6-38 dev]# sudo parted -l
				Model: Xen Virtual Block Device (xvd)
				Disk /dev/xvda: 10.7GB
				Sector size (logical/physical): 512B/512B
				Partition Table: gpt
				Disk Flags: pmbr_boot

				Number  Start   End     Size    File system  Name  Flags
				 1      1049kB  2097kB  1049kB                     bios_grub
				 2      2097kB  10.7GB  10.7GB  xfs


 
4. Disable transparent hugepage support 
			  if test -f /sys/kernel/mm/transparent_hugepage/enabled; then
			   echo never > /sys/kernel/mm/transparent_hugepage/enabled
			 fi

 
5. List your network interface configuration 

			[root@ip-172-31-9-175 network-scripts]# cat ifcfg-eth0
			DEVICE="eth0"
			BOOTPROTO="dhcp"
			ONBOOT="yes"
			TYPE="Ethernet"
			USERCTL="yes"
			PEERDNS="yes"
			IPV6INIT="no"

 
			 [root@ip-172-31-6-38 etc]#  cat /etc/sysconfig/network
			 NETWORKING=yes
			 NOZEROCONF=yes


6. Show correct forward and reverse host lookups
For /etc/hosts, use getent
For DNS, use nslookup

		Forward DNS lookup is using an Internet domain name to find an IP address. 
		Reverse DNS lookup is using an Internet IP address to find a domain name.

          $yum install bind-utils - to install nslookup, dig utilities

		  
		  [ec2-user@ip-172-31-9-175 ~]$ getent ahosts ip-172-31-9-175.ap-southeast-2.compute.internal has address
			172.31.9.175    STREAM ip-172-31-9-175.ap-southeast-2.compute.internal
			172.31.9.175    DGRAM
			172.31.9.175    RAW
			
						[ec2-user@ip-172-31-9-175 ~]$ dig -x 172.31.9.175

						; <<>> DiG 9.9.4-RedHat-9.9.4-38.el7_3.3 <<>> -x 172.31.9.175
						;; global options: +cmd
						;; Got answer:
						;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62773
						;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

						;; OPT PSEUDOSECTION:
						; EDNS: version: 0, flags:; udp: 4096
						;; QUESTION SECTION:
						;175.9.31.172.in-addr.arpa.     IN      PTR

						;; ANSWER SECTION:
						175.9.31.172.in-addr.arpa. 60   IN      PTR     ip-172-31-9-175.ap-southeast-2.compute.internal.

						;; Query time: 10 msec
						;; SERVER: 172.31.0.2#53(172.31.0.2)
						;; WHEN: Mon May 01 06:02:27 EDT 2017
						;; MSG SIZE  rcvd: 115

			[ec2-user@ip-172-31-9-175 ~]$ host 172.31.9.175
			175.9.31.172.in-addr.arpa domain name pointer ip-172-31-9-175.ap-southeast-2.compute.internal.
			
					[ec2-user@ip-172-31-9-175 ~]$ host -t  a ip-172-31-9-175.ap-southeast-2.compute.internal
					ip-172-31-9-175.ap-southeast-2.compute.internal has address 172.31.9.175
					


	 
7.Show the nscd service is running  -  not able to check in EC2 instance 
8.Show the ntpd service is running  - Requires configuration in aws??
					[root@ip-172-31-6-38 init.d]# ntpstat
					Unable to talk to NTP daemon. Is it running?
					[root@ip-172-31-6-38 init.d]# ntpq -p
					ntpq: read: Connection refused
					[root@ip-172-31-6-38 init.d]# sudo service ntpd start
					Redirecting to /bin/systemctl start  ntpd.service
					[root@ip-172-31-6-38 init.d]# sudo chkconfig ntpd on
					Note: Forwarding request to 'systemctl enable ntpd.service'.


	
	 
	 