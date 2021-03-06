﻿---
title: Lync Server 2013：前端池配对数据安全
TOCTitle: 前端池配对数据安全
ms:assetid: edb852b8-ea86-4948-b756-60fe6ee876d2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ721930(v=OCS.15)
ms:contentKeyID: 49888674
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 中的前端池配对数据安全

 

_**上一次修改主题：** 2016-12-08_

备份服务是 Lync Server 2013 中引进的一种数据重复机制，为灾难恢复的目的不断跨两个数据中心在两个成对的 前端池之间转换用户数据和会议内容。用户数据包含 SIP URI，以及联系人列表和设置。会议内容包括 Microsoft PowerPoint 2010 上载，以及会议中使用的白板。从源池，将用户数据和会议内容从本地存储导出、提取和转换到目标池，其中是解压和导入到本地存储。备份服务假定两个数据中心之间的通讯链路位于公司网络内部，受 Internet 保护。它不会在两个数据中心之间加密传输的数据，也不会在安全协议（如 HTTPS）内进行本地封装。因此有可能受到公司网络内来自内部人员的中间人攻击。

## 评估安全风险

跨多个数据中心部署 Lync Server 2013 并使用灾难恢复功能的企业必须确保跨数据中心流量受其公司 Intranet 保护。在意内部攻击保护的企业必须保护数据中心中通讯链路的安全。

假定企业的数据中心受公司 Intranet 的保护是标准。有许多其他类型的公司敏感数据在这些数据中心间传输。如果不保护跨数据中心链接，则企业的 IT 基础结构处于极端的风险中。

当公司网络内存在中间人攻击的风险时，比较而言，它相当于包含将流量公开到 Internet。尤其是，通过备份服务（如，SIP URI）公开的用户数据通过其他方法（例如，按 Exchange 或其他目录软件列出的全局通讯簿）通常可用于公司内的所有员工。因此，当将备份服务用于复制两个成对池之间的数据时，重点应该是保护两个数据中心之间的 WAN。

## 减轻安全风险

有多种方法可加强备份服务流量安全保护，其范围包括从限制对数据中心的访问到保护两个数据中心之间的 WAN 传输。在大多数情况下，部署 Lync Server 2013 的企业可能已将所需的安全基础结构部署到位。对于寻求指导的企业，Microsoft 提供作为如何构建安全 IT 基础结构示例的解决方案。但是，这不表示它只是解决方案，也不表示它是 Lync Server 的首选解决方案。我们建议企业客户根据其 IT 安全基础结构和需要选择其特定需要的解决方案套件。例如，Microsoft 解决方案将 IPSec 和组策略应用于服务器和域隔离。有关详细信息，请参阅 [http://go.microsoft.com/fwlink/?linkid=268544\&clcid=0x804](http://go.microsoft.com/fwlink/?linkid=268544%26clcid=0x804)。有关问题和评论，请联系 secwish@microsoft.com。

另一个可能的解决方案是仅使用 IPSec 来帮助保护由备份服务本身发送的数据。如果选择此方法，您应该为以下服务器配置 SMB 协议的 IPSec 规则，其中，池 A 和池 B 是两个配对前端池。

  - SMB 服务 (TCP/445) 从池 A 中的每个前端服务器到由池 B 使用的文件存储。

  - SMB 服务 (TCP/445) 从池 B 中的每个前端服务器到由池 A 使用的文件存储。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ656815.warning(OCS.15).gif" title="warning" alt="warning" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>IPsec 不专门用于代替应用程序级别的安全，例如，SSL/TLS。使用 IPsec 的一个优势是，可为现有应用程序提供网络流量安全，但无需更改它们。只想在两个数据中心之间提供传输保护的企业应该咨询其相应的网络硬件供应商，以了解有关通过使用供应商的设备建立安全 WAN 连接的方法。</td>
</tr>
</tbody>
</table>

