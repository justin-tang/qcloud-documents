Tencent Cloud offers two CVM purchase modes: Annual/Monthly Package and pay-by-traffic, which are designed respectively for user needs in different scenarios.
The following table lists the differences between the two billing modes:
<p class="table-hover">&nbsp;</p>
<table align="left";">
	<thead>
		<tr>
<th scope="row"><strong>CVM billing mode </strong></th>
<th scope="col"><strong>Annual/Monthly Package</strong></th>
			<th scope="col"><strong>Pay by Traffic</strong></th>
		</tr>
	</thead>
	<tbody>
		<tr>
<th scope="row"><strong>Payment method</strong></th>
			<td>Prepaid</td>
			<td>Fees frozen upon purchase, settled every hour</td>
		</tr>
		<tr>
<th scope="row">Billing unit</th>
			<td>
			CNY/month <br> At least for one month
			</td>
			<td>
		CNY/second <br> billing in seconds, settled every hour, in service upon purchase
			</td>
		</tr>
		<tr>
			<th scope="row">Unit price</th>
			<td>Lower unit price</td>
			<td>
			Higher initial unit price, tiered reduction <br> After use of 15 consecutive days, its unit price is close to that of the Annual/Monthly Package
			</td>
		</tr>
		<tr>
<th scope="row">Pay by Bandwidth mode</th>
<td colspan="2" rowspan="1">Supports both pay-by-bandwidth and pay-by-traffic</td>
		</tr>
		<tr>
		<th scope="row">Adjust instance configuration</th>
			<td>
			Configuration upgrade/downgrade at any time, <span style="background-color:  transparent;">Configuration downgrade only can be used three times</span>
			</td>
			<td>Configuration upgrade/downgrade at any time, without restrictions</td>
		</tr>
		<tr>
<th scope="row">Application scenarios</th>
			<td>Applicable to mature services with predictable long-term and stable equipment demands</td>
			<td>Applicable to online scare buying and other scenarios with highly fluctuating equipment demands</td>
		</tr>
	</tbody>
</table>





## 1.	Annual/Monthly Package

An example for annual/monthly-package CVMs is first purchase and then use: When you purchase CVMs in the prepaid mode, the system will deduct corresponding amount from your cloud expense account based on the resources hardware (including CPU, memory, data disk) that you purchase and network costs.

An example for annual/monthly-package CVMs is first purchase and then use: When you purchase CVMs in the prepaid mode, the system will deduct corresponding amount from your cloud expense account based on the resources hardware (including CPU, memory, data disk) that you purchase and network costs.

Amount to be deducted for buying cloud services = Number of cloud services applied × Unit price of cloud services.

Therefore, before purchasing cloud services, you need first to check the balance of your cloud expense account. If the balance is less than the amount required, please top up first.

For prices of annual/monthly-package CVM instances, [see here](http://www.qcloud.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E4%BB%B7%E6%A0%BC#1.-Annual/Monthly Package) 
For configuration of annual/monthly-package CVM instances, "see>" (http://www.qcloud.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)
For expiration reminder for annual/monthly-package CVMs, [see here](http://www.qcloud.com/doc/product/213/%E5%88%B0%E6%9C%9F%E6%8F%90%E9%86%92#1.-Expiration reminder for annual/monthly-package CVMs)
For adjusting instance configuration of annual/monthly-package CVMs, [see here](http://www.qcloud.com/doc/product/213/%E8%B0%83%E6%95%B4CVM%E7%A1%AC%E4%BB%B6%E9%85%8D%E7%BD%AE)


## 2.	Pay by Traffic

Pay by Traffic is an elastic billing mode for CVM instances. You can activate/terminate at any time to make payment based on actual CVM usage. Billing reference period is accurate to **seconds**. Advance payment is not required and settlement is made every hour on the hour. Applicable to online scare buying and other scenarios with highly fluctuating equipment demands, its unit price 3-4 times higher than that of the Annual/Monthly Package mode.

When you activate a pay-by-traffic CVM instance, the system will freeze in advance one-hour hardware (including CPU, memory, and data disk) fees for the CVM and make settlement every hour on the hour (Beijing time, based on your last-hour actual CVM usage. The hourly unit price of CVM instances is displayed upon purchase, and settlement is made by **actual seconds**, with costs rounded to two decimal places. Billing starts at the point when the CVM instance is created successfully, and ends at the point when you initiate a termination operation.

One-hour fees will be frozen when a pay-by-traffic CVM is created. When you adjust configuration of the pay-by-traffic CVM, the system unfreeze the already frozen fees and freeze another fees based on the unit price of the new configuration. When the CVM instance is terminated, the frozen fees become unfrozen. 

**Billing in seconds, no cost waste**
Billing starts when the CVM instance is created successfully, and ends when you initiate a termination operation.
![](//mc.qcloudimg.com/static/img/b67e5fbde8f2a9d2c0e619c633ce0b89/image.jpg)
**Tiered price reduction, saving more money for longer usage**
Pay-by-traffic CVMs use 3-tier pricing, saving more money for longer usage.
 
| Phase | Tier 1 | Tier 2 | Tier 3|
|---|---|---|---|
| Duration (hours) | 0 < T  96 | 96 <T  360 | T > 360 |
>Note:  T is the time of continuous use of pay-by-traffic CVMs.

| Phase | Tier 1 | Tier 2 | Tier 3|
|---|---|---|---|
| Price (CNY/hour) | P | 50% × P | 34% × P |
> Note:  P is the tier-1 unit price of pay-by-traffic CVMs.


![](//mc.qcloudimg.com/static/img/2b8e3a898dab0454d77d99a0e1c1eb07/image.jpg)

Take 1-core 2 GB configuration as an example: tier-1 unit price is 0.42 CNY/hour, tier-2 unit price 0.42 × (1-50%) = 0.21 CNY/hour, and tier-3 unit price 0.42 × (1-50%-16%) = 0.14 CNY/hour

"Note"
1. CVM tiered pricing program only involves CPU and memory costs, excluding network and disk costs.
2. The tiered pricing program only involves CPU and memory costs, excluding network and disk costs
3. The tiered pricing program applies only to the same configuration. If the configuration changes, billing will starts again from tier 1 of the new configuration. In the CVM example: the original configuration is 2-core 4 GB and you have entered tier 2 after using it for 100 hours. Then you change the configuration to 1-core 2 GB, so your billing starts again from tier 1 of the 1-core 2 GB configuration.
4. The pay-by-traffic arrears program remains unchanged. [Learn about the Pay-by-Traffic Arrears Program](https://www.qcloud.com/doc/product/213/%E5%88%B0%E6%9C%9F%E6%8F%90%E9%86%92#2.3.-.E6.AC.A0.E8.B4.B9.E5.A4.84.E7.90.86)

Click the links below for more information on pay-by-traffic instructions.

For prices of pay-by-traffic CVM instances, [see here](http://www.qcloud.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E4%BB%B7%E6%A0%BC#2.-Pay by Traffic) 
For configuration of pay-by-traffic CVM instances, [see here](http://www.qcloud.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)
For expiration reminder for pay-by-traffic CVMs, [see here](http://www.qcloud.com/doc/product/213/%E5%88%B0%E6%9C%9F%E6%8F%90%E9%86%92#2.-Expiration reminder for pay-by-traffic CVMs) 
For adjusting instance configuration of pay-by-traffic CVMs, [see here](http://www.qcloud.com/doc/product/213/%E8%B0%83%E6%95%B4CVM%E7%A1%AC%E4%BB%B6%E9%85%8D%E7%BD%AE)


