# hive installation #
## 1. install hadoop in advance ##
1. download hadoop  
	[http://www.apache.org/dyn/closer.cgi/hadoop/common](http://www.apache.org/dyn/closer.cgi/hadoop/common "hadoop download")  
	*we need to run hadoop in windows, we have to hadooponwindows-master.zip, and this zip file support 2.7.3 hadoop, so we select hadoop 2.6.5 to install.*.
2. uncompress hadoop  
	uncompress hadoop to a directory you want as ***HIVE_HOME***. for example, *d:\hadoop_2.5.6*.
3. replace bin and etc of hadoop  
	1. because native hadoop does not support windows, you have to download ***hadooponwindows-master.zip*** which is included in this project.
	2. uncompress ***hadooponwindows-master.zip***
	3. overwrite ***HIVE_HOME***\bin and ***HIVE_HOME***\lib using ***hadooponwindows-master.zip***.
4. config env variables  
	1. config ***JAVA_HOME***
	2. add ***JAVA_HOME***\bin to `path` env variable.
	3. config ***HADOOP_HOME***. For example, *d:\hadoop_2.5.6*.
	4. add HADOOP_HOME\bin to `path` env variable.
5. config jdk path in hadoop env  
	open ***HADOOP_HOME***\etc\hadoop\hadoop-env.cmd and find `set JAVA_HOME`, and set this to you own env value. If there is `Program Files` in ***JAVA_HOME***, replace it using `PROGRA~1`.
6. confirm hadoop version  
	After above steps, prompt `hadoop version` in command line windows, then hadoop version inforamtion will be shown.
7. confirm hadoop config xml files
	1. ***HADOOP_HOME***/etc/hadoop/core-site.xml  
		    `<configuration>  
    			<property>  
    				<name>fs.defaultFS</name>  
					<value>hdfs://localhost:9000</value>    
    			</property>  
    		</configuration>`
	2. ***HADOOP_HOME***/etc/hadoop/mapred-site.xml
			`<configuration>   
				<property>       
					<name>mapreduce.framework.name</name>       
					<value>yarn</value>   
				</property>
			</configuration>`
	3. ***HADOOP_HOME***/etc/hadoop/hdfs-site.xml  
		set your own directory to `dfs.namenode.name.dir` and `dfs.datanode.data.dir`.
		`<configuration>
			<property>       
				<name>dfs.replication</name>       
				<value>1</value>   
			</property>   
			<property>       
				<name>dfs.namenode.name.dir</name>       
				<value>/E:/hadoop-2.7.3/namenode</value>   
			</property>   
			<property>       
				<name>dfs.datanode.data.dir</name>     
				<value>/E:/hadoop-2.7.3/datanode</value>   
			</property>
		</configuration>`
	4. ***HADOOP_HOME***/etc/hadoop/yarn-site.xml  
		`<configuration>   
			<property>       
				<name>yarn.nodemanager.aux-services</name>       
				<value>mapreduce_shuffle</value>   
			</property>   
			<property>       
				<name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>       
				<value>org.apache.hadoop.mapred.ShuffleHandler</value>   
			</property>
		</configuration>`
8. start hadoop service.
	1. create three directories.  
		-***HADOOP_HOME***  \tmp
		-***HADOOP_HOME***  \datanode  
		-***HADOOP_HOME***  \namenode 
	2.  format hdfs  
		`hdfs namenode -format` in command line with admin user.
	3. go into ***HADOOP_HOME***\sbin.
	4. execute `start-all.cmd`.
9. these above steps are referred by following url.  
	[https://blog.csdn.net/csdn_fzs/article/details/78985586](https://blog.csdn.net/csdn_fzs/article/details/78985586 "hadoop guide")
## 2. install hive ##
1. set &amp;serverTimezone=UTC to `<name>javax.jdo.option.ConnectionURL</name>`
2. set hive db to latin1.
3. execute `schematool -dbType mysql -initSchema` before creating table.