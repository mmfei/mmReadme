#/usr/local/elasticsearch/bin/elasticsearch -d
#curl -XPUT 'http://localhost:9200/dept/employee/30' -d '{ "empname": "emp30"}'
#http://localhost:9200/_plugin/bigdesk/
#http://localhost:9200/_plugin/head/
#http://localhost:9200/_plugin/kopf/#!/cluster
./bin/plugin install medcl/elasticsearch-analysis-ik
./bin/plugin install mobz/elasticsearch-head
./bin/plugin install lmenezes/elasticsearch-kopf/1.2
