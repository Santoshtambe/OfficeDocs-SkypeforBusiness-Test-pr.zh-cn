﻿---
title: Lync Server 2013：配置带媒体旁路的中继
TOCTitle: 配置带媒体旁路的中继
ms:assetid: 99d729ea-5a4c-4ff2-a4a3-93a24368da6d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg398792(v=OCS.15)
ms:contentKeyID: 49313710
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中配置带媒体旁路的中继

 

_**上一次修改主题：** 2016-12-08_

执行以下步骤可配置启用媒体旁路的中继。要配置禁用媒体旁路的中继，请参阅[在 Lync Server 2013 中配置无媒体旁路功能的中继](lync-server-2013-configure-a-trunk-without-media-bypass.md)。如果希望将部署的中介服务器数目降至最低，媒体旁路非常有用。通常会在中央站点部署中介服务器池，中介服务器池将控制分支站点的网关。启用媒体旁路后，来自分支站点中客户端的公用电话交换网 (PSTN) 呼叫的媒体可直接通过这些站点中的网关流动。必须正确配置 Lync Server 2013 出站呼叫路由和企业语音策略，以使来自分支站点中客户端的 PSTN 呼叫路由至相应的网关。

强烈建议您启用媒体旁路。但是在 SIP 中继上启用媒体旁路之前，请确认您的合格 SIP 中继提供商是否支持媒体旁路且能够满足成功启用方案的要求。具体而言，提供商必须具有您组织内部网络中的服务器的 IP 地址。如果提供商无法支持此方案，则媒体旁路将会失败。有关详细信息，请参阅规划文档中的 [在 Lync Server 2013 中规划媒体旁路](lync-server-2013-planning-for-media-bypass.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>媒体旁路将不会与每个公用电话交换网 (PSTN) 网关、IP-PBX 和会话边界控制器 (SBC) 进行交互操作。Microsoft 与认证合作伙伴一起对一组 PSTN 网关和 SBC 进行了测试，另外也对 Cisco IP-PBX 进行了一些测试。针对 SBC 的证书正在测试中。媒体旁路仅支持 <a href="http://go.microsoft.com/fwlink/?linkid=214406%26clcid=0x804" class="uri">http://go.microsoft.com/fwlink/?linkid=214406&amp;clcid=0x804</a> 上的“统一通信开放式互操作性程序 – Lync Server”中列出的产品和版本。</td>
</tr>
</tbody>
</table>


如下所述的中继组合了一组应用于分配了此中继配置的中继的参数。可以将特定的中继配置的范围限定为全局（没有更特定的站点或池配置的所有中继）、一个站点或一个池。池级别中继配置用于将特定中继配置的范围限定为单个中继。

## 配置带媒体旁路的中继

1.  以 RTCUniversalServerAdmins 组成员的身份或者以 CsVoiceAdministrator、CsServerAdministrator 或 CsAdministrator 角色成员的身份登录计算机。有关详细信息，请参阅[Lync Server 2013 中的委派安装权限](lync-server-2013-delegate-setup-permissions.md)。

2.  打开浏览器窗口，然后输入管理 URL 以打开 Lync Server 控制面板。有关可以用于启动 Lync Server 控制面板的不同方法的详细信息，请参阅[打开 Lync Server 管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左侧导航栏中，单击“语音路由”，然后单击“Trunk 配置”。

4.  在“Trunk 配置”页上，使用以下方法之一配置中继：
    
      - 双击某个现有的中继（例如“全局”中继）以显示“编辑 Trunk 配置”对话框。
    
      - 单击“新建”，然后为新的中继配置选择范围：
        
          - **站点 Trunk：** 从“选择站点”中，为此中继配置选择站点，然后单击“确定”。请注意，如果已为站点创建中继配置，则该站点不会显示在“选择站点”中。此中继配置将应用于此站点中的所有中继。
        
          - **池 Trunk：** 选择应用了此中继配置的中继的名称。此中继可以是根中继或拓扑生成器中定义的任何其他中继。从“选择服务”中，单击“确定”。请注意，如果已为特定中继创建中继配置，则此中继不会显示在“选择服务”中。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>选择中继配置的范围后无法更改该范围。<br />
    “名称”字段会使用中继配置的关联站点或服务的名称进行预填充，且不能更改。</td>
    </tr>
    </tbody>
    </table>


5.  在“支持的最大早期对话数”中指定一个值。这是公用电话交换网 (PSTN) 网关、IP-PBX 或 ITSP 会话边界控制器 (SBC) 可以接收的分叉响应的最大数目，这些响应针对的是发送到中介服务器的邀请。默认值为 20。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在更改此值之前，请咨询您的服务提供商或设备制造商，以了解有关所用系统功能的详细信息。</td>
    </tr>
    </tbody>
    </table>


6.  选择以下“加密支持级别”选项之一：
    
      - **必需 ：** 必须使用安全实时传输协议 (SRTP) 加密以帮助保护中介服务器与网关或专用交换机 (PBX) 之间的通信。
    
      - **可选 ：** 如果服务提供商或设备制造商支持 SRTP，则使用 SRTP 加密。
    
      - **不支持 ：** SRTP 加密不受服务提供商或设备制造商支持，因此不使用。

7.  如果您要绕过中介服务器而通过中继对等方处理媒体，请选中“启用媒体旁路”复选框。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>为使媒体旁路功能成功发挥作用，PSTN 网关、IP-PBX 或 ITSP 会话边界控制器必须支持某些功能。有关详细信息，请参阅规划文档中的 <a href="lync-server-2013-planning-for-media-bypass.md">在 Lync Server 2013 中规划媒体旁路</a>。</td>
    </tr>
    </tbody>
    </table>


8.  如果存在一个已知的媒体端点（例如 PSTN 网关，其中媒体终端与信号终端具有相同的 IP），则选中“集中式媒体处理”复选框。如果中继没有已知的媒体端点，则清除该复选框。

9.  如果中继对等方支持接收来自中介服务器的 SIP REFER 请求，则选中“允许将引用发送到网关”复选框。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果禁用此选项而选中“启用媒体旁路”选项，则需要其他设置。如果中继对等方不支持接收来自中介服务器的 SIP REFER 请求且启用了媒体旁路，则为了支持媒体旁路的适当条件，还必须运行 <strong>Set-CsTrunkConfiguration</strong> cmdlet 以禁用活动呼叫和保留呼叫的 RTCP。有关详细信息，请参阅 <a href="lync-server-2013-lync-server-management-shell.md">Lync Server 命令行管理程序</a>文档。<br />
    此外，如果您希望转移的呼叫传输支持媒体旁路，并且网关不支持 SIP REFER 请求，则您可以选择“允许使用第三方呼叫控制的引用”。</td>
    </tr>
    </tbody>
    </table>


10. （可选）若要启用中继间路由，请将 PSTN 用法记录关联到此中继配置并进行相应的配置。与此中继配置关联的 PSTN 用法将通过不是源自 Lync 终结点的中继应用于所有传入呼叫。若要管理与中继配置关联的 PSTN 用法记录，请使用下列方法之一：
    
      - 要从企业语音部署中提供的所有 PSTN 用法记录列表中选择一个或多个记录，请单击“选择”。突出显示要与此中继配置关联的记录，然后单击“确定”。
    
      - 要删除此中继配置中的某个 PSTN 用法记录，请选择此记录，并单击“删除”。
    
      - 要定义新的 PSTN 用法记录并将其与此中继配置相关联，请执行以下操作：
        
        1.  单击“新建”。
        
        2.  在“名称”字段中，为记录指定唯一的描述性名称。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>PSTN 用法记录名称在企业语音部署中必须是唯一的。保存记录后，将无法编辑“名称”字段。</td>
            </tr>
            </tbody>
            </table>
        
        3.  使用下列方法之一为此 PSTN 用法记录关联和配置路由：
            
              - 要从企业语音部署中提供的所有路由列表中选择一个或多个路由，请单击“选择”。突出显示要与此 PSTN 用法记录相关联的路由，然后单击“确定”。
            
              - 要删除 PSTN 用法记录中的某个路由，请选择此路由，然后单击“删除”。
            
              - 要定义新路由并将其与此 PSTN 用法记录相关联，请单击“新建”。有关详细信息，请参阅[在 Lync Server 2013 中创建语音路由](lync-server-2013-create-a-voice-route.md)。
            
              - 要编辑与此 PSTN 用法记录相关联的路由，请选择此路由，然后单击“显示详细信息”。有关详细信息，请参阅[在 Lync Server 2013 中修改语音路由](lync-server-2013-modify-a-voice-route.md)。
        
        4.  单击“确定”。
    
      - 要编辑已经与此中继配置相关联的 PSTN 用法记录，请执行以下操作：
        
        1.  选择要编辑的 PSTN 用法记录，然后单击“显示详细信息”。
        
        2.  使用下列方法之一为此 PSTN 用法记录关联和配置路由：
            
              - 要从企业语音部署中提供的所有路由列表中选择一个或多个路由，请单击“选择”。突出显示要与此 PSTN 用法记录相关联的路由，然后单击“确定”。
            
              - 要删除 PSTN 用法记录中的某个路由，请选择此路由，然后单击“删除”。
            
              - 要定义新路由并将其与此 PSTN 用法记录相关联，请单击“新建”。有关详细信息，请参阅[在 Lync Server 2013 中创建语音路由](lync-server-2013-create-a-voice-route.md)。
            
              - 要编辑与此 PSTN 用法记录相关联的路由，请选择此路由，然后单击“显示详细信息”。有关详细信息，请参阅[在 Lync Server 2013 中修改语音路由](lync-server-2013-modify-a-voice-route.md)。
        
        3.  单击“确定”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>根据与要配置的中继关联的中介服务器对等方关联 PSTN 用法记录非常重要。如果中介服务器对等方是 PSTN 网关或会话边界控制器 (SBC)，则强烈建议不要将中继配置与将路由到 PSTN 目标或通过 Lync Server 连接的任何其他下游系统的 PSTN 用法记录相关联。</td>
    </tr>
    </tbody>
    </table>


11. 排列 PSTN 用法记录以获得最佳性能。要更改记录在列表中的位置，请选择 PSTN 用法记录，并单击向上箭头或向下箭头。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>PSTN 用法记录在中继配置中列出的顺序很重要。Lync Server 会从上到下遍历该列表。</td>
    </tr>
    </tbody>
    </table>


12. 应选择“启用 RTP 闭锁”为网络地址转换 (NAT) 或防火墙以及支持闭锁的 SBC 后面的客户端启用媒体旁路。

13. 应选择“启用呼叫转接历史记录”以支持将呼叫历史记录信息发送到中介服务器的对等网关。

14. 应选择“启用转发 P-Asserted-Identity 数据”以支持在中介服务器端和网关端之间转发 P-Asserted-Identity (PAI) 呼叫发起人信息（如果有），反之亦然。

15. 应选择“启用出站路由故障转移计时器”以启用快速故障转移。与此中继关联的网关会在 10 秒内发送通知，告知正在处理出站呼叫。如果中介服务器未收到此通知，则将重新路由到另一个中继。在延迟可能推迟响应时间或网关需要花费 10 秒以上的时间才能响应，应禁用快速故障转移。

16. （可选）为中继关联和配置“主叫号码转换规则”。这些转换规则适用于出站呼叫的主叫号码
    
      - 要从企业语音部署中提供的所有转换规则列表中选择一个或多个规则，请单击“选择”。在“选择转换规则”中，单击要与中继关联的规则，然后单击“确定”。
    
      - 要定义新的转换规则并将其与中继相关联，请单击“新建”。有关定义新规则的详细信息，请参阅部署文档中的[在 Lync Server 2013 中定义转换规则](lync-server-2013-defining-translation-rules.md)。
    
      - 要编辑已与中继关联的转换规则，请单击相应的规则名称，然后单击“显示详细信息”。有关详细信息，请参阅部署文档中的[在 Lync Server 2013 中定义转换规则](lync-server-2013-defining-translation-rules.md)。
    
      - 要复制现有的转换规则以作为定义新规则的起点，请单击相应的规则名称，再单击“复制”，然后单击“粘贴”。有关详细信息，请参阅[在 Lync Server 2013 中定义转换规则](lync-server-2013-defining-translation-rules.md)。
    
      - 要从中继删除某个转换规则，请突出显示相应的规则名称，然后单击“删除”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ656815.warning(OCS.15).gif" title="warning" alt="warning" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果已在关联的中继对等方上配置了转换规则，则不要将任何转换规则与中继相关联，因为这两种规则可能会发生冲突。</td>
    </tr>
    </tbody>
    </table>


17. （可选）为中继关联和配置“被叫号码转换规则”。这些转换规则适用于出站呼叫的被叫号码。
    
      - 要从企业语音部署中提供的所有转换规则列表中选择一个或多个规则，请单击“选择”。在“选择转换规则”中，单击要与中继关联的规则，然后单击“确定”。
    
      - 要定义新的转换规则并将其与中继相关联，请单击“新建”。有关定义新规则的详细信息，请参阅部署文档中的[在 Lync Server 2013 中定义转换规则](lync-server-2013-defining-translation-rules.md)。
    
      - 要编辑已与中继关联的转换规则，请单击相应的规则名称，然后单击“显示详细信息”。有关详细信息，请参阅部署文档中的[在 Lync Server 2013 中定义转换规则](lync-server-2013-defining-translation-rules.md)。
    
      - 要复制现有的转换规则以作为定义新规则的起点，请单击相应的规则名称，再单击“复制”，然后单击“粘贴”。有关详细信息，请参阅[在 Lync Server 2013 中定义转换规则](lync-server-2013-defining-translation-rules.md)。
    
      - 要从中继删除某个转换规则，请突出显示相应的规则名称，然后单击“删除”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ656815.warning(OCS.15).gif" title="warning" alt="warning" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果已在关联的中继对等方上配置了转换规则，则不要将任何转换规则与中继相关联，因为这两种规则可能会发生冲突。</td>
    </tr>
    </tbody>
    </table>


18. 确保中继的转换规则按正确的顺序排列。要更改规则在列表中的位置，请突出显示相应的规则名称，然后单击向上箭头或向下箭头。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server 2013 按照从上到下的顺序遍历转换规则列表，并使用第一个与拨打号码相匹配的规则。如果要配置中继以使拨打号码可以匹配多个转换规则，则确保限制较严格的规则排在限制较宽松的规则上方。例如，如果具有与任何 11 位数字相匹配的转换规则和只与以 +1425 开头的 11 位数字相匹配的转换规则，则确保与任何 11 位数字相匹配的规则排在更加严格的规则<em>下方</em>。</td>
    </tr>
    </tbody>
    </table>


19. 完成中继的配置后，单击“确定”。

20. 在“Trunk 配置”页上，单击“提交”，然后单击“全部提交”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>任何时候创建或修改中继配置，都必须运行“全部提交”命令以发布配置更改。有关详细信息，请参阅操作文档中的<a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">在 Lync Server 2013 中发布对语音路由配置所做的待处理更改</a>。</td>
    </tr>
    </tbody>
    </table>


配置中继后，可通过选择不同的全局媒体旁路选项继续配置媒体旁路，如部署文档中的 [全局媒体绕过选项](lync-server-2013-global-media-bypass-options.md)中所述。

## 另请参阅

#### 任务

[在 Lync Server 2013 中配置无媒体旁路功能的中继](lync-server-2013-configure-a-trunk-without-media-bypass.md)  

#### 概念

[在 Lync Server 2013 中配置媒体绕过](lync-server-2013-configure-media-bypass.md)  
[全局媒体绕过选项](lync-server-2013-global-media-bypass-options.md)  

#### 其他资源

[在 Lync Server 2013 中定义转换规则](lync-server-2013-defining-translation-rules.md)

