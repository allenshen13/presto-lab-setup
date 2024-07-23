# presto-lab-setup
Instructions for setting up Presto Java and Presto C++ with docker compose and running pbench


# Presto Benchmarking Setup

This guide will help you set up and run Presto benchmarks using PrestoDB and PBench.

## Prerequisites

- Git
- Docker
- Docker Compose

## Setup

1. Pull the required images first to allow time for downloading

```bash
docker pull prestodb/presto:latest
docker pull public.ecr.aws/oss-presto/presto-native:0.289-ubuntu-arm64
```

2. Clone the required repositories

```bash
git clone https://github.com/prestodb/prestorials.git
git clone https://github.com/prestodb/pbench.git
```

3. Download the dataset [here]()

4. Copy the downloaded zip file to both of the following directories and unzip the file in each:
```
prestorials/docker-compose/data
prestorials/docker-compose-native/prestissimo/data
```
This should result in the `tpcds` and `tpch` directories being created in the `/data` directories.
The zip file can then be deleted from the `/data` directories.

### Running Presto Java
```bash
cd prestorials/docker-compose
docker compose -v -f docker-compose-arm64.yaml up
```

### Running Presto C++
```bash
cd prestorials/docker-compose-native
docker compose -v -f docker-compose-arm64.yaml up
```

### Using Presto CLI to run queries manually
After deploying a Presto cluster and confirming that the server started, run the Presto CLI from the coordinator container: 
```bash
docker exec -it coordinator /opt/presto-cli --server http://127.0.0.1:8080 
```
While in Presto CLI, verify that the schemas exist and use hive.tpcds for example:
```sql
SHOW schemas in hive;
USE hive.tpcds;
SHOW tables;
```


## Using the pbench tool
```bash
cd path/to/pbench
make all
./pbench run benchmarks/tpc-ds/sf1.json benchmarks/tpc-ds/ds_power.json
```

