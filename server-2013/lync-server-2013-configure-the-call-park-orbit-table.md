﻿---
title: Lync Server 2013：配置呼叫寄存通道表
TOCTitle: 配置呼叫寄存通道表
ms:assetid: e5cc0c19-7b2c-48e7-a21d-cfb23c842f0f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg399020(v=OCS.15)
ms:contentKeyID: 49314554
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中配置呼叫寄存通道表

 

_**上一次修改主题：** 2012-09-10_

呼叫寄存使用通道来寄存呼叫。用户必须先配置 呼叫寄存通道表，然后才能寄存和取回呼叫。您需要指定组织将保留用于寄存呼叫的分机号（通道）范围，并通过指定处理每个范围的 呼叫寄存池来定义这些范围的路由。定义通道范围时，目标是具有足够的通道，以便不会在短时间内重用任何一个通道，但又不能有太多通道，以致于不得不限制用户或其他服务可使用的分机数量。您可以为部署了 呼叫寄存应用程序的每个 Lync Server 池创建多个 呼叫寄存通道范围。每个 呼叫寄存通道范围必须具有全局唯一的名称和唯一的分机集合。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每个通道范围包含的通道数通常不超过 100。范围可以更大一点，只要每个范围的通道数小于最大值 10,000 且每个池的通道数小于 50,000。如果范围太小，很快就会重用通道。</td>
</tr>
</tbody>
</table>


请使用虚拟分机（未向其分配用户或电话的分机）块作为通道范围。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支持将外线直拨分机 (DID) 号码分配为 呼叫寄存通道表中的通道号码。</td>
</tr>
</tbody>
</table>


## 本部分内容

[在 Lync Server 2013 中创建或修改呼叫寄存通道范围](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)

