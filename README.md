
first step:
docker create \
   -v /opt/prometheus/data \
   -v /opt/consul-data \
   -v /var/lib/mysql \
   -v /var/lib/grafana \
   --name pmm-data \
   percona/pmm-server:latest /bin/true

second step: 
docker run -d \
  -p 81:80 \
  --volumes-from pmm-data \
  --name pmm-server \
  --restart always \
  percona/pmm-server:latest

remove pmm-server container:

  docker stop pmm-server_container

  docker rm pmm-server_container

after that сopy volumes files from pmm-data container to host:

copy prometheus data:

  docker cp id_pmm-data_container:/opt/prometheus/ /your/prometheus/data/on/host

copy consul data:

  docker cp id_pmm-data_container:/opt/consul-data/ /your/consul/data/on/host

copy mysql data:

  docker cp id_pmm-data_container:/var/lib/mysql /your/mysql/data/on/host

copy grafana data:

  docker cp id_pmm-data_container:/var/lib/grafana /your/grafana/data/on/host

after thatneed delete pmm-data container:
  docker rm pmm-data_container
