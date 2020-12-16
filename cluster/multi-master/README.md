# Multi Master

## Version
```
ElasticSearch: 7.6.1
Kibana: 7.6.1
```

## Run
### Example
|host name|node.name|host ip|master|data|
|:-:|:-:|:-:|:-:|:-:|
|pdk1|es01|10.1.110.1|true|true|
|pdk2|es02|10.1.110.2|true|true|
|pdk3|es03|10.1.110.3|true|true|

please modify the network.publish_host, discovery.seed_hosts in docker-compose.yml to match your host IP

### In pdk1 host
modify docker-compose.yml
```
...
es01:
  ...
  environment:
    - network.publish_host=10.1.110.1
    - discovery.seed_hosts=10.1.110.2,10.1.110.3
    - node.master=true
    - node.data=true
...
```
run container es01, kib01
```
$ sudo docker-compose up es01 kib01
```

### In pdk2 host
modify docker-compose.yml
```
...
es02:
  ...
  environment:
    - network.publish_host=10.1.110.2
    - discovery.seed_hosts=10.1.110.1,10.1.110.3
    - node.master=true
    - node.data=true
...
```
run container es02
```
$ sudo docker-compose up es02
```

### In pdk3 host
modify docker-compose.yml
```
...
es03:
  ...
  environment:
    - network.publish_host=10.1.110.3
    - discovery.seed_hosts=10.1.110.1,10.1.110.2
    - node.master=true
    - node.data=true
...
```
run container es03
```
$ sudo docker-compose up es03
```


