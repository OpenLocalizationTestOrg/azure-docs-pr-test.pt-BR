---
title: "Recursos e configurações do serviço de sincronização do Azure AD Connect | Microsoft Docs"
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
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="c1f98-103">Recursos do serviço de sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c1f98-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="c1f98-104">O recurso de sincronização do Azure AD Connect tem dois componentes:</span><span class="sxs-lookup"><span data-stu-id="c1f98-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="c1f98-105">O componente local denominado **Sincronização do Azure AD Connect**, também chamado de **mecanismo de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="c1f98-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="c1f98-106">O serviço que reside no Azure AD, também conhecido como **Serviço de sincronização do Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="c1f98-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="c1f98-107">Este tópico explica como os seguintes recursos do **Serviço de sincronização do Azure AD Connect** funcionam e como você pode configurá-los usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1f98-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="c1f98-108">Estas configurações são definidas pelo [Módulo do Azure Active Directory para Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="c1f98-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="c1f98-109">Baixe e instale-o separadamente do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c1f98-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="c1f98-110">Os cmdlets documentados neste tópico foram introduzidos na [versão de março de 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="c1f98-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="c1f98-111">Se você não tiver os cmdlets documentados neste tópico ou se eles não produzirem o mesmo resultado, certifique-se de executar a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="c1f98-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="c1f98-112">Para ver a configuração em seu diretório do Azure AD, execute `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="c1f98-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="c1f98-113">![Resultado de Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="c1f98-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="c1f98-114">Muitas dessas configurações podem ser alteradas somente pelo Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c1f98-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="c1f98-115">As configurações a seguir podem ser definidas por `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="c1f98-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="c1f98-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="c1f98-116">DirSyncFeature</span></span> | <span data-ttu-id="c1f98-117">Comentário</span><span class="sxs-lookup"><span data-stu-id="c1f98-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="c1f98-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="c1f98-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="c1f98-119">Permite que os objetos se unam em userPrincipalName além do endereço SMTP primário.</span><span class="sxs-lookup"><span data-stu-id="c1f98-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="c1f98-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="c1f98-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="c1f98-121">Permite que o mecanismo de sincronização atualize o atributo userPrincipalName para usuários gerenciados/licenciados (não federados).</span><span class="sxs-lookup"><span data-stu-id="c1f98-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="c1f98-122">Depois que você habilitar um recurso, ele não poderá ser desabilitado novamente.</span><span class="sxs-lookup"><span data-stu-id="c1f98-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="c1f98-123">A partir de 24 de agosto de 2016 o recurso *Duplicar a resiliência do atributo* é habilitado por padrão para novos diretórios do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1f98-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="c1f98-124">Este recurso também será distribuído e habilitado em diretórios criados antes dessa data.</span><span class="sxs-lookup"><span data-stu-id="c1f98-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="c1f98-125">Você receberá uma notificação por email quando o diretório estiver prestes a habilitar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c1f98-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="c1f98-126">As configurações a seguir são definidas pelo Azure AD Connect e não podem ser modificadas por `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="c1f98-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="c1f98-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="c1f98-127">DirSyncFeature</span></span> | <span data-ttu-id="c1f98-128">Comentário</span><span class="sxs-lookup"><span data-stu-id="c1f98-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="c1f98-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="c1f98-129">DeviceWriteback</span></span> |[<span data-ttu-id="c1f98-130">Azure AD Connect: habilitando o write-back do dispositivo</span><span class="sxs-lookup"><span data-stu-id="c1f98-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="c1f98-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="c1f98-131">DirectoryExtensions</span></span> |[<span data-ttu-id="c1f98-132">Sincronização do Azure AD Connect: extensões do Directory</span><span class="sxs-lookup"><span data-stu-id="c1f98-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="c1f98-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="c1f98-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="c1f98-134">Permite que um atributo seja colocado em quarentena quando ele é uma duplicata de outro objeto, em vez de causar falha de todo o objeto durante a exportação.</span><span class="sxs-lookup"><span data-stu-id="c1f98-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="c1f98-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="c1f98-135">PasswordSync</span></span> |[<span data-ttu-id="c1f98-136">Implementação de sincronização de senha com a sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c1f98-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="c1f98-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="c1f98-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="c1f98-138">Visualização: write-back de grupo</span><span class="sxs-lookup"><span data-stu-id="c1f98-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="c1f98-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="c1f98-139">UserWriteback</span></span> |<span data-ttu-id="c1f98-140">Não há suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="c1f98-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="c1f98-141">Duplicar a resiliência do atributo</span><span class="sxs-lookup"><span data-stu-id="c1f98-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="c1f98-142">Em vez de falhar ao provisionar objetos com UPNs/proxyAddresses duplicados, o atributo duplicado é "colocado em quarentena" e um valor temporário é atribuído.</span><span class="sxs-lookup"><span data-stu-id="c1f98-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="c1f98-143">Quando o conflito é resolvido, o UPN temporário é alterado para o valor correto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c1f98-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="c1f98-144">Para obter mais detalhes, consulte [Sincronização de identidades e resiliência do atributo duplicado](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="c1f98-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="c1f98-145">Correspondência suave de UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="c1f98-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="c1f98-146">Quando este recurso é habilitado, a correspondência suave é habilitada para UPN além do [endereço SMTP primário](https://support.microsoft.com/kb/2641663), que está sempre habilitado.</span><span class="sxs-lookup"><span data-stu-id="c1f98-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="c1f98-147">A correspondência suave é usada para fazer a correspondência de usuários na nuvem existentes no Azure AD com usuários locais.</span><span class="sxs-lookup"><span data-stu-id="c1f98-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="c1f98-148">Se você precisar corresponder as contas AD locais com contas existentes criadas na nuvem e você não estiver usando o Exchange Online, este recurso será útil.</span><span class="sxs-lookup"><span data-stu-id="c1f98-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="c1f98-149">Nesse cenário, você normalmente não tem um motivo para definir o atributo SMTP na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c1f98-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="c1f98-150">O recurso fica ativado por padrão para diretórios recém-criados do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1f98-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="c1f98-151">Você pode ver se este recurso está habilitado executando:</span><span class="sxs-lookup"><span data-stu-id="c1f98-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="c1f98-152">Se o recurso não estiver habilitado para seu diretório do Azure AD, você poderá habilitá-lo executando:</span><span class="sxs-lookup"><span data-stu-id="c1f98-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="c1f98-153">Sincronizar atualizações de userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="c1f98-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="c1f98-154">Historicamente, atualizações do atributo UserPrincipalName usando o serviço de sincronização local são bloqueadas, a menos que estas duas condições sejam verdadeiras:</span><span class="sxs-lookup"><span data-stu-id="c1f98-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="c1f98-155">O usuário é gerenciado (não federado).</span><span class="sxs-lookup"><span data-stu-id="c1f98-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="c1f98-156">Não foi atribuída uma licença ao usuário.</span><span class="sxs-lookup"><span data-stu-id="c1f98-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="c1f98-157">Para obter mais detalhes, consulte [Os nomes de usuário no Office 365, Azure ou Intune não coincidem com o UPN local ou ID de logon alternativo](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="c1f98-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="c1f98-158">Habilitar o recurso permite que o mecanismo de sincronização atualize o userPrincipalName quando ele é alterado localmente e você usa a sincronização da senha.</span><span class="sxs-lookup"><span data-stu-id="c1f98-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="c1f98-159">Se você usar a federação, não haverá suporte pra este recurso.</span><span class="sxs-lookup"><span data-stu-id="c1f98-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="c1f98-160">O recurso fica ativado por padrão para diretórios recém-criados do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1f98-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="c1f98-161">Você pode ver se este recurso está habilitado executando:</span><span class="sxs-lookup"><span data-stu-id="c1f98-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="c1f98-162">Se o recurso não estiver habilitado para seu diretório do Azure AD, você poderá habilitá-lo executando:</span><span class="sxs-lookup"><span data-stu-id="c1f98-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="c1f98-163">Depois de habilitar esse recurso, os valores existentes de userPrincipalName permanecerão os mesmos.</span><span class="sxs-lookup"><span data-stu-id="c1f98-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="c1f98-164">Na próxima alteração do atributo userPrincipalName local, a sincronização delta normal dos usuários atualizará o UPN.</span><span class="sxs-lookup"><span data-stu-id="c1f98-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="c1f98-165">Confira também</span><span class="sxs-lookup"><span data-stu-id="c1f98-165">See also</span></span>
* [<span data-ttu-id="c1f98-166">Sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c1f98-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="c1f98-167">[Integração de suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c1f98-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

