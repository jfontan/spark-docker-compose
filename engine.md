
* Build docker files

```
./build_images.sh
```

* Start containers with:

```
docker-compose up -d
```

* Set environment for HDFS client:

```
export HADOOP_NAMENODE=localhost:9000
export HADOOP_USER_NAME=root
```

* Install go hadoop client (you can use hadoop client instead):

```
go get -u github.com/colinmarc/hdfs/...
```

* Copy some files to HDFS:

```
hdfs put siva-files /
```

* Create a directory with a file named `core-site.xml` that contain hdfs configuration:

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License. See accompanying LICENSE file.
-->

<!-- Put site-specific property overrides in this file. -->

<configuration>
<property>
  <name>fs.default.name</name>
  <value>hdfs://172.17.0.1:9000</value>
</property>
</configuration>
```

* Move to engine directory and start spark shell:

```
HADOOP_CONF_DIR=/my/directory spark-shell --jars target/engine-uber.jar --conf spark.tech.sourced.bblfsh.grpc.host=172.17.0.1 --master spark://172.17.0.1:7077
```




