# Livy Docker image
Start by building a binary distribution :
```
mvn -U clean package -DskipITs -DskipTests -P targz
```
Copy the generated artifact to the docker context directory :
```
cp assembly/target/livy-0.5.0-incubating-SNAPSHOT-bin.tar.gz docker/
```
Build the docker image :
```
docker build -t talend/livy:0.5.0-SNAPSHOT .
```
Start Livy container  :
```
docker run -p 8998:8998 -d talend/livy:0.5.0-SNAPSHOT
```
Run a smoke test :
```
curl -X POST --data '{"file": "/opt/spark/examples/spark-pi-example.jar", "className": "org.apache.spark.examples.SparkPi"}' -H "Content-Type: application/json" localhost:8998/batches
```
Then go to http://localhost:8998/

# TODO
- Replace manual copy and build by https://github.com/spotify/dockerfile-maven to integrate the docker image build with the Maven lifecycle
