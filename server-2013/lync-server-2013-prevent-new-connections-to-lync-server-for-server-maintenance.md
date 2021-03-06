﻿---
title: 阻止与 Lync Server 建立新连接以进行服务器维护
TOCTitle: 阻止与 Lync Server 建立新连接以进行服务器维护
ms:assetid: 22b27adf-a590-43bd-9306-a5789ae108d7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg520964(v=OCS.15)
ms:contentKeyID: 49312245
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 阻止与 Lync Server 建立新连接以进行服务器维护

 

_**上一次修改主题：** 2012-11-01_

Lync Server 允许您将服务器置于脱机状态（例如，应用软件或硬件升级）而不会影响用户服务。

如果指定阻止对池中服务器的新连接或新呼叫的选项，则一旦实现此选项，服务器将停止接收任何新连接和呼叫。这些新的连接和呼叫将通过池中的其他服务器进行路由。阻止新连接的服务器允许其现有连接上的会话继续进行，直至会话自然结束。所有现有会话都结束后，即可将服务器置于脱机状态。

如果阻止对前端服务器的新连接，Lync Server 的某些功能和服务将依赖 DNS 负载平衡来确保正常工作。如果在池中没有使用 DNS 负载平衡，则服务器阻止新连接期间，通过这些服务的连接可能不会重新路由到其他服务器，因此将服务器置于脱机状态时，某些会话和呼叫可能会中断。依赖 DNS 负载平衡以确保此选项正常运行的功能如下所示：

  - 助理

  - 会议通知应用程序

  - 响应组应用程序

  - 通知应用程序

  - 呼叫寄存应用程序

有关 DNS 负载平衡的详细信息，请参阅规划文档中的 [Lync Server 2013 中的 DNS 负载平衡](lync-server-2013-dns-load-balancing.md)。

除了阻止运行 Lync Server 的服务器上所有服务的新连接之外，还可以阻止单个 Lync Server 服务的新连接。例如，此方法适用于需要应用 Lync Server 更新但无需关闭整台服务器的情况。请注意，阻止一项服务的连时，必须选择 Windows 服务列表中所属和显示的服务。例如，Lync Server 前端服务和监控的数据收集代理是不同的 Lync Server 服务，但在 Windows 服务列表中，它们合并显示为 Lync Server 前端服务。可以阻止 Lync Server 前端服务的新连接，但无法分别阻止这两个底层 Lync Server 服务各自的新连接。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果将某台服务器设置为阻止新连接，然后重新启动该服务器，则默认情况下，该服务器启动后将立即开始接受新连接。要防止此情况发生，请在重新启动服务器之前，将其设置为仅手动暂停和恢复。</td>
</tr>
</tbody>
</table>


## 阻止与 Lync Server 建立新连接：

1.  以 Administrators 组成员的身份登录本地计算机。

2.  打开服务管理单元控制台：单击“开始”，依次指向“所有程序”和“管理工具”，然后单击“服务”。

3.  在列表中，双击要阻止与其建立新连接的 Lync Server Windows 服务。

4.  在“属性”对话框的“服务状态: 已启动”下，单击“暂停”。

5.  或者，作为推荐选项，单击“启动类型”旁边的“手动”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果将某台服务器设置为阻止新连接，然后重新启动该服务器，则默认情况下，该服务器启动后将立即开始接受新连接。要防止此情况发生，请在重新启动服务器之前，将其设置为仅手动暂停和恢复。</td>
    </tr>
    </tbody>
    </table>


6.  完成后，单击“确定”。

