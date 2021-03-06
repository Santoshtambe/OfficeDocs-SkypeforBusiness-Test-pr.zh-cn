﻿---
title: 使用用户标识的 Cmdlet
TOCTitle: 使用用户标识的 Cmdlet
ms:assetid: be87409f-6372-4c70-91ac-6ef13dfbe65a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn362842(v=OCS.15)
ms:contentKeyID: 56271200
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 使用用户标识的 Cmdlet

 

_**上一次修改主题：** 2015-06-22_

在 Skype for Business Online 中，有许多不同的方法可引用单个用户标识：

  - 使用用户的 Active Directory 域服务显示名称。例如：
    
        -Identity "Ken Myer"

  - 使用用户的 SIP 地址。例如：
    
        -Identity "sip:kenmyer@litwareinc.com"

  - 使用用户的 UPN。例如：
    
        -Identity " kenmyer@litwareinc.com"

  - 使用用户的 Active Directory 域服务可分辨名称。例如：
    
        -Identity "CN=48ebd1ba-95d4-460c-b751-811ebf0c4611,OU=fa8226f5-14fa-46da-8 236-039b25bc7a27,OU=Lync Online Tenants,DC=litwareinc,DC=com"

以下 cmdlet 接受用户标识：

  - [Disable-CsMeetingRoom](disable-csmeetingroom.md)

  - [Enable-CsMeetingRoom](enable-csmeetingroom.md)

  - [Get-CsExUmContact](get-csexumcontact.md)

  - [Get-CsMeetingRoom](get-csmeetingroom.md)

  - [Get-CsOnlineUser](get-csonlineuser.md)

  - [Get-CsUserAcp](get-csuseracp.md)

  - [New-CsExUmContact](new-csexumcontact.md)

  - [Remove-CsExUmContact](remove-csexumcontact.md)

  - [Remove-CsUserAcp](remove-csuseracp.md)

  - [Set-CsExUmContact](set-csexumcontact.md)

  - [Set-CsMeetingRoom](set-csmeetingroom.md)

  - [Set-CsUserAcp](set-csuseracp.md)

请注意，在调用其中一个 **Get-Cs** cmdlet 时，您无需指定用户标识。在这种情况下，cmdlet 将返回指定项目的所有实例。例如，此命令返回有关已启用 Skype for Business Online 的所有用户的信息：

    Get-CsOnlineUser

只有当您想要返回特定用户的信息时，才需要 Identity 参数：

    Get-CsOnlineUser -Identity "Ken Myer"

## 另请参阅

#### 概念

[标识、作用域和租户](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online Cmdlet](the-skype-for-business-online-cmdlets.md)

