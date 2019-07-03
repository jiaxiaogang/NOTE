> 问题起源: 本地jar一般都不在target目录下,而很多服务端仅更新target目录运行;
> 这导致,到服务端运行时,会显示找不到类;从而报错;

1. 在pom.xml中加入如下代码段:
2. 将start和end间的xml插入到plugns标签下;
3. 解决问题,此时maven clean再maven install,可发现已经将local.jar复制到了target指定目录下;

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
	xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<modelVersion>4.0.0</modelVersion>
  ...
	<dependencies>
		...
	</dependencies>

	<build>
    ...
		<plugins>
      //start-------------------------------------------
			<!-- 用antRun把jar复制到target目录下的lib目录下 -->
			<plugin>
			    <artifactId>maven-antrun-plugin</artifactId>
			    <executions>
			        <execution>
			            <phase>install</phase>
			            <goals>
			                <goal>run</goal>
			            </goals>
			            <configuration>  
			                <tasks>  
			                    <echo message="********************copy profile propertie file *************************"/>
			                     <copy file="WebContent/WEB-INF/lib/local-1.0-SNAPSHOT.jar"
			                           tofile="${project.build.directory}/your-project-name/WEB-INF/lib/local-1.0-SNAPSHOT.jar" overwrite="true"/>
			                </tasks>
			            </configuration>  
			        </execution>
			    </executions>  
			</plugin>
      //end-------------------------------------------
			...
</project>
```

> 注:
> 1. 以上xml,在antrun下,有一个phase; (无phase的话,是不会执行的)
> 2. 在phase下,有一个goals (无goals的话,phase是无意义的)
> 3. 在tasks下,打出echo日志,并将local.jar复制到target下的xxx/lib/文件夹下;
