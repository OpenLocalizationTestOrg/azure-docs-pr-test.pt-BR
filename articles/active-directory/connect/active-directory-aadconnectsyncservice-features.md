---
title: "recursos e a configuração de serviço aaaAzure AD Connect sincronização | Microsoft Docs"
description: "Descreve os recursos do serviço de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="583b1-103">Recursos do serviço de sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="583b1-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="583b1-104">recurso de sincronização de saudação do Azure AD Connect tem dois componentes:</span><span class="sxs-lookup"><span data-stu-id="583b1-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="583b1-105">componente de local de saudação denominado **sincronização do Azure AD Connect**, também chamado **mecanismo de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="583b1-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="583b1-106">serviço Olá residentes no AD do Azure, também conhecido como **o serviço de sincronização do Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="583b1-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="583b1-107">Este tópico explica como os recursos a seguir de saudação do hello **o serviço de sincronização do Azure AD Connect** funcionam e como você pode configurá-los usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="583b1-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="583b1-108">Essas configurações são definidas por Olá [Azure módulo Active Directory para Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="583b1-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="583b1-109">Baixe e instale-o separadamente do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="583b1-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="583b1-110">cmdlets de saudação documentadas neste tópico foram introduzidos no hello [versão de março de 2016 (compilação 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="583b1-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="583b1-111">Se você não tem os cmdlets de saudação documentados neste tópico ou eles não produzem Olá mesmo resultado, em seguida, certifique-se de você executar a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="583b1-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="583b1-112">configuração de saudação toosee em seu diretório do AD do Azure, execute `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="583b1-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="583b1-113">![Resultado de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="583b1-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="583b1-114">Muitas dessas configurações podem ser alteradas somente pelo Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="583b1-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="583b1-115">Olá configurações a seguir podem ser configuradas por `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="583b1-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="583b1-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="583b1-116">DirSyncFeature</span></span> | <span data-ttu-id="583b1-117">Comentário</span><span class="sxs-lookup"><span data-stu-id="583b1-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="583b1-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="583b1-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="583b1-119">Permite que objetos toojoin userPrincipalName no endereço de tooprimary SMTP de adição.</span><span class="sxs-lookup"><span data-stu-id="583b1-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="583b1-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="583b1-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="583b1-121">Permite atributo do hello sincronização mecanismo tooupdate Olá userPrincipalName gerenciados/licenciado usuários (não federados).</span><span class="sxs-lookup"><span data-stu-id="583b1-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="583b1-122">Depois que você habilitar um recurso, ele não poderá ser desabilitado novamente.</span><span class="sxs-lookup"><span data-stu-id="583b1-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="583b1-123">De 24 de agosto de 2016 Olá recurso *duplicado resiliência do atributo* é habilitado por padrão para o novo Azure diretórios do AD.</span><span class="sxs-lookup"><span data-stu-id="583b1-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="583b1-124">Este recurso também será distribuído e habilitado em diretórios criados antes dessa data.</span><span class="sxs-lookup"><span data-stu-id="583b1-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="583b1-125">Você receberá uma notificação por email quando o diretório é sobre tooget esse recurso habilitado.</span><span class="sxs-lookup"><span data-stu-id="583b1-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="583b1-126">Olá configurações a seguir são configuradas pelo Azure AD Connect e não pode ser modificadas por `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="583b1-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="583b1-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="583b1-127">DirSyncFeature</span></span> | <span data-ttu-id="583b1-128">Comentário</span><span class="sxs-lookup"><span data-stu-id="583b1-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="583b1-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="583b1-129">DeviceWriteback</span></span> |[<span data-ttu-id="583b1-130">Azure AD Connect: habilitando o write-back do dispositivo</span><span class="sxs-lookup"><span data-stu-id="583b1-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="583b1-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="583b1-131">DirectoryExtensions</span></span> |[<span data-ttu-id="583b1-132">Sincronização do Azure AD Connect: extensões do Directory</span><span class="sxs-lookup"><span data-stu-id="583b1-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="583b1-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="583b1-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="583b1-134">Permite que um toobe de atributo em quarentena quando ele é uma duplicata de outro objeto, em vez de falha do objeto inteiro Olá durante a exportação.</span><span class="sxs-lookup"><span data-stu-id="583b1-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="583b1-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="583b1-135">PasswordSync</span></span> |[<span data-ttu-id="583b1-136">Implementação de sincronização de senha com a sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="583b1-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="583b1-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="583b1-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="583b1-138">Visualização: write-back de grupo</span><span class="sxs-lookup"><span data-stu-id="583b1-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="583b1-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="583b1-139">UserWriteback</span></span> |<span data-ttu-id="583b1-140">Não há suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="583b1-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="583b1-141">Duplicar a resiliência do atributo</span><span class="sxs-lookup"><span data-stu-id="583b1-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="583b1-142">Em vez de falhar tooprovision objetos com UPNs duplicados / proxyAddresses, atributo duplicado Olá é "em quarentena" e um valor temporário é atribuído.</span><span class="sxs-lookup"><span data-stu-id="583b1-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="583b1-143">Quando a saudação conflito é resolvido, Olá temporário UPN é alterada automaticamente o valor adequado toohello.</span><span class="sxs-lookup"><span data-stu-id="583b1-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="583b1-144">Para obter mais detalhes, consulte [Sincronização de identidades e resiliência do atributo duplicado](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="583b1-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="583b1-145">Correspondência suave de UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="583b1-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="583b1-146">Quando esse recurso está habilitado, correspondência de software está habilitada para UPN na adição toohello [endereço SMTP primário](https://support.microsoft.com/kb/2641663), que está sempre habilitado.</span><span class="sxs-lookup"><span data-stu-id="583b1-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="583b1-147">Soft-match é usado toomatch usuários de nuvem existente no AD do Azure com usuários locais.</span><span class="sxs-lookup"><span data-stu-id="583b1-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="583b1-148">Se você precisar toomatch contas com contas existentes criadas na nuvem de saudação do AD local e você não estiver usando o Exchange Online, esse recurso é útil.</span><span class="sxs-lookup"><span data-stu-id="583b1-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="583b1-149">Nesse cenário, você geralmente não tem um atributo de SMTP do motivo tooset Olá na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="583b1-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="583b1-150">O recurso fica ativado por padrão para diretórios recém-criados do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="583b1-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="583b1-151">Você pode ver se este recurso está habilitado executando:</span><span class="sxs-lookup"><span data-stu-id="583b1-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="583b1-152">Se o recurso não estiver habilitado para seu diretório do Azure AD, você poderá habilitá-lo executando:</span><span class="sxs-lookup"><span data-stu-id="583b1-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="583b1-153">Sincronizar atualizações de userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="583b1-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="583b1-154">Historicamente, atributo de UserPrincipalName toohello atualizações usando o serviço de sincronização de saudação do local foi bloqueado, a menos que as duas condições forem verdadeiras:</span><span class="sxs-lookup"><span data-stu-id="583b1-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="583b1-155">usuário Olá é gerenciado (não federados).</span><span class="sxs-lookup"><span data-stu-id="583b1-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="583b1-156">não foi atribuído uma licença ao usuário Hello.</span><span class="sxs-lookup"><span data-stu-id="583b1-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="583b1-157">Para obter mais detalhes, consulte [usuário nomes no Office 365, Azure ou Intune não correspondem Olá UPN local ou ID de logon alternativo](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="583b1-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="583b1-158">Habilitar esse recurso permite Olá sincronização mecanismo tooupdate Olá userPrincipalName quando ele for alterado no local e você usar a sincronização de senha. Se você usar a federação, não haverá suporte pra este recurso.</span><span class="sxs-lookup"><span data-stu-id="583b1-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="583b1-159">O recurso fica ativado por padrão para diretórios recém-criados do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="583b1-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="583b1-160">Você pode ver se este recurso está habilitado executando:</span><span class="sxs-lookup"><span data-stu-id="583b1-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="583b1-161">Se o recurso não estiver habilitado para seu diretório do Azure AD, você poderá habilitá-lo executando:</span><span class="sxs-lookup"><span data-stu-id="583b1-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="583b1-162">Depois de habilitar esse recurso, os valores existentes de userPrincipalName permanecerão os mesmos.</span><span class="sxs-lookup"><span data-stu-id="583b1-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="583b1-163">Na próxima alteração de saudação userPrincipalName atributo local, sincronização de delta normal de saudação em usuários atualizará Olá UPN.</span><span class="sxs-lookup"><span data-stu-id="583b1-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="583b1-164">Consulte também</span><span class="sxs-lookup"><span data-stu-id="583b1-164">See also</span></span>
* [<span data-ttu-id="583b1-165">Sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="583b1-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="583b1-166">[Integração de suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="583b1-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

