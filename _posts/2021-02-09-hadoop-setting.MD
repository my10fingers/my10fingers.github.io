---
layout: post
title:  "HADOOP Setting"
author: Yi MoonSeok
date:   2021-02-09 16:50:28
categories: Post
---
HADOOP 설치 정리

1. Java 설치
   + Open JDK 11 설치

        ```Bash
        prompt> java -version
        openjdk version "11.0.10" 2021-01-19
        OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.10+9)
        OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.10+9, mixed mode)
        ```

2. 변수 설정 (bash 등)
   + JAVA_HOME
   + HADOOP_HOME
   + HADOOP_CONFIG_HOME
  
3. Hadoop Download (https://archive.apache.org/dist)
   + Hive
   + Hadoop
   + Hbase
   + Spark
   + 기타 필요한 것들

4. Hadoop 설치 경로에 해제 및 디렉토리 생성
   + tar zxvf [파일]
   + mkdir temp
   + mkdir datanode
   + mkdir namenode

5. Hadoop Config 수정
   + hadoop-env.sh (option) 
        ```Bash
        # 추가
        export JAVA_HOME=[your installed java path]
        ```
   + core-site.xml
        ```Xml
        <property>
            <name>hadoop.tmp.dir</name>
            <value>[installed hadoop dir]/node/temp</value>
        </property>

        <property>
            <name>fs.default.name</name>
            <value>hdfs://localhost:9000</value>
        </property>
        ```
   + hdfs-site.xml
        ```Xml
        <property>
            <name>dfs.replication</name>
            <value>1</value>
            <final>true</value>
        <property>
        <property>
            <name>dfs.namenode.name.dir</name>
            <value>[installed hadoop dir]/node/namenode</value>
            <final>true</fifnal>
        </property>
        <property>
            <name>dfs.datanode.name.dir</name>
            <value>[installed hadoop dir]/node/datanode</value>
            <final>true</final>
        </property>
        ```
   + mapred-site.xml
        ```Xml
        <property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
        </proerty>
        <property>
            <name>mapred.job.tracker</name>
            <value>localhost:9001</value>
        </proerty>
        ```
   + yarn-site.xml
        ```Xml
        <property>
            <name>yarn.nodemanager.aux-services</name>
            <value>mapreduce_shuffle</value>
        </proerty>
        <property>
            <name>yarn.resourcemanager.address</name>
            <value>localhost:8032</value>
        </proerty>
        <property>
            <name>yarn.resourcemanager.scheduler.address</name>
            <value>localhost:8030</value>
        </proerty>
        <property>
            <name>yarn.resourcemanager.resource-tracker.address</name>
            <value>localhost:8031</value>
        </proerty>
        <property>
            <name>yarn.resourcemanager.admin.address</name>
            <value>localhost:8033</value>
        </proerty>
        <property>
            <name>yarn.resourcemanager.wepapp.address</name>
            <value>localhost:8088</value>
        </proerty>
        ```
6. namenode format
   ```Bash
   prompt> hdfs namenode -format
   ```

7. cluster 설정 시
   + hdfs-site.xml replicate를 node 갯수만큼 수정
   + hadoop_config 의 slave 파일에 node 목록(host 이름) 등록
   + /etc/hosts 에 node 들의 ip hostname 등록



(계속 업데이트 중)

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
