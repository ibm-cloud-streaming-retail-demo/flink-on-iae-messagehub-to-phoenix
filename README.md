# flink-on-iae-messagehub-to-phoenix

### Write kafka data to phoenix on IAE

```
//String query = "select CURRENT_DATE SEGMENTSTARTTIME, CURRENT_DATE SEGMENTENDTIME, cast (imsi as varchar) imsi, cast(imei as varchar) imei from ts ";
//Table table = ste.sqlQuery(query);

// Table table = from kafka?

JDBCAppendTableSinkBuilder jdbc = JDBCAppendTableSink.builder();
jdbc.setDrivername("org.apache.phoenix.jdbc.PhoenixDriver");
jdbc.setDBUrl("jdbc:phoenix:hosts:2181:/hbase-unsecure;autocommit=true");
jdbc.setQuery("upsert INTO GEO_ANALYTICS_STREAMING_DATA (SEGMENTSTARTTIME,SEGMENTENDTIME, imsi, imei) values (?,?,?, ?)");
jdbc.setParameterTypes(Types.SQL_DATE, Types.SQL_DATE, Types.STRING, Types.STRING);
JDBCAppendTableSink sink = jdbc.build();
table.writeToSink(sink);
```

Source: https://issues.apache.org/jira/browse/FLINK-8356?jql=project%20%3D%20FLINK%20AND%20text%20~%20hbase%20and%20text%20~%20sink

### Query from hive (not all reporting tools support phoenix)

https://hortonworks.com/blog/hbase-hive-better-together/

### Export to COS for access by other wdp tools

Refinery Hive connector?  IAE Spark job? 
