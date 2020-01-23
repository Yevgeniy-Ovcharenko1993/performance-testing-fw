Performance testing project framework for performance testing with dashboard plugins for Grafana 
- application side metrics 
- server side metrics 

Full configuration: 
- Add https://github.com/NovaTecConsulting/JMeter-InfluxDB-Writer/releases plugin to jmeter 
- Download the Plugins Manager JAR file and put it into JMeter's lib/ext directory. https://jmeter-plugins.org/wiki/PluginsManager/
- Run jmeter 
- Add BackEnd listener 
- Choose the rocks.nt.apm.jmeter.JMeterInfluxDBBackendListenerClient in Backend listener implementation drop down list 
- configure your data-writting 
    1. influxdbUrl http://host_to_change:8086/write?db=<ACTUAL_DB_NAME> needs to be created before running Jmeter scenario 
    2. measurement <YOUR_OWN_NAME> creates automatically on start up Jmeter scenario 
- create Jmeter scenario 
- open the src folder and run docker-compose up (wait for running services)
- create databasee in InfluxDB by executing the command curl -i -XPOST http://localhost:8086/query --data-urlencode "q=CREATE DATABASE <DATABASE_NAME>"
- Open Grafana on http://localhost:3000/ and login 
- Open Datasources and add InfluxDB if NOT EXISTS
- Configure InfluxDB datasource to your created Database 
- Import JMeter Load Test plugin 
- Open Jmeter Load Test dashboard 
- Run Jmeter scenario 
- Check metrics in Dashboard 

If you want to check server side metrics (in this case it's local config) you should execute the following commands: 
- docker pull telegraf 
- docker run --net=container: influxDbContainerID telegraf
- open influxDB datasources and change db name from current to (telegraf) 
- Import the https://grafana.com/dashboards/928 dashboard into grafana 
- Open dashboard and check metrics 