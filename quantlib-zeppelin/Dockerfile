FROM apfadler/quantlib-java
MAINTAINER Andreas Pfadler <andreas.pfadler@gmail.com>
LABEL Description="An environment with the QuantLib Java module and Apache Zeppelin notebook"

RUN apt-get update && apt-get install -y maven

RUN ls && git clone https://github.com/apfadler/incubator-zeppelin.git \
    && cd incubator-zeppelin \
	&& git checkout branch-0.5.5  \
	&& mvn clean package -DskipTests -Dignite.version=1.6.0 -Pbuild-distr \
    && cp /incubator-zeppelin/zeppelin-distribution/target/zeppelin-0.5.5-incubating*gz / \
    && cd / && tar zxfv zeppelin*gz &&  mv zeppelin-0.5.5-incubating zeppelin && rm /zeppelin*gz \
    && mkdir -p /zeppelin/notebook && rm -rf /incubator-zeppelin
	
COPY libs/server-0.1-SNAPSHOT.jar /zeppelin/interpreter/ignite/server-0.1-SNAPSHOT.jar

COPY libs/common-0.1-SNAPSHOT.jar /zeppelin/interpreter/ignite/common-0.1-SNAPSHOT.jar

COPY libs/interpreter-0.1-SNAPSHOT.jar /zeppelin/interpreter/ignite/interpreter-0.1-SNAPSHOT.jar

COPY libs/qlobjects-0.1-SNAPSHOT.jar /zeppelin/interpreter/ignite/qlobjects-0.1-SNAPSHOT.jar

COPY libs/scala-macros-0.1-SNAPSHOT.jar /zeppelin/interpreter/ignite/scala-macros-0.1-SNAPSHOT.jar

COPY libs/json4s-ast_2.11-3.3.0.jar /zeppelin/interpreter/ignite/json4s-ast_2.11-3.3.0.jar

COPY libs/json4s-core_2.11-3.3.0.jar /zeppelin/interpreter/ignite/json4s-core_2.11-3.3.0.jar

COPY libs/json4s-native_2.11-3.3.0.jar /zeppelin/interpreter/ignite/json4s-native_2.11-3.3.0.jar

COPY libs/json4s-scalap_2.11-3.3.0.jar /zeppelin/interpreter/ignite/json4s-scalap_2.11-3.3.0.jar

COPY libs/json-simple-1.1.1.jar /zeppelin/interpreter/ignite/json-simple-1.1.1.jar

COPY libs/spray-json_2.10-1.3.2.jar /zeppelin/interpreter/ignite/spray-json_2.10-1.3.2.jar

COPY libs/quantlib-1.7.jar /zeppelin/interpreter/ignite/quantlib-1.7.jar

COPY interpreter.json /zeppelin/conf/interpreter.json

COPY quil-common.xml /zeppelin/quil-common.xml

COPY quil-client.xml /zeppelin/quil-client.xml

COPY quil-server.xml /zeppelin/quil-server.xml

CMD cd /zeppelin && JAVA_OPTS=" -DIGNITE_QUIET=false " LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib:/usr/local/lib bin/zeppelin-daemon.sh start && top -b


