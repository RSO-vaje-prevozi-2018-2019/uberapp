# RSO: Customers microservice

## Prerequisites

```bash
docker run -d --name pg-customers -e POSTGRES_USER=dbuser -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=customer -p 5432:5432 postgres:10.5
```

#### Local etcd
```bash
docker run -d -p 2379:2379 --name etcd --volume=/tmp/etcd-data:/etcd-data quay.io/coreos/etcd:latest /usr/local/bin/etcd --name my-etcd-1 --data-dir /etcd-data --listen-client-urls http://0.0.0.0:2379 --advertise-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-advertise-peer-urls http://0.0.0.0:2380 --initial-cluster my-etcd-1=http://0.0.0.0:2380 --initial-cluster-token my-etcd-token --initial-cluster-state new --auto-compaction-retention 1   -cors="*"
 ```
    
##### Local build and run image
```bash
docker build -t uberapp-XXservice-nameXX-img .
```

```bash
docker run -p 808X:808X --env KUMULUZEE_CONFIG_ETCD_HOSTS=http://etcd:2379 --env KUMULUZEE_DISCOVERY_ETCD_HOSTS=http://etcd:2379 --name XXservice-nameXX uberapp-XXservice-nameXX-img
```

#### Etcd settings
```bash
docker exec etcd etcdctl --endpoints //192.168.99.100:2379 set /environments/dev/services/uberapp-reviews/1.0.0/config/app-properties/enable-notifications true

```

## Ports
* Users:8080
* Rides:8081
* Reviews:8082
* Notifications:8083
* Chat:8084 (still in development)
* RideManagement:8085 (still in development)

## 
