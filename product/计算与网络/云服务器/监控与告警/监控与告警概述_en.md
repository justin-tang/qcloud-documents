Provides Tencent Cloud CVMs with a good monitoring environment, in order to maintain high reliability, high availability and high performance for the most important parts of CVM instances. Users can easily collect different dimensions of monitoring data from different resources; this allows for an easy grasp of the use of these resources and location of faults.

Collecting monitoring data helps the user establish normal criteria for CVM instance performance. By measuring the performance of an instance and collecting monitoring data history at different times and under different load conditions, the user can clearly understand the normal performance of the instance and quickly determine whether the instance is in an abnormal state according to the current monitoring data; this will allow them to quickly find a solution to the problem. For example, users can monitor instances of CPU utilization, memory usage and disk I/O. If the instance performance is lower than normal at a certain time, you may need to trigger an alert to notify the user to upgrade the instance configuration or increase the number of instances, in order to reduce single instance loads and keep the system running smoothly.

To establish a normal performance baseline for a CVM instance, you should monitor at least the following:

| Monitoring item | Monitoring indicator | 
|---------|---------|
| CPU usage | cpu_usage | 
| Memory usage	 | mem_usage|
| Private network outgoing traffic | lan_outtraffic |
| Private network incoming traffic | lan_intraffic|
| Public network outgoing traffic	 | wan_outtraffic|
| WAN incoming traffic | wan_intraffic |
| Disk usage | disk_usage |
| Disk IO waiting time |disk_io_await	|

For more details on monitoring indicators, refer to [Cloud Monitoring Product Documentation](https://www.qcloud.com/doc/product/248).

Cloud monitoring collects raw data from running CVM instances and presents the data as an easy-to-read icon. By default, the statistics are saved for one month. You can view the operation status of an instance for one month to get a better understanding of the application service. By default, cloud monitoring collects operating data of an instance every 5 minutes; Tencent Cloud also has products that support a more detailed 1 minute granular monitoring.

The console of different products may display a series of graphs based on the raw data of cloud monitoring. The cloud monitoring console integrates monitoring data of all products, which is beneficial for users when obtaining an overall operations overview. According to the user's requirements, they can choose different access points to obtain instance data.

At the same time, creating an alert for an instance indicator that you are following, will enable the CVM instance to send alert information to the concerned group in a timely manner, when the operation status has reached a certain condition. This allows you to detect anomalies in a timely manner and take the appropriate measures to maintain system stability and reliability. For more information, refer to [Creating Alerts](/doc/product/248/6126).