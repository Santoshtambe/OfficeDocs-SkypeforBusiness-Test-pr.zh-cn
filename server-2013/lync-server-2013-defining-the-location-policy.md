﻿---
title: Lync Server 2013：定义位置策略
TOCTitle: 定义位置策略
ms:assetid: da3cca7f-f6e5-4b6f-90a1-2008e3dd1ebd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg398962(v=OCS.15)
ms:contentKeyID: 49314441
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 为 Lync Server 2013 定义位置策略

 

_**上一次修改主题：** 2012-10-29_

每个位置策略包含以下信息：

  - **启用紧急服务**  
    该值设置为“是”时，可为客户端启用 E9-1-1。客户端在注册时将尝试从 位置信息服务获得一个位置，并将包括位置信息作为紧急呼叫的一部分。

<!-- end list -->

  - **需要位置**  
    仅当“启用紧急服务”设置为“是”时才使用此设置。
    
    可以配置“所需位置”设置来定义客户端行为。将该值设为“否”表示不会提示用户输入位置。设为“是”表示将提示用户输入位置，但可以消除提示。设置为“免责声明”表示将会提示用户输入位置，并且当用户尝试消除提示时将显示免责声明。在所有情况下，用户都可以继续使用该客户端。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果在启用 E9-1-1 之前用户手动输入位置，则不会显示免责声明文本。已查看免责声明的用户将不能查看免责声明文本的更新。</td>
    </tr>
    </tbody>
    </table>


<!-- end list -->

  - **增强型紧急服务免责声明**  
    该设置指定当用户消除输入位置提示时显示的免责声明。在 Lync Server 2013 中，可以使用位置策略为不同的区域设置或不同的用户集合设置不同的免责声明。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>该位置策略与在 Lync Server 2010 中使用 <strong>Set-CsEnhancedEmergencyServiceDisclaimer</strong> cmdlet 为整个组织设置全局免责声明不同。如果全局免责声明已经存在，则需要在位置策略中指定该免责声明。即， Lync Server 2013 仅使用位置策略中指定的免责声明。</td>
    </tr>
    </tbody>
    </table>


<!-- end list -->

  - **紧急拨号串**  
    该拨号字符串（没有前导“+”，但包含 Lync 用户拨号计划完成的任何规范化）表示呼叫是一个紧急呼叫。**紧急拨号串**使客户端包括有关呼叫的位置和回拨信息。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果组织未使用外线访问前缀，则您无需创建对应的拨号计划规范化规则，该规则为在将呼叫发送至 Lync 池服务器上的出站路由前，在 911 字符串前添加“+”；由于位置策略，“+”将由 Lync 客户端自动追加。但是，如果您的站点使用外部访问前缀，则您需要向适用的拨号计划策略添加规范化规则，以去掉外部访问前缀并添加“+”。例如，如果您所在位置使用外部访问前缀 9，用户拨打 9 911 发出紧急呼叫，则客户端将使用其拨号计划策略将此呼叫规范化为 +911，然后再由主叫方的位置配置文件中的路由评估拨号号码。</td>
    </tr>
    </tbody>
    </table>


<!-- end list -->

  - **紧急拨号串掩码**  
    一个分号分隔的拨号字符串列表将转换为指定的 **紧急拨号字符串**。例如，您可能想要添加 112（欧洲大部分地区的紧急服务号码）。来自欧洲的访问 Lync 用户可能不知道美国的紧急号码是 911，但他们可拨打 112，结果都一样。使用紧急拨号字符串，每个号码前都没有“+”，如果您使用外线访问代码，请确保用户的拨号计划策略中存在规范化规则以去掉访问代码数字。

<!-- end list -->

  - **PSTN 用法**  
    包含确定紧急呼叫将转至哪一 SIP 中继、PSTN 网关或 ELIN 网关的路由路径的 PSTN 用法名称。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>一个用法只能分配给一个位置策略。此 PSTN 用法覆盖分配给用户语音策略的 PSTN 用法，但仅适用于紧急拨号字符串或紧急拨号字符串掩码之一发出的呼叫。</td>
    </tr>
    </tbody>
    </table>


<!-- end list -->

  - **通知 URI**  
    指定要在发出紧急呼叫时接收即时消息 (IM) 通知的安全人员的一个或多个 SIP URI。支持通讯组。

<!-- end list -->

  - **会议 URI**  
    指定在发出紧急呼叫时应加入会议的外线直拨分机 (DID) 号码（通常是安全服务台号码）。

<!-- end list -->

  - **会议模式**  
    指定会议 URI 将使用单向还是双向通信加入紧急呼叫。

<!-- end list -->

  - **位置刷新间隔**  
    指定对 位置信息服务位置更新的客户端请求之间的时间量（小时）。该值可以设置为 1 和 12 之间的任意值。默认值为 4。

