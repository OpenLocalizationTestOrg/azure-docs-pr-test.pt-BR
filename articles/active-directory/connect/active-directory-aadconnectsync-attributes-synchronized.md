---
title: Atributos sincronizados pelo Azure AD Connect | Microsoft Docs
description: "Atributos de saudação de listas que são sincronizados tooAzure do Active Directory."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Sincronização do Azure AD Connect: atributos sincronizados tooAzure do Active Directory
Este tópico lista os atributos de saudação que são sincronizados pela sincronização do Azure AD Connect.  
Olá atributos são agrupados por Olá relacionados ao aplicativo do Azure AD.

## <a name="attributes-toosynchronize"></a>Atributos toosynchronize
Uma pergunta comum é *Olá lista de atributos mínimos toosynchronize*. padrão de saudação e a abordagem recomendada é atributos do tookeep saudação padrão para que um total GAL (lista de endereços Global) pode ser construído em Olá nuvem e tooget todos os recursos em cargas de trabalho do Office 365. Em alguns casos, há alguns atributos que sua organização não deseja toohello sincronizado nuvem desde que esses atributos contêm confidenciais ou dados do PII (informações de identificação pessoal), como neste exemplo:  
![atributos incorretos](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

Nesse caso, inicie com lista de saudação de atributos neste tópico e identificar os atributos que contém dados PII ou confidenciais e não podem ser sincronizados. Então, desmarque-os durante a instalação usando o [aplicativo Azure AD e a filtragem de atributos](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Ao cancelar a seleção de atributos, seja cuidadoso e desmarque apenas esses toosynchronize absolutamente não é possível de atributos. Desmarcar outros atributos poderá causar um impacto negativo sobre os recursos.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Nome do atributo | Usuário | Comentário |
| --- |:---:| --- |
| accountEnabled |X |Define se uma conta está habilitada. |
| cn |X | |
| displayName |X | |
| objectSID |X |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| pwdLastSet |X |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. Usado pela sincronização de senha e pela federação. |
| sourceAnchor |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| usageLocation |X |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userPrincipalName |X |UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |

## <a name="exchange-online"></a>Exchange Online
| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se uma conta está habilitada. |
| assistente |X |X | | |
| altRecipient |X | | |Exige o Azure AD Connect, build 1.1.552.0 ou posterior. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| homePhone |X |X | | |
| informações |X |X |X |Atualmente, este atributo não é consumido para grupos. |
| Initials |X |X | | |
| l |X |X | | |
| legacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| Serviço Móvel |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Disponível no Azure AD Connect versão 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Atualmente, este atributo não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Atualmente, este atributo não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Atualmente, este atributo não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Atualmente, este atributo não é consumido pelo Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Atualmente, este atributo não é consumido pelo Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg-IsOrganizational | | |X | |
| objectSID |X | |X |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. Usado pela sincronização de senha e pela federação. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Derivado de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se uma conta está habilitada. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homePhone |X |X | | |
| informações |X |X |X | |
| Initials |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| middleName |X |X | | |
| Serviço Móvel |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| otherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. Usado pela sincronização de senha e pela federação. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Derivado de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| unauthOrig |X |X |X | |
| url |X |X | | |
| usageLocation |X | | |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userPrincipalName |X | | |UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se uma conta está habilitada. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homePhone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| Serviço Móvel |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. Usado pela sincronização de senha e pela federação. |
| securityEnabled | | |X |Derivado de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| título |X |X | | |
| usageLocation |X | | |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userPrincipalName |X | | |UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se uma conta está habilitada. |
| cn |X | |X |Alias ou nome comum. Geralmente prefixo Olá de valor [email]. |
| displayName |X |X |X |Uma cadeia de caracteres que representa o nome hello geralmente exibido como o nome amigável da saudação (nome sobrenome). |
| mail |X |X |X |endereço de email completo. |
| member | | |X | |
| objectSID |X | |X |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| proxyAddresses |X |X |X |propriedade mecânica. Usado pelo AD do Azure. Contém todos os endereços de email secundários para o usuário hello. |
| pwdLastSet |X | | |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. |
| securityEnabled | | |X |Derivado de groupType. |
| sourceAnchor |X |X |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| usageLocation |X | | |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userPrincipalName |X | | |Este UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |

## <a name="intune"></a>Intune
| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se uma conta está habilitada. |
| c |X |X | | |
| cn |X | |X | |
| description |X |X |X | |
| displayName |X |X |X | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | |X |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. Usado pela sincronização de senha e pela federação. |
| securityEnabled | | |X |Derivado de groupType |
| sourceAnchor |X |X |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| usageLocation |X | | |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userPrincipalName |X | | |UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se uma conta está habilitada. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| Serviço Móvel |X |X | | |
| objectSID |X | |X |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. Usado pela sincronização de senha e pela federação. |
| securityEnabled | | |X |Derivado de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| título |X |X | | |
| usageLocation |X | | |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userPrincipalName |X | | |UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |

## <a name="3rd-party-applications"></a>aplicativos de terceira parte
Esse grupo é um conjunto de atributos usados como Olá atributos mínimos necessários para uma carga de trabalho genérica ou o aplicativo. Ele pode ser usado para uma carga de trabalho não listada em outra seção ou para um aplicativo não Microsoft. Explicitamente, ela é usada para seguir hello:

* Yammer (somente o Usuário é consumido)
* [Cenários de colaboração híbrida entre organizações B2B (entre empresas) oferecidos por recursos como o SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Esse grupo é um conjunto de atributos que podem ser usados se o diretório do AD do Azure Olá não é usada toosupport Office 365, Dynamics ou Intune. Ele tem um pequeno conjunto de atributos principais.

| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Define se uma conta está habilitada. |
| cn |X | |X | |
| displayName |X |X |X | |
| givenName |X |X | | |
| mail |X | |X | |
| managedBy | | |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | | |propriedade mecânica. Identificador de usuário do AD usado toomaintain sincronização entre o Azure AD e do AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriedade mecânica. Tooknow usado quando tooinvalidate já os tokens emitidos. Usado pela sincronização de senha e pela federação. |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriedade mecânica. Relação de toomaintain identificador imutável entre o ADDS e o AD do Azure. |
| usageLocation |X | | |propriedade mecânica. País saudação do usuário. Usado para atribuição de licença. |
| userPrincipalName |X | | |UPN é a ID de logon de saudação do usuário hello. Olá geralmente igual ao valor [email]. |

## <a name="windows-10"></a>Windows 10
Um computer(device) de domínio do Windows 10 sincroniza tooAzure alguns atributos AD. Para obter mais informações sobre cenários de hello, consulte [conectar dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](../active-directory-azureadjoin-devices-group-policy.md). Esses atributos sempre são sincronizados e o Windows 10 não aparece como um aplicativo que pode ser desmarcado. Um computador ingressado no domínio do Windows 10 é identificado por ter Olá atributo userCertificate preenchido.

| Nome do atributo | Dispositivo | Comentário |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |Valor fixo no código para computadores ingressados do domínio. |
| displayName |X | |
| ms-DS-CreatorSID |X |Também chamado de registeredOwnerReference. |
| objectGUID |X |Também chamado de deviceID. |
| objectSID |X |Também chamado de onPremisesSecurityIdentifier. |
| operatingSystem |X |Também chamado de deviceOSType. |
| operatingSystemVersion |X |Também chamado de deviceOSVersion. |
| userCertificate |X | |

Esses atributos para **usuário** é toohello além de outros aplicativos que você selecionou.  

| Nome do atributo | Usuário | Comentário |
| --- |:---:| --- |
| domainFQDN |X |Também chamado de dnsDomainName. Por exemplo, contoso.com. |
| domainNetBios |X |Também chamado de netBiosName. Por exemplo, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Write-back híbrido do Exchange
Esses atributos são gravados do AD do Azure tooon local do Active Directory quando você seleciona tooenable **híbrida do Exchange**. Dependendo da sua versão do Exchange, menos atributos poderão ser sincronizados.

| Nome do atributo | Usuário | Contato | Agrupar | Comentário |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Derivado de cloudAnchor no AD do Azure. Esse atributo é novo no AD do Windows Server 2016 e Exchange 2016. |
| msExchArchiveStatus |X | | |Arquivamento on-line: Mail tooarchive permite que os clientes. |
| msExchBlockedSendersHash |X | | |Filtragem: faz write-back de dados de remetentes bloqueados e seguros de filtragem local e online por meio de clientes. |
| msExchSafeRecipientsHash |X | | |Filtragem: faz write-back de dados de remetentes bloqueados e seguros de filtragem local e online por meio de clientes. |
| msExchSafeSendersHash |X | | |Filtragem: faz write-back de dados de remetentes bloqueados e seguros de filtragem local e online por meio de clientes. |
| msExchUCVoiceMailSettings |X | | |Habilitar Unificação de mensagens (UM) - postal Online: usado pelo Microsoft Lync Server integração tooindicate tooLync servidor local que o usuário Olá tem postal nos serviços online. |
| msExchUserHoldPolicies |X | | |Litígio: Habilita toodetermine de serviços de nuvem que os usuários estão em litígio. |
| proxyAddresses |X |X |X |Somente Olá x500 endereço do Exchange Online é inserido. |
| publicDelegates |X | | |Permite que um toobe de caixa de correio Exchange Online concedidas SendOnBehalfTo direitos toousers com caixa de correio do Exchange no local. Exige o Azure AD Connect, build 1.1.552.0 ou posterior. |

## <a name="exchange-mail-public-folder"></a>Pasta pública do Exchange Mail
Esses atributos são sincronizados do local do Active Directory tooAzure AD quando você seleciona tooenable **pasta pública do Exchange Mail**.

| Nome do atributo | PublicFolder | Comentário |
| --- | :---:| --- |
| displayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Write-back de dispositivo
Os objetos do dispositivo são criados no Active Directory. Esses objetos podem ser dispositivos ligados tooAzure AD ou computadores com Windows 10 ingressados no domínio.

| Nome do atributo | Dispositivo | Comentário |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| displayName |X | |
| dn |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Somente com o esquema do AD do Windows Server 2016 |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Observações
* Quando usar uma ID alternativa, hello local atributo userPrincipalName é sincronizada com onPremisesUserPrincipalName de atributo do AD do Azure hello. Olá atributo ID alternativo, como email, está sincronizado com hello AD do Azure atributo userPrincipalName.
* Em listas de saudação acima, Olá o tipo de objeto **usuário** também se aplica o tipo de objeto toohello **iNetOrgPerson**.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
