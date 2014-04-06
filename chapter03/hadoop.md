##一、配置core-site.xml


	<configuration>
	        <property>
	                <name>fs.defaultFS</name>
	                <value>hdfs://cloud001:9000</value>
	        </property>
	
	        <property>
	                <name>io.file.buffer.size</name>
	                <value>131072</value>
	        </property>
	
	        <property>
	
	<configuration>
	        <property>
	                <name>fs.defaultFS</name>
	                <value>hdfs://cloud001:9000</value>
	        </property>
	
	        <property>
	                <name>io.file.buffer.size</name>
	                <value>131072</value>
	        </property>
	
	        <property>
	                <name>hadoop.tmp.dir</name>
	                <value>file:/home/hadoop/temp</value>
	        </property>
	
	        <property>
	
	                <name>hadoop.proxyuser.hduser.hosts</name>
	
	                <value>*</value>
	
	        </property>
	
	        <property>
	
	                <name>hadoop.proxyuser.hduser.groups</name>
	
	                <value>*</value>
	
	        </property>
	
	</configuration>

##二、

##三、错误解决
	File /in/file._COPYING_ could only be replicated to 0 nodes instead of minReplication (=1).  There are 0 datanode(s) running and no node(s) are excluded in this operation
	
	问题解决：
	
##四、hadoop清理回收站
	Hadoop回收站trash，默认是关闭的。 
	修改conf/core-site.xml,增加 
	<property>
	  <name>fs.trash.interval</name>
	  <value>3</value>
	  <description>Number of minutes between trash checkpoints.   If zero, the trash feature is disabled.  
	  </description>
	</property>
	
	默认是0.单位分钟。（PS：发现设置了这个值没什么作用，进行对一个文件删除后，等了一个早上回收站里面的那个文件依然存在）
	
	能在用户的垃圾桶中找回
	hadoop fs -ls /user/hadoop/.Trash/Current/
	
	删除.Trash目录（清理垃圾） 
	hadoop fs -rmr .Trash  