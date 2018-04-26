﻿---
title: 配置在 Windows 7 或 Windows 8 上运行的客户端的服务质量策略
TOCTitle: 配置在 Windows 7 或 Windows 8 上运行的客户端的服务质量策略
ms:assetid: efff2b98-b3fb-4183-a4f0-329a9105ce2c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ205371(v=OCS.15)
ms:contentKeyID: 49314676
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 配置在 Windows 7 或 Windows 8 上运行的客户端的服务质量策略

 

_**上一次修改主题：** 2016-03-29_

除了指定由您的 Lync 客户端使用的端口范围外，您还必须创建将应用于客户端计算机的单独的服务质量策略。（不应将为会议、应用程序和中介服务器创建的服务质量策略应用于客户端计算机。）此信息仅适用于运行 Lync 2013 客户端和 Windows 7 或 Windows 8 的计算机。

以下示例使用此端口范围的设置创建音频策略和视频策略：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端通信类型</th>
<th>端口启动</th>
<th>端口范围</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音频</p></td>
<td><p>50020</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>视频</p></td>
<td><p>58000</p></td>
<td><p>20</p></td>
</tr>
<tr class="odd">
<td><p>应用程序共享</p></td>
<td><p>42000</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>文件传输</p></td>
<td><p>42020</p></td>
<td><p>20</p></td>
</tr>
</tbody>
</table>


要创建 Windows 7 或 Windows 8 计算机的服务质量音频策略，首先要登录到安装有组策略管理的计算机。打开组策略管理（单击“开始”，指向“管理工具”，然后单击“组策略管理”），然后完成下列过程：

1.  在组策略管理中，找到其中应创建新策略的容器。例如，如果所有客户端计算机位于名为客户端的 OU 中，则应在客户端 OU 中创建新策略。

2.  右键单击相应的容器，然后单击“在这个域中创建 GPO 并在此处链接”。

3.  在“新 GPO”对话框中，为“名称”框（例如，“Lync 音频”）中的新组策略对象输入一个名称，然后单击“确定”。

4.  右键单击新创建的策略，然后单击“编辑”。

5.  在组策略管理编辑器中，依次展开“计算机配置”、“策略”和“Windows 设置”， 右键单击“基于策略的 QoS”，然后单击“创建新策略”。

6.  在“基于策略的 QoS”对话框中的打开的页面上，在“名称”框中键入新策略（即：“Lync 音频”）的名称。选择“指定 DSCP 值”，并将该值设置为“46”。将“指定出站调节率”保留为未选中状态，然后单击“下一步”。

7.  在下一个页面上，确保选中“所有应用程序”，然后单击“下一步”。此设置指示该网络查看 DSCP 标记为 46 的所有数据包，不只是由特定应用程序创建的数据包。

8.  在第三页上，确保选中“任意源 IP 地址”和“任意目标 IP 地址”，然后单击“下一步”。这两个设置确保将管理这些数据包，与哪台计算机（IP 地址）发送这些数据包及哪台计算机（IP 地址）将接收这些数据包无关。

9.  在第四页上，从“选择此 QoS 策略所适用的协议”下拉列表中选择“TCP 和 UDP”。TCP（传输控制协议）和 UDP（用户数据报协议）是由 Lync Server 及其客户端应用程序最常使用的两个网络协议。

10. 在标题“指定源端口号”下，选择“从此源端口或范围”。在附带的文本框中，键入为音频传输保留的端口范围。例如，如果您为音频流量保留端口 50020 到端口 50039，则使用以下格式输入端口范围：“50020:50039”。单击“完成”。

在您为音频创建了 QoS 策略后，然后应该为视频创建第二个策略。要为视频创建策略，请按照您创建音频策略时遵循的相同基本过程，进行下列替换项：

  - 使用其他（及唯一）策略名称（例如，“Lync 视频”）。

  - 将 DSCP 值设置为“34”代替 46。（如先前所述，您不必使用为 34 的 DSCP 值；只是必须分配一个与用于音频不同的 DSCP 值。）

  - 使用先前为视频流量配置的端口范围。例如，如果已为视频保留端口 58000 到 58019，然后将端口范围设置为：“58000:58019”。

