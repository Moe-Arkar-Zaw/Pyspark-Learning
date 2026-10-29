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

---
## 2. Quick Spark XLS / Seperator Fix

Environment: Windows, Pyspark, file named (sample.xls)

Error: "ValueError: Excel file format cannot be determined..."

Problem: Spark is reading the file with the wrong delimiter or assuming it is a real Exel file

Cause: 
-The file is a tab-seperated text file, not a valid excel workbook

Solution:
1. If the file is tab-seprated use
'df = spark.read.option("header", True).option("sep", "\t").csv("sample.xls")
df.show()'

Note:
1. .xls extension does not always mean it is a valid Excel file.
2. Always specify the actual separator or file format.

---
