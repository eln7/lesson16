podman system reset

mysql_ssl_rsa_setup -d /opt/lesson16/cert/


docker run -d \
  -e MYSQL_ROOT_PASSWORD=root \
  -e CLUSTER_NAME=lesson16-cluster1 \
  --name=lesson16-node1 \
  --net=lesson16-network \
  -v /opt/lesson16/cert:/cert \
  -v /opt/lesson16/config:/etc/percona-xtradb-cluster.conf.d \
  percona/percona-xtradb-cluster:8.0

docker run -d \
  -e MYSQL_ROOT_PASSWORD=root \
  -e CLUSTER_NAME=lesson16-cluster1 \
  -e CLUSTER_JOIN=lesson16-node1 \
  --name=lesson16-node2 \
  --net=lesson16-network \
  -v /opt/lesson16/cert:/cert \
  -v /opt/lesson16/config:/etc/percona-xtradb-cluster.conf.d \
  percona/percona-xtradb-cluster:8.0

docker run -d \
  -e MYSQL_ROOT_PASSWORD=root \
  -e CLUSTER_NAME=lesson16-cluster1 \
  -e CLUSTER_JOIN=lesson16-node1 \
  --name=lesson16-node3 \
  --net=lesson16-network \
  -v /opt/lesson16/cert:/cert \
  -v /opt/lesson16/config:/etc/percona-xtradb-cluster.conf.d \
  percona/percona-xtradb-cluster:8.0