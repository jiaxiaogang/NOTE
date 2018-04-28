# 环境 >>

| 1. 安装jdk1.8 |
| --- |
| <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html> |
| ![](assets/导入ddgsService到eclipse记-29d065b8.png) |

| 2. 安装tomcat |
| --- |

| 3. 安装maven |  |
| --- | --- |
| title | 修改localRepository |
| path | maven/apache-maven-3.3.9/conf/setting.xml |
| 图 | ![](assets/导入ddgsService到eclipse记-d8012731.png) |
| title2 | 指定maven给eclipse |
| 图 | ![](assets/导入ddgsService到eclipse记-ad7293bc.png) |




<br><br><br><br><br>




| 步骤 >> |  |
| --- | --- |
| 1 | workspace定位到parent的父目录; ![](assets/导入ddgsService到eclipse记-8ccb4318.png) |
| 2 | ![](assets/导入ddgsService到eclipse记-c43423ab.png) |
| 3 | 导致maven项目,选择parent;![](assets/导入ddgsService到eclipse记-17bb95ed.png) |
| 4 | 将子项目,一个一个import as Project; ![](assets/导入ddgsService到eclipse记-d0714b4c.png) |





<br><br><br><br><br>






# 错误 >>

| 1 | Cannot change version of project facet Dynamic web module to 3.0 |
| --- | --- |
| 1改对应版本 | ![](assets/导入ddgsService到eclipse记-7c868937.png) |
| 2更新 | ![](assets/导入ddgsService到eclipse记-4746f388.png) |


| 2 | `Description	Resource	Path	Location	Type Java compiler level does not match the version of the in` 或 `'<>' operator is not allowed for source level below 1.7` |
| --- | --- |
| 1修改java版本 | ![](assets/导入ddgsService到eclipse记-30ce32b3.png) |
| 2更新 | ![](assets/导入ddgsService到eclipse记-4746f388.png) |


| 3 | Java compiler level does not match the version of the installed Java project facet. |
| --- | --- |
|  | ![](assets/导入ddgsService到eclipse记-cf2e8564.png) |
