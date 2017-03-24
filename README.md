# Product overview

This document contains the following topics:
このドキュメントには次のトピックが含まれています。
- [VPC overview](overview)
- [Basic architecture](#architecutre)
- [VPC benefits](#benefits)
VPCの概要
基本的なアーキテクチャ
VPCのメリット

<a name="overview"></a>
## VPC overview

The Alibaba Cloud Virtual Private Cloud (VPC) is a private network established in Alibaba Cloud. It is logically isolated from other virtual networks in Alibaba Cloud. Alibaba Cloud VPC enables you to launch and use the Alibaba Cloud resources in your own VPC.

You have full control over your Alibaba Cloud VPC, for example, you can select its IP address range, further segment your VPC into subnets, as well as configure routing tables and network gateways. Additionally, you can connect your VPC to your on-premises network using a physical connection or a VPN to form an on-demand customizable network environment. This allows you to smoothly migrate your applications to Alibaba Cloud with little effort.

Alibaba Cloud仮想プライベートクラウド（VPC）は、Alibaba Cloudに設置されたプライベートネットワークです。Alibaba Cloudの他の仮想ネットワークと論理的に分離されています。Alibaba Cloud VPCを使用すると、独自のVPCでAlibaba Cloudリソースを起動して使用することができます。

Alibaba Cloud VPCを完全に制御できます。たとえば、IPアドレス範囲を選択したり、VPCをサブネットに分割したり、ルーティングテーブルやネットワークゲートウェイを設定することができます。さらに、物理接続またはVPNを使用してVPCをオンプレミスネットワークに接続して、オンデマンドのカスタマイズ可能なネットワーク環境を構築することもできます。これにより、少ない労力でアプリケーションをAlibaba Cloudにスムーズに移行できます。


![1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/34217/intl_en/1490084621378/Basic_VPC.png)

<a name="architecutre"></a>
## Basic architecture  基本的なアーキテクチャ

Based on the mainstream tunneling technology, the virtual private cloud isolates the virtual network. Each VPC has a unique tunnel ID and a tunnel ID corresponds to a virtual network. The data packets transmitted between ECS instances within a VPC are encapsulated with a unique tunnel ID and then sent to the physical network for transmission. The tunnel IDs for ECS instances in different VPCs are different, communication is impossible between the two tunnels, which achieves data isolation between the two networks.

主流のトンネリング技術をベースにした仮想プライベートクラウドは、仮想ネットワークを分離します。各VPCに固有のトンネルIDがあり、トンネルIDは、仮想ネットワークに対応します。VPCのECSのインスタンス間で送信されたデータパケットは、固有のトンネルIDでカプセル化された次の転送のために、実際のネットワークに転送されます。別のVPCのECSインスタンスのトンネルIDが異なる場合は、2つのトンネル間の通信が不可能であり、2つのネットワーク間でデータの分離が行われます。

The Alibaba Cloud development team developed VSwitch, Software Defined Network (SDN) and hardware gateway independently based on the tunneling technology. It is the support of these software and hardware devices, the Alibaba Cloud Virtual Private Cloud is emerged. VSwitches, gateways, and controllers are three important components of a VPC. VSwitches and gateways are the main path for data transfer. The controller uses self-developed protocol to forward routing tables to VSwitches and gateways. The configuration channel and data channel are separated in the whole architecture.

Alibaba Cloud開発チームは、トンネリング技術をベースに、VSwitch、SDN（Software Defined Network）、およびハードウェアゲートウェイを独自に開発しました。これらのソフトウェアとハードウェアデバイスのサポートで、Alibaba Cloud Virtual Private Cloudが登場しました。VSwitch、ゲートウェイ、およびコントローラは、VPCの3つの重要な構成要素です。VSwitchとゲートウェイは、データ転送の主な経路です。コントローラは、自社開発のプロトコルを使用してルーティングテーブルをVSwitchとゲートウェイに転送します。構成チャネルとデータチャネルは、全体のアーキテクチャで分離されています。

Alibaba Cloud VPC provides you with a separate VRouter and VSwitch for better VPC configuration and gives you more freedom. If you have high demand on intranet security, you can use security groups to manage the VPC access control in a finer granularity. By default, an ECS instance can only communicate with other ECS instances (or other cloud services) within the same VPC. You can use the Elastic IP address and ExpressConnect functions provided by Alibaba Cloud to connect your VPC to the Internet, to other VPCs, and to your own networks.

Alibaba Cloud VPCは、より良いVPCの構成のために、別のVRouterとVSwitchを提供してより多くの自由度を提供しています。イントラネットのセキュリティの需要が高い場合は、セキュリティグループを使用してVPCのアクセス制御を細かく管理することができます。基本的にECSインスタンスは、同じVPC内の他のECSのインスタンス（または他のクラウドサービス）のみと通信することができます。Alibaba Cloudで提供されるElastic IPアドレスとExpressConnect機能を使用してVPCをインターネットまたは他のVPCと自分のネットワークに接続することができます。


![1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/34217/intl_en/1490087831180/VPC_New.png)

<a name="benefits"></a>
## VPC benefits   VPCのメリット

- **Security isolation   セキュリティの分離**   
	- The cloud servers of different users are located in the different VPCs.
	- 異なるユーザーのクラウドサーバーは、異なるVPCに配置されています。
	- Different VPCs are isolated by tunnel IDs. Using VSwitches and VRouters, you can segment your VPC into subnets as you do in the traditional network environment. Different cloud servers in the same subnet use the VSwitch to communicate with each other, while cloud servers in different subnets within a VPC use VRouters to communicate with each other.
	- 異なるVPCはトンネルIDによって隔離されています。VSwitchとVRouterを使用すると、従来のネットワーク環境と同じように、VPCをサブネットに分割できます。同じサブネット内の異なるクラウドサーバはVSwitchを使用して相互に通信し、VPC内の異なるサブネットにあるクラウドサーバはVRouterを使用して相互に通信します。
	
	- The intranet between different VPCs are completely isolated and can only be interconnected by external mapping of IP (Elastic IP and NAT IP).
	- 異なるVPC間のイントラネットは完全に分離されており、IP（Elastic IPおよびNAT IP）の外部マッピングによってのみ相互接続できます。
	
	- Because the IP packets of cloud servers are encapsulated with the tunneling ID, the data link layer (two-layer MAC address) of the cloud server will not transfer to the physical network. Therefore, the two-layer network of different cloud servers are isolated. In another word, the two-layer networks between different VPCs are isolated.
	- クラウドサーバのIPパケットはトンネリングIDでカプセル化されているため、クラウドサーバのデータリンク層（2層MACアドレス）は物理ネットワークに転送されません。したがって、異なるクラウドサーバーの2層ネットワークが分離されます。言い換えれば、異なるVPC間の2層ネットワークが分離されています。

	- The ECS instances within a VPC uses a security group firewall to control the network access. This is the third layer isolation.
	- VPC内のECSインスタンスは、セキュリティグループファイアウォールを使用してネットワークアクセスを制御します。これは第3層の分離です。

- **Access controlアクセス制御**
	- Security groups provide flexible access control rules.
	- セキュリティグループは、柔軟なアクセス制御ルールを提供します。
	- Compliant with security isolation rules of government and financial users.
	- 政府および金融ユーザーのセキュリティ分離ルールに準拠しています。
	
- **Software Defined Network (SDN)ソフトウェア定義ネットワーク（SDN）**
	- SDN provides customized network configurations.
	- SDNはカスタマイズされたネットワーク構成を提供します。
	- Management operations take effect in real time.
	- 管理業務はリアルタイムで有効になります。
	
- **Various network connection methodsさまざまなネットワーク接続方法**
	- Software VPNs are supported.ソフトウェアVPNがサポートされています。
	- Lease line connection is supported.リース回線接続がサポートされています。
  