如果您决定创建用于管理应用程序共享流量的策略，请进行下列替换项：

  - 使用其他（及唯一）策略名称（例如，“Lync Server 应用程序共享”）。

  - 将 DSCP 设置为“24”代替 46。（另外，此值不必为 24；只是必须用于不同于音频和视频的 DSCP 值。）

  - 使用先前为视频流量配置的端口范围。例如，如果已为应用程序共享保留端口 42000 到 42019，然后将端口范围设置为：“42000:42019”。

对于文件传输策略：

  - 使用其他（及唯一）策略名称（例如，“Lync Server 文件传输”）。

  - 将 DSCP 值设置为“14”。（另外，此值不必为 14；只是它必须为唯一 DSCP 代码。）

  - 使用先前为应用程序配置的端口范围。例如，如果已为应用程序共享保留端口 42020 到 42039，然后将端口范围设置为：“42020:42039”。

在客户端计算机上刷新组策略之前，已创建的新策略不会生效。尽管组策略会定期自行刷新，但是您可以通过在需要刷新的组策略所在的每台计算机上运行下列命令来强制立即刷新：

    Gpudate.exe /force

可从在管理员凭据下运行的任何命令窗口运行此命令。要在管理员凭据下运行命令窗口，请单击“开始”，右键单击“命令提示符”，然后单击“以管理员身份运行”。

请记住，应该将这些策略指向客户端计算机目标。它们不应该应用到运行 Lync Server 的服务器。

要确保将网络数据包标记为相应的 DSCP 值，还应该通过完成以下过程在每台计算机上创建新的注册表项：

1.  单击“开始”，再单击“运行”。

2.  在“运行”对话框中，键入“regedit”，然后按 Enter 键。

3.  在注册表编辑器中，依次展开“HKEY\_LOCAL\_MACHINE”、“SYSTEM”、“CurrentControlSet”、“服务”和“Tcpip”。

4.  右键单击“Tcpip”，指向“新建”，然后单击“项”。创建新注册表项后，键入“QoS”，然后按 Enter 键以重命名该项。

5.  右键单击“QoS”，指向“新建”，然后单击“字符串值”。在创建新的注册表值之后，键入“不使用 NLA”，然后按 Enter 键以重命名值。

6.  双击“不使用 NLA”。在“编辑字符串”对话框的“数值数据”框中，键入“1”，然后单击“确定”。

7.  关闭注册表编辑器，然后重新启动您的计算机。

## 在具有多个网络适配器的计算机上配置服务质量

如果您的计算机有多个网络适配器，可能会偶尔遇到问题，即，DSCP 值显示为 0x00，而不是配置的值。此错误通常会发生在一个或多个网络适配器无法访问 Active Directory 域的计算机上（例如，如果这些适配器用于专用网络）。如果出现这种情况，则将 DSCP 值标记为使这些适配器可以访问该域，但不会标记为使这些适配器无法访问该域。

如果想在计算机中为所有网络适配器标记 DSCP 值，包括对您的域没有访问权限的适配器，则需要将值添加到注册表并进行配置。这可通过执行下列过程来完成：

1.  单击“开始”，再单击“运行”。

2.  在“运行”对话框中，键入“regedit”，然后按 Enter 键。

3.  在注册表编辑器中，依次展开“HKEY\_LOCAL\_MACHINE”、“SYSTEM”、“CurrentControlSet”、“服务”和“Tcpip”。

4.  如果没有看到标记为“QoS”的注册表项，则右键单击“Tcpip”，指向“新建”，然后单击“项”。创建新项后，键入“QoS”，然后按 Enter 键来重命名该项。

5.  右键单击“QoS”，指向“新建”，然后单击“字符串值”。在创建新的注册表值之后，键入“不使用 NLA”，然后按 Enter 键以重命名值。

6.  双击“不使用 NLA”。在“编辑字符串”对话框的“数值数据”框中，键入“1”，然后单击“确定”。

创建并配置新注册表值后，将需要重新启动计算机才能使更改生效。
