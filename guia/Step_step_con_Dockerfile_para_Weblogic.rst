Step to step con Dockerfile paraWeblogic
==========================================

::
 
	[oracle@srvdocker01 consis]$ docker build -t "weblogic:12.2.1.3.0" --build-arg PORT=7022 .
	Sending build context to Docker daemon  1.382GB
	Step 1/45 : FROM centos:7
	 ---> e934aafc2206
	Step 2/45 : MAINTAINER Carlos Gomez G cgomeznt@gmail.com
	 ---> Using cache
	 ---> fbc44dce01f0
	Step 3/45 : ENV     container docker
	 ---> Using cache
	 ---> 16a41c8d8aca
	Step 4/45 : RUN     yum -y update
	 ---> Using cache
	 ---> 2c45010d1cea
	Step 5/45 : RUN     yum -y install sudo         tar         gzip         openssh-clients         vi         find 	net-tools
	 ---> Using cache
	 ---> 3b931b4b93b0
	Step 6/45 : RUN	yum clean all
	 ---> Using cache
	 ---> 5294974e5923
	Step 7/45 : RUN     groupadd oinstall
	 ---> Using cache
	 ---> 6dfd6ab8a946
	Step 8/45 : RUN     useradd -g oinstall oracle
	 ---> Using cache
	 ---> 57c43cd10cd9
	Step 9/45 : RUN	mkdir -p /u01/software
	 ---> Using cache
	 ---> da8c726b3870
	Step 10/45 : RUN	mkdir -p /scm/EAR
	 ---> Using cache
	 ---> 0085290b44db
	Step 11/45 : RUN	mkdir -p /scm/external
	 ---> Using cache
	 ---> dafa82c83727
	Step 12/45 : RUN	mkdir -p /scm/scripts
	 ---> Using cache
	 ---> 5c354b2b2f53
	Step 13/45 : RUN	mkdir -p /scm/logs
	 ---> Using cache
	 ---> 6fc16ba88d9c
	Step 14/45 : RUN	mkdir -p /u01/app/oracle/middleware
	 ---> Using cache
	 ---> b5ca5dfc813a
	Step 15/45 : RUN	mkdir -p /u01/app/oracle/config/domains
	 ---> Using cache
	 ---> 65ba0c39580e
	Step 16/45 : RUN	mkdir -p /u01/app/oracle/config/applications
	 ---> Using cache
	 ---> a8cb4e49c520
	Step 17/45 : RUN	chown -R oracle:oinstall /u01
	 ---> Using cache
	 ---> 4f95bf308b10
	Step 18/45 : RUN	chown -R oracle:oinstall /scm
	 ---> Using cache
	 ---> 80a07afe789f
	Step 19/45 : RUN	chmod -R 775 /u01/
	 ---> Using cache
	 ---> 43cf8e0003af
	Step 20/45 : RUN	chmod -R 775 /scm/
	 ---> Using cache
	 ---> f91a6931ec31
	Step 21/45 : ENV	export MW_HOME=/u01/app/oracle/middleware
	 ---> Using cache
	 ---> 1c5c2b90ca79
	Step 22/45 : ENV	export WLS_HOME=$MW_HOME/wlserver
	 ---> Using cache
	 ---> b83b9a0efa5d
	Step 23/45 : ENV	export WL_HOME=$WLS_HOME
	 ---> Using cache
	 ---> 23248529d8d9
	Step 24/45 : ENV	export JAVA_HOME=/u01/app/oracle/jdk1.8.0_77
	 ---> Using cache
	 ---> 137d51d92144
	Step 25/45 : ENV	export PATH=$JAVA_HOME/bin:$PATH
	 ---> Using cache
	 ---> 7595abfb8a5c
	Step 26/45 : COPY	jdk-8u101-linux-x64.rpm	/u01/software
	 ---> Using cache
	 ---> 48ac6a4656fa
	Step 27/45 : RUN	rpm -ivh /u01/software/jdk-8u101-linux-x64.rpm
	 ---> Using cache
	 ---> 3f4106072fd3
	Step 28/45 : COPY	wls.rsp /u01/software
	 ---> Using cache
	 ---> 23693beabd4e
	Step 29/45 : COPY	oraInst.loc /u01/software
	 ---> Using cache
	 ---> d685143d1422
	Step 30/45 : COPY	basicWLSDomain7021DataSource.py /u01/software
	 ---> 7bb269f2fe67
	Step 31/45 : COPY 	fmw_12.2.1.3.0_wls.jar /u01/software
	 ---> 664110d2217b
	Step 32/45 : COPY	AcseleConfigurationfile_7022_CRECER_13.8.txt /scm/external
	 ---> 48a49f70c1f3
	Step 33/45 : COPY	CONSIS.ear /scm/EAR
	 ---> 6f784b3ff4e4
	Step 34/45 : COPY	startWebLogic.sh /scm/scripts
	 ---> ec74e210d293
	Step 35/45 : COPY	stopWebLogic.sh /scm/scripts
	 ---> e6151cc8f3ea
	Step 36/45 : USER	oracle
	 ---> Running in a116d4a03214
	Removing intermediate container a116d4a03214
	 ---> 3ad5f4de83c8
	Step 37/45 : RUN 	$JAVA_HOME/bin/java -Xmx1024m -jar /u01/software/fmw_12.2.1.3.0_wls.jar -silent -responseFile /u01/software/wls.rsp -invPtrLoc /u01/software/oraInst.loc
	 ---> Running in 6a8bd19fbf89
	Launcher log file is /tmp/OraInstall2018-05-18_02-06-23PM/launcher2018-05-18_02-06-23PM.log.
	Extracting the installer . . . . . . . . . . . . . . . . . . . . . . Done
	Checking if CPU speed is above 300 MHz.   Actual 2993.200 MHz    Passed
	Checking swap space: must be greater than 512 MB.   Actual 1023 MB    Passed
	Checking if this platform requires a 64-bit JVM.   Actual 64    Passed (64-bit not required)
	Checking temp space: must be greater than 300 MB.   Actual 18190 MB    Passed
	Preparing to launch the Oracle Universal Installer from /tmp/OraInstall2018-05-18_02-06-23PM
	Log: /tmp/OraInstall2018-05-18_02-06-23PM/install2018-05-18_02-06-23PM.log
	Copyright (c) 1996, 2017, Oracle and/or its affiliates. All rights reserved.
	Reading response file..
	Skipping Software Updates
	Starting check : CertifiedVersions
	Prerequisite Check was skipped and did not execute.
	Warning: Check:CertifiedVersions completed with warnings.


	Starting check : CheckJDKVersion
	Problem: This JDK version was not certified at the time it was made generally available. It may have been certified following general availability.

	Recommendation: Check the Supported System Configurations Guide (http://www.oracle.com/technetwork/middleware/ias/downloads/fusion-certification-100350.html) for further details. Press "Next" if you wish to continue.

	Expected result: 1.8.0_131
	Actual result: 1.8.0_101
	Warning: Check:CheckJDKVersion completed with warnings.


	Validations are enabled for this session.
	Verifying data
	Copying Files
	Percent Complete : 10
	Percent Complete : 20
	Percent Complete : 30
	Percent Complete : 40
	Percent Complete : 50
	Percent Complete : 60
	Percent Complete : 70
	Percent Complete : 80
	Percent Complete : 90
	Percent Complete : 100

	The installation of Oracle Fusion Middleware 12c WebLogic Server and Coherence 12.2.1.3.0 completed successfully.
	Logs successfully copied to /u01/app/oraInventory/logs.
	Removing intermediate container 6a8bd19fbf89
	 ---> d612ebf56fb4
	Step 38/45 : RUN	source /u01/app/oracle/middleware/wlserver/server/bin/setWLSEnv.sh  && 	$JAVA_HOME/bin/java weblogic.WLST /u01/software/basicWLSDomain7021DataSource.py
	 ---> Running in 480c0896b261
	CLASSPATH=/usr/java/jdk1.8.0_101/lib/tools.jar:/u01/app/oracle/middleware/wlserver/modules/features/wlst.wls.classpath.jar:

	PATH=/u01/app/oracle/middleware/wlserver/server/bin:/u01/app/oracle/middleware/wlserver/../oracle_common/modules/thirdparty/org.apache.ant/1.9.8.0.0/apache-ant-1.9.8/bin:/usr/java/jdk1.8.0_101/jre/bin:/usr/java/jdk1.8.0_101/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/u01/app/oracle/middleware/wlserver/../oracle_common/modules/org.apache.maven_3.2.5/bin

	Your environment has been set.

	Initializing WebLogic Scripting Tool (WLST) ...

	Jython scans all the jar files it can find at first startup. Depending on the system, this process may take a few minutes to complete, and WLST may not return a prompt right away.

	Welcome to WebLogic Server Administration Scripting Shell

	Type help() for help on available commands

	Iniciando el proceso desasistido de la instalacion de Weblogic 12.2.1.3.0
	Creando el puerto por el 7021
	Creando el usuario weblogic y asignandole la clave
	Create datasource Datasource-GS para el esquema SCM_CRECERGU_V138
	Asignando el Datasource a AdminServer
	Create datasource Datasource-PE SCM_CRECER_V138
	Asignando el Datasource a AdminServer
	Creating Domain...!!!
	Culminado el proceso de creacion de Dominio para Weblogic


	Exiting WebLogic Scripting Tool.

	Removing intermediate container 480c0896b261
	 ---> 1d6f8d644939
	Step 39/45 : RUN	sed -i '/<configuration-version>12.2.1.3.0<\/configuration-version>/a <web-app-container>' 	/u01/app/oracle/middleware/user_projects/domains/D7021/config/config.xml; 	sed -i '/<web-app-container>/a <show-archived-real-path-enabled>true<\/show-archived-real-path-enabled>' 	/u01/app/oracle/middleware/user_projects/domains/D7021/config/config.xml; 	sed -i '/<show-archived-real-path-enabled>true<\/show-archived-real-path-enabled>/a <\/web-app-container>' 	/u01/app/oracle/middleware/user_projects/domains/D7021/config/config.xml
	 ---> Running in 051874b65025
	Removing intermediate container 051874b65025
	 ---> 257575c8ff51
	Step 40/45 : RUN	rm -rf /u01/software/*
	 ---> Running in 2ec9c7dc872f
	Removing intermediate container 2ec9c7dc872f
	 ---> 756fead8273e
	Step 41/45 : VOLUME	"/scm"
	 ---> Running in 07d617e8b5d0
	Removing intermediate container 07d617e8b5d0
	 ---> d6cf8b55b619
	Step 42/45 : EXPOSE	7021
	 ---> Running in 52f7b7f6f129
	Removing intermediate container 52f7b7f6f129
	 ---> 7c0c4bc7eaa5
	Step 43/45 : ARG	PORT=7021
	 ---> Running in 2beabd30b102
	Removing intermediate container 2beabd30b102
	 ---> cfe76a95ba8b
	Step 44/45 : EXPOSE	$PORT
	 ---> Running in e46ddc5e0ba3
	Removing intermediate container e46ddc5e0ba3
	 ---> e622a61460b7
	Step 45/45 : CMD ["/scm//scripts/startWebLogic.sh"]
	 ---> Running in e9d94ea5d225
	Removing intermediate container e9d94ea5d225
	 ---> fd40a4b4601f
	Successfully built fd40a4b4601f
	Successfully tagged weblogic:12.2.1.3.0

::

	[oracle@srvdocker01 consis]$ docker images
	REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
	weblogic            12.2.1.3.0          fd40a4b4601f        3 minutes ago       3.05GB
	weblogic            latest              bd722b6a550b        11 hours ago        3.05GB
	<none>              <none>              10e84e7d6d57        13 hours ago        3.05GB
	hello-world         latest              e38bc07ac18e        5 weeks ago         1.85kB
	centos              7                   e934aafc2206        5 weeks ago         199MB

::

	[oracle@srvdocker01 consis]$ docker run -dti --name "WebLogic"  -p 7022:7021 "weblogic:12.2.1.3.0"
	ecde063fb19c461fa93af1684ae1755a0e081ddfc6efb303e6b3e6c6a5e313a6
	[oracle@srvdocker01 consis]$ 

::

	[oracle@srvdocker01 consis]$ docker ps
	CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                              NAMES
	dfbf1dbe6c1d        weblogic:12.2.1.3.0   "/scm//scripts/start???"   51 seconds ago      Up 49 seconds       7022/tcp, 0.0.0.0:7022->7021/tcp   WebLogic
	[oracle@srvdocker01 consis]$ 


::

	[oracle@srvdocker01 consis]$ docker exec -i -t WebLogic /bin/bash
	[oracle@ecde063fb19c /]$ 

::

	[oracle@ecde063fb19c /]$ netstat -nat
	Active Internet connections (servers and established)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State      
	tcp        0      0 127.0.0.1:1527          0.0.0.0:*               LISTEN     

::

	[oracle@ecde063fb19c /]$ ps -ef | grep java
	oracle      55     1  1 14:23 pts/0    00:00:00 /usr/java/jdk1.8.0_101/bin/java -Dderby.system.home=/u01/app/oracle/middleware/user_projects/domains/D7021/common/db -classpath /u01/app/oracle/middleware/wlserver/common/derby/lib/derby.jar:/u01/app/oracle/middleware/wlserver/common/derby/lib/derbynet.jar:/u01/app/oracle/middleware/wlserver/common/derby/lib/derbytools.jar:/u01/app/oracle/middleware/wlserver/common/derby/lib/derbyclient.jar org.apache.derby.drda.NetworkServerControl start
	oracle      56     5 12 14:23 pts/0    00:00:11 /usr/java/jdk1.8.0_101/bin/java -server -Xms256m -Xmx512m -XX:CompileThreshold=8000 -cp /u01/app/oracle/middleware/wlserver/server/lib/weblogic-launcher.jar -Dlaunch.use.env.classpath=true -Dweblogic.Name=AdminServer -Djava.security.policy=/u01/app/oracle/middleware/wlserver/server/lib/weblogic.policy -Djava.system.class.loader=com.oracle.classloader.weblogic.LaunchClassLoader -javaagent:/u01/app/oracle/middleware/wlserver/server/lib/debugpatch-agent.jar -da -Dwls.home=/u01/app/oracle/middleware/wlserver/server -Dweblogic.home=/u01/app/oracle/middleware/wlserver/server weblogic.Server
	oracle     121   104  0 14:24 pts/1    00:00:00 grep --color=auto java
	[oracle@ecde063fb19c /]$ 

::

	[oracle@srvdocker01 consis]$ docker stop WebLogic
	WebLogic

::

	[oracle@srvscm02 ~]$ docker ps -f "status=exited"
	CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                            PORTS               NAMES
	1a5d26666303        weblogic:12.2.1.3.0   "/scm//scripts/start???"   3 hours ago         Exited (137) About a minute ago                       WebLogic
	31f32df457c2        hello-world           "/hello"                 4 hours ago         Exited (0) 4 hours ago                                friendly_kilby
	7395b2dc046a        hello-world           "/hello"                 4 hours ago         Exited (0) 4 hours ago                                lucid_banach
	[oracle@srvscm02 ~]$ 


::

	[oracle@srvdocker01 consis]$ docker start WebLogic
	WebLogic

::

	[oracle@srvdocker01 consis]$ docker container inspect WebLogic
	[
	    {
		"Id": "ecde063fb19c461fa93af1684ae1755a0e081ddfc6efb303e6b3e6c6a5e313a6",
		"Created": "2018-05-18T14:23:12.658965556Z",
		"Path": "/scm//scripts/startWebLogic.sh",
		"Args": [],
		"State": {
		    "Status": "running",
		    "Running": true,
		    "Paused": false,
		    "Restarting": false,
		    "OOMKilled": false,
		    "Dead": false,
		    "Pid": 1536,
		    "ExitCode": 0,
		    "Error": "",
		    "StartedAt": "2018-05-18T14:27:36.756656157Z",
		    "FinishedAt": "2018-05-18T14:27:06.389591103Z"
		},
		"Image": "sha256:bd722b6a550b3a3fe668d5b1ac0a58c5ca0fc7358a00a94b23c90843ad355435",
		"ResolvConfPath": "/var/lib/docker/containers/ecde063fb19c461fa93af1684ae1755a0e081ddfc6efb303e6b3e6c6a5e313a6/resolv.conf",
		"HostnamePath": "/var/lib/docker/containers/ecde063fb19c461fa93af1684ae1755a0e081ddfc6efb303e6b3e6c6a5e313a6/hostname",
		"HostsPath": "/var/lib/docker/containers/ecde063fb19c461fa93af1684ae1755a0e081ddfc6efb303e6b3e6c6a5e313a6/hosts",
		"LogPath": "/var/lib/docker/containers/ecde063fb19c461fa93af1684ae1755a0e081ddfc6efb303e6b3e6c6a5e313a6/ecde063fb19c461fa93af1684ae1755a0e081ddfc6efb303e6b3e6c6a5e313a6-json.log",
		"Name": "/WebLogic",
		"RestartCount": 0,
		"Driver": "overlay2",
		"Platform": "linux",
		"MountLabel": "",
		"ProcessLabel": "",
		"AppArmorProfile": "",
		"ExecIDs": null,
		"HostConfig": {
		    "Binds": null,
		    "ContainerIDFile": "",
		    "LogConfig": {
		        "Type": "json-file",
		        "Config": {}
		    },
		    "NetworkMode": "default",
		    "PortBindings": {
		        "7021/tcp": [
		            {
		                "HostIp": "",
		                "HostPort": "7022"
		            }
		        ]
		    },
		    "RestartPolicy": {
		        "Name": "no",
		        "MaximumRetryCount": 0
		    },
		    "AutoRemove": false,
		    "VolumeDriver": "",
		    "VolumesFrom": null,
		    "CapAdd": null,
		    "CapDrop": null,
		    "Dns": [],
		    "DnsOptions": [],
		    "DnsSearch": [],
		    "ExtraHosts": null,
		    "GroupAdd": null,
		    "IpcMode": "shareable",
		    "Cgroup": "",
		    "Links": null,
		    "OomScoreAdj": 0,
		    "PidMode": "",
		    "Privileged": false,
		    "PublishAllPorts": false,
		    "ReadonlyRootfs": false,
		    "SecurityOpt": null,
		    "UTSMode": "",
		    "UsernsMode": "",
		    "ShmSize": 67108864,
		    "Runtime": "runc",
		    "ConsoleSize": [
		        0,
		        0
		    ],
		    "Isolation": "",
		    "CpuShares": 0,
		    "Memory": 0,
		    "NanoCpus": 0,
		    "CgroupParent": "",
		    "BlkioWeight": 0,
		    "BlkioWeightDevice": [],
		    "BlkioDeviceReadBps": null,
		    "BlkioDeviceWriteBps": null,
		    "BlkioDeviceReadIOps": null,
		    "BlkioDeviceWriteIOps": null,
		    "CpuPeriod": 0,
		    "CpuQuota": 0,
		    "CpuRealtimePeriod": 0,
		    "CpuRealtimeRuntime": 0,
		    "CpusetCpus": "",
		    "CpusetMems": "",
		    "Devices": [],
		    "DeviceCgroupRules": null,
		    "DiskQuota": 0,
		    "KernelMemory": 0,
		    "MemoryReservation": 0,
		    "MemorySwap": 0,
		    "MemorySwappiness": null,
		    "OomKillDisable": false,
		    "PidsLimit": 0,
		    "Ulimits": null,
		    "CpuCount": 0,
		    "CpuPercent": 0,
		    "IOMaximumIOps": 0,
		    "IOMaximumBandwidth": 0
		},
		"GraphDriver": {
		    "Data": {
		        "LowerDir": "/var/lib/docker/overlay2/521b4d30e8458923d4af51b0ae1666f65e646f21181cb9da026760bb02c2ca39-init/diff:/var/lib/docker/overlay2/8ed6a80c2f3287260d2f71c03b08413dcd4f4f3940943883b5557dc66622eb21/diff:/var/lib/docker/overlay2/d9dea1e51d1686cacb0ac36f2c7f0973242b354f89700690f49624eb8d260d68/diff:/var/lib/docker/overlay2/4575ddf5565c3d0fa6463719c70ee10de819ea6648fed748ae420037c330f388/diff:/var/lib/docker/overlay2/30e190cf9299a38524bddf7453072fcf195574e0d2da5429fcc251b2e8e5e703/diff:/var/lib/docker/overlay2/097c2a68acb056a5697133a7bad8312467461675c52670d3186f79fa1f57ce21/diff:/var/lib/docker/overlay2/cbe5f0d998a78c2de3f55b9c7e4e7f249bd0e70fed933283a722af495013bde2/diff:/var/lib/docker/overlay2/1d7652cca1780b949aaec8bf7dc5449ea030296ae7493c6ef4cc8ffa30527e2b/diff:/var/lib/docker/overlay2/05188f180773d27b6fdd75827936bacd240df6c13e2411fdbdd629c00aca923d/diff:/var/lib/docker/overlay2/4f8d615a5850d16abe2335b618d97d6c94da62f293beb5ece27432790f447907/diff:/var/lib/docker/overlay2/28dad173d42c9c6eb84938c7787591fa8a8f30f0adb78932cd62545348bb1fe0/diff:/var/lib/docker/overlay2/f5b58377500d81e51bba9d39683b6ad019086dcdd256643a2c89b77acb7f9dd0/diff:/var/lib/docker/overlay2/9f4cf3c9fdf84f4d97011e58f05bfc19c61b64751dcc9c976e3c22c224235eef/diff:/var/lib/docker/overlay2/9182f065c32341f91fef8344b58e792edb22f2c92b3b92be4ebe440385f5cb55/diff:/var/lib/docker/overlay2/2c5d1430df8cb85527c71717431fdd3b90c3193f7890a3c5a6fe3b22453d1254/diff:/var/lib/docker/overlay2/d217b9af1ce2e35dd78ab7e670efd8bb00ee342fb766213b3b3cf29d4d9b4747/diff:/var/lib/docker/overlay2/2c9ce3d6ff761468554df147263d56f489e907f841fb65da9f808a303c72825a/diff:/var/lib/docker/overlay2/4b5fb1144fcacc79c59cfdce34eb718dee60b433228c1feafa7977a792d57b62/diff:/var/lib/docker/overlay2/e1f85f1cb3f4fe39384e3a6e48514acc61e32640164f20713484ea3984792edd/diff:/var/lib/docker/overlay2/586f8eec2d52d6c148a0ec309f81c1254a4b1caeb166b57526d9d2a80d77f237/diff:/var/lib/docker/overlay2/463e2e94c10677fd3342a15f294c13ca56c7368fd2f46d2b21636b59c5d96b4d/diff:/var/lib/docker/overlay2/6fdf702988f6e244ef7a9ecb75b3016eb496c9ce55bcf39bc400b9d96c444b91/diff:/var/lib/docker/overlay2/c7cad16d39855867fed80bc099ac743bf98a621b930ae29e6e180d77a977cd5b/diff:/var/lib/docker/overlay2/fffa2447a0bff823d0b0290de03c934ec622da56981bc70c662c26da2a36dbaa/diff:/var/lib/docker/overlay2/d9cb6ee5bde2d00736df400da9897dcb14a927e2f435580f398aa391d30a62b4/diff:/var/lib/docker/overlay2/4d422300a9d525512f029b9271fd01982c7024e516ee408609dad5442aa03448/diff:/var/lib/docker/overlay2/005141ab2c077600a40479fafdb07d19e1ceeec96f4fa37675a0092af58f7cb9/diff:/var/lib/docker/overlay2/94e20194cb8347f0b3da69bdbbd4d004241f69485f98a08e621ecd3826fb9ff9/diff:/var/lib/docker/overlay2/c7ee37000b449ce9bbc65c03c0f8fa03e5735b548c43fcc76460bee73a3c8933/diff:/var/lib/docker/overlay2/faaf32bdc82b7accdb1e152dd1539d706a9e33939943922d5430257b15a74363/diff:/var/lib/docker/overlay2/3663781180b74a8a73e59080cada4ffd26e9ca2a17a589b22bf006cbcedb788f/diff:/var/lib/docker/overlay2/344b15ec87ea34b5ece8f746107d2a944351c5835561613402779c7fc7db6c94/diff:/var/lib/docker/overlay2/fb9d7eb8a05600e74cbdd603b7f0c634f2f73ec41f203d5e909e44fe5e222ae2/diff",
		        "MergedDir": "/var/lib/docker/overlay2/521b4d30e8458923d4af51b0ae1666f65e646f21181cb9da026760bb02c2ca39/merged",
		        "UpperDir": "/var/lib/docker/overlay2/521b4d30e8458923d4af51b0ae1666f65e646f21181cb9da026760bb02c2ca39/diff",
		        "WorkDir": "/var/lib/docker/overlay2/521b4d30e8458923d4af51b0ae1666f65e646f21181cb9da026760bb02c2ca39/work"
		    },
		    "Name": "overlay2"
		},
		"Mounts": [
		    {
		        "Type": "volume",
		        "Name": "2d2f5bdc92ea056ddc8dbaf54fed2db5b4c1d709e2a045d8862618ec8c049e54",
		        "Source": "/var/lib/docker/volumes/2d2f5bdc92ea056ddc8dbaf54fed2db5b4c1d709e2a045d8862618ec8c049e54/_data",
		        "Destination": "/scm",
		        "Driver": "local",
		        "Mode": "",
		        "RW": true,
		        "Propagation": ""
		    }
		],
		"Config": {
		    "Hostname": "ecde063fb19c",
		    "Domainname": "",
		    "User": "oracle",
		    "AttachStdin": false,
		    "AttachStdout": false,
		    "AttachStderr": false,
		    "ExposedPorts": {
		        "7021/tcp": {},
		        "7022/tcp": {}
		    },
		    "Tty": true,
		    "OpenStdin": true,
		    "StdinOnce": false,
		    "Env": [
		        "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
		        "container=docker",
		        "export=PATH=/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
		    ],
		    "Cmd": [
		        "/scm//scripts/startWebLogic.sh"
		    ],
		    "ArgsEscaped": true,
		    "Image": "weblogic",
		    "Volumes": {
		        "/scm": {}
		    },
		    "WorkingDir": "",
		    "Entrypoint": null,
		    "OnBuild": null,
		    "Labels": {
		        "org.label-schema.schema-version": "= 1.0     org.label-schema.name=CentOS Base Image     org.label-schema.vendor=CentOS     org.label-schema.license=GPLv2     org.label-schema.build-date=20180402"
		    }
		},
		"NetworkSettings": {
		    "Bridge": "",
		    "SandboxID": "812cadc8c07be5224644c09a8f797421dd0a112fceb8dc1d158e7b20e248e5c3",
		    "HairpinMode": false,
		    "LinkLocalIPv6Address": "",
		    "LinkLocalIPv6PrefixLen": 0,
		    "Ports": {
		        "7021/tcp": [
		            {
		                "HostIp": "0.0.0.0",
		                "HostPort": "7022"
		            }
		        ],
		        "7022/tcp": null
		    },
		    "SandboxKey": "/var/run/docker/netns/812cadc8c07b",
		    "SecondaryIPAddresses": null,
		    "SecondaryIPv6Addresses": null,
		    "EndpointID": "af67c5a4f71b7f30af652cf223834b84d1f09d5935a821111a8304073c7a84a9",
		    "Gateway": "172.17.0.1",
		    "GlobalIPv6Address": "",
		    "GlobalIPv6PrefixLen": 0,
		    "IPAddress": "172.17.0.2",
		    "IPPrefixLen": 16,
		    "IPv6Gateway": "",
		    "MacAddress": "02:42:ac:11:00:02",
		    "Networks": {
		        "bridge": {
		            "IPAMConfig": null,
		            "Links": null,
		            "Aliases": null,
		            "NetworkID": "ad51c36b3512171f158fa177ee8f248d166a992cc8926dc7dc862f03631fc880",
		            "EndpointID": "af67c5a4f71b7f30af652cf223834b84d1f09d5935a821111a8304073c7a84a9",
		            "Gateway": "172.17.0.1",
		            "IPAddress": "172.17.0.2",
		            "IPPrefixLen": 16,
		            "IPv6Gateway": "",
		            "GlobalIPv6Address": "",
		            "GlobalIPv6PrefixLen": 0,
		            "MacAddress": "02:42:ac:11:00:02",
		            "DriverOpts": null
		        }
		    }
		}
	    }
	]
	[oracle@srvdocker01 consis]$ 



Listo podemos abrir un navegador y verificar que ya el Weblogic esta operativo
	http://srvdocker01:7022/console

Realizamos el Despliegue de la aplicacion CONSIS, las entonaciones de los pool de Datasource y podemos ir a la URL
	http://srvdocker01:7022/WController



::

	[oracle@srvdocker01 consis]$ docker stop WebLogic && docker rm WebLogic
	WebLogic
	WebLogic
	[oracle@srvdocker01 consis]$ 

::

	[oracle@srvdocker01 consis]$ docker rmi fd40a4b4601f bd722b6a550b 10e84e7d6d57
	Untagged: weblogic:12.2.1.3.0
	Deleted: sha256:fd40a4b4601f9c9e29ecb99dd959766b9ff99ef42394103c31fcfe25176f5c22

::

	[oracle@srvdocker01 consis]$ docker volume rm $(docker volume ls -qf dangling=true)
	2d2f5bdc92ea056ddc8dbaf54fed2db5b4c1d709e2a045d8862618ec8c049e54


