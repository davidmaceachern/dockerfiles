## docker-elasticsearch-arm
### 测试验证
> 请根据自己需求修改configure目录下的配置文件
```bash
[root@arm~]$ sudo docker build -t elasticsearch:6.2.3 . 
[root@arm~]$ sudo docker run -idt -p 9200:9200 elasticsearch:6.2.3
[root@arm~]$ sudo docker ps
[root@arm~]$ curl http://localhost:9200  
{
  "name" : "_ZribmL",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "Kwnp_xC5RQ-cArpqj4I3GA",
  "version" : {
    "number" : "6.2.3",
    "build_hash" : "c59ff00",
    "build_date" : "2018-03-13T10:06:29.741383Z",
    "build_snapshot" : false,
    "lucene_version" : "7.2.1",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}

```