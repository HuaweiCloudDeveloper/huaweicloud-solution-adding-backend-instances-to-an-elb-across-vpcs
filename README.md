[TOC]

**Solution Overview**
===============
If you deploy services on multiple servers in different VPCs, you can use ELB to route traffic to backend servers in different VPCs connected over a VPC peering connection.

For details, visit https://www.huaweicloud.com/solution/implementations/adding-backend-instances-to-an-elb-across-vpcs.html.

**Solution Architecture**
---------------

![Architecture](http://image.huawei.com/tiny-lts/v1/images/45170a864cc81c189c5fac6f24fa8cec_1169x712.png)

**Architecture Overview**
---------------

To use this solution, you need to:
- Create two ECSs in different VPCs for running services.
- Configure a security group to control traffic to and from the two ECSs.
- Create a dedicated load balancer to distribute incoming traffic to the two ECSs.


**Organizational Structure**
---------------

``` lua
huaweicloud-solution-adding-backend-instances-to-an-elb-across-vpcs
├── adding-backend-instances-to-an-elb-across-vpcs.tf.json -- Resource orchestration template
```
**Getting Started**
---------------

1. Log in to the EIP console, create two EIPs, and bind them respectively to the two ECSs created as instructed in *Section 3.2 Quick Deployment* of the deployment guide.

    Figure 1 Creating EIPs
    ![Creating EIPs](./document/readme-image-001.PNG)

2. Log in to the two ECSs created as instructed in *Section 3.2 Quick Deployment* of the deployment guide, deploy the httpd service on each ECS, and run the command below. Note that you can configure the message in the double quotation marks in the second line whatever you like. If the load balancer routes the request to the ECSs, this message will be returned.

	yum -y install httpd

	echo "www.test01.com" > /var/www/html/index.html

	chmod 777  /var/www/html/index.html

	systemctl start httpd

	curl localhost

	Figure 2 Logging in to the ECSs
	![Logging in to the ECSs](./document/readme-image-002.PNG)

	Figure 3 Installing the httpd service
	![Installing the httpd service](./document/readme-image-003.PNG)

	Figure 4 Installing the httpd service
	![Installing the httpd service](./document/readme-image-004.PNG)

3. Unbind the EIPs bound to the two ECSs in step 2 and release the EIPs.

	Figure 5 Unbinding and releasing the EIPs
	![Unbinding and releasing the EIPs](./document/readme-image-005.PNG)

4. On the ELB console, view the dedicated load balancer you have created for deploying this solution.

	Figure 6 Viewing the load balancer
	![Viewing the load balancer](./document/readme-image-006.PNG)

5. Enter the EIP address assigned in step 4 in the address box of your browser to access the dedicated load balancer. If the following two pages are displayed, the load balancer routes the requests to the two ECSs.

	Figure 7 Verifying that the request is routed to one ECS

	![Verifying that the request is routed to one ECS](./document/readme-image-007.PNG)

	Figure 8 Verifying that the request is routed to the other ECS

	![Verifying that the request is routed to the other ECS](./document/readme-image-008.PNG)






