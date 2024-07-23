# presto-lab-setup
Instructions for setting up Presto Java and Presto C++ with docker compose and running pbench


# Presto Benchmarking Setup

This guide will help you set up and run Presto benchmarks using PrestoDB and PBench.

## Prerequisites

- Git
- Docker
- Docker Compose

## Setup

1. Clone the required repositories:

```bash
git clone https://github.com/prestodb/prestorials.git
git clone https://github.com/prestodb/pbench.git
```

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
