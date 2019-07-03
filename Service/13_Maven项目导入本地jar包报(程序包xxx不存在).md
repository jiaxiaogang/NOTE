> 说明:本问题在eclipse下,的spring+maven项目下;
> 1. 导入包后,maven不报错,但只要引入jar中的类就报错;
> 2. 导入包后,如果另建一个main()引入jar中的类,则不报错;
> 3. 导入包后,并引入jar中的类时,maven clean -> maven install就报错;错误信息为:(程序包xxx不存在)

1. 将local.jar放到项目目录下:`{projectPath}/WebContent/WEB-INF/lib`
2. 点项目右键-properties-JavaBuildPath-Libraries-AddJARs;
3. 弹出窗,选择"/WebContent/WEB-INF/lib/local.jar",并点击确定-ApplyAndClose;
4. 打开pom.xml,加入下图红框中代码,到plugins下即可:

| ![](assets/13_Maven项目导入本地jar包报(程序包xxx不存在)-2314f8a3.png) |
| --- |
| 注:在compilerArguments中,指定了本地jar目录; |

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <version>3.0</version>
  <configuration>
  	<source>1.7</source>
  	<target>1.7</target>
  	<encoding>UTF-8</encoding>
      <compilerArguments>
          <extdirs>${project.basedir}/WebContent/WEB-INF/lib</extdirs>
      </compilerArguments>
  </configuration>
</plugin>
```
