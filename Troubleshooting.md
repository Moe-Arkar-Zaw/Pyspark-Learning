## 1. Quick Spark Java Error Fix

Environment: Windows, Pyspark 4.x, JDK 17 

Error: PySparkRuntimeError: [JAVA_GATEWAY_EXITED] Java gateway process exited before sending its port number.

Cause: 
Spark cannot start java
JAVA_HOME is missing
Java not installed corrrectly 

Solution:
1. install JDK 17 on Oracle Website
2. Set: 
setx JAVA_HOME "D:\Program Files\jdk-17"
setx PATH "%JAVA_HOME%\bin;%PATH%"
3. Reopen terminal and check: java --version

Note: Note:
This is usually a Java setup issue, not a Python/PySpark code bug.