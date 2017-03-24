# Product overview

This document contains the following topics:

- [VPC overview](overview)
- [Basic architecture](#architecutre)
- [VPC benefits](#benefits)


<a name="overview"></a>
## VPC overview

The Alibaba Cloud Virtual Private Cloud (VPC) is a private network established in Alibaba Cloud. It is logically isolated from other virtual networks in Alibaba Cloud. Alibaba Cloud VPC enables you to launch and use the Alibaba Cloud resources in your own VPC.

You have full control over your Alibaba Cloud VPC, for example, you can select its IP address range, further segment your VPC into subnets, as well as configure routing tables and network gateways. Additionally, you can connect your VPC to your on-premises network using a physical connection or a VPN to form an on-demand customizable network environment. This allows you to smoothly migrate your applications to Alibaba Cloud with little effort.

![1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/34217/intl_en/1490084621378/Basic_VPC.png)

<a name="architecutre"></a>
## Basic architecture

Based on the mainstream tunneling technology, the virtual private cloud isolates the virtual network. Each VPC has a unique tunnel ID and a tunnel ID corresponds to a virtual network. The data packets transmitted between ECS instances within a VPC are encapsulated with a unique tunnel ID and then sent to the physical network for transmission. The tunnel IDs for ECS instances in different VPCs are different, communication is impossible between the two tunnels, which achieves data isolation between the two networks.

The Alibaba Cloud development team developed VSwitch, Software Defined Network (SDN) and hardware gateway independently based on the tunneling technology. It is the support of these software and hardware devices, the Alibaba Cloud Virtual Private Cloud is emerged. VSwitches, gateways, and controllers are three important components of a VPC. VSwitches and gateways are the main path for data transfer. The controller uses self-developed protocol to forward routing tables to VSwitches and gateways. The configuration channel and data channel are separated in the whole architecture.

Alibaba Cloud VPC provides you with a separate VRouter and VSwitch for better VPC configuration and gives you more freedom. If you have high demand on intranet security, you can use security groups to manage the VPC access control in a finer granularity. By default, an ECS instance can only communicate with other ECS instances (or other cloud services) within the same VPC. You can use the Elastic IP address and ExpressConnect functions provided by Alibaba Cloud to connect your VPC to the Internet, to other VPCs, and to your own networks.

![1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/34217/intl_en/1490087831180/VPC_New.png)

<a name="benefits"></a>
## VPC benefits

- **Security isolation**
	- The cloud servers of different users are located in the different VPCs.
	- Different VPCs are isolated by tunnel IDs. Using VSwitches and VRouters, you can segment your VPC into subnets as you do in the traditional network environment. Different cloud servers in the same subnet use the VSwitch to communicate with each other, while cloud servers in different subnets within a VPC use VRouters to communicate with each other.
	- The intranet between different VPCs are completely isolated and can only be interconnected by external mapping of IP (Elastic IP and NAT IP).
	- Because the IP packets of cloud servers are encapsulated with the tunneling ID, the data link layer (two-layer MAC address) of the cloud server will not transfer to the physical network. Therefore, the two-layer network of different cloud servers are isolated. In another word, the two-layer networks between different VPCs are isolated.
	- The ECS instances within a VPC uses a security group firewall to control the network access. This is the third layer isolation.

- **Access control**
	- Security groups provide flexible access control rules.
	- Compliant with security isolation rules of government and financial users.
	
- **Software Defined Network (SDN)**
	- SDN provides customized network configurations.
	- Management operations take effect in real time.
	
- **Various network connection methods**
	- Software VPNs are supported.
	- Lease line connection is supported.
  
  
 -----------------------------------**************************--------------******************---------------**********
 
 # Product Introduction

Virtual Private Cloud (VPC) helps you establish an isolated network environment based on Alibaba Cloud. You have full control over your own VPC, including choosing a preferred IP address range, CIDR block, route table, and gateway. In addition, you can establish a customizable network environment by connecting your VPC to your traditional data center through a physical connection/VPN, achieving smooth application migration to the cloud.

**Difference Between a VPC and a Classic Cloud**

* The products of classic network type are uniformly deployed in Alibaba Cloud&apos;s public infrastructure network, whose planning and management are Alibaba Cloud&apos;s responsibility. These products are more suitable for customers who have high ease-of-use requirements.
* VPC enables you to establish a customizable isolated private cloud on Alibaba Cloud&apos;s basic network and define the network topology and IP address of this VPC. Compared with the classic cloud, the VPC is more suitable for customers that require and able to manage their clouds.

**Regions with the VPC Service Available**

Asia-Pacific (Singapore), South China 1 (Shenzhen), North China 2 (Beijing), East China 2 (Shanghai), East US (Virginia), Hong Kong, East China 1 (Hangzhou), and West US (Silicon Valley)

The complete list of regions is available on the console.

## Product Comparison

<table>
	<tr>
		<td>Function Point</td>
		<td>Classic Cloud</td>
		<td>VPC</td>
	</tr>
	<tr>
		<td>L2 logical isolation</td>
		<td>No</td>
		<td>Yes</td>
	</tr>
	<tr>
		<td>Customized CIDR block</td>
		<td>No</td>
		<td>Yes</td>
	</tr>
	<tr>
		<td>Private IP addresses</td>
		<td>Intra-classic cloud unique</td>
		<td>Intra-VPC unique, but inter-VPC duplicable</td>
	</tr>
	<tr>
		<td>Customer VPN</td>
		<td>No</td>
		<td>Yes</td>
	</tr>
	<tr>
		<td>Instance communication</td>
		<td>Allowed for instances of the same account and region</td>
		<td>Allowed for instances within the same VPC, but not between VPCs</td>
	</tr>
	<tr>
		<td>Customer NAT gateway</td>
		<td>No</td>
		<td>Yes</td>
	</tr>
	
</table>
