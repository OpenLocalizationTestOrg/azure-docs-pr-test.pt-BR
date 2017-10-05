---
title: "Atributos sombra do serviço de sincronização do Azure AD Connect | Microsoft Docs"
description: "Descreve como os atributos sombra funcionam no serviço de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 0b6a7f22d744480a40a878c979986cdd7667109c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="142fd-103">Atributos sombra do serviço de sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="142fd-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="142fd-104">A maioria dos atributos é representada da mesma maneira no Azure AD e no Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="142fd-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="142fd-105">Mas alguns atributos têm tratamentos especiais, e o valor do atributo no Azure AD pode ser diferente do que é sincronizado no Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="142fd-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="142fd-106">Introdução aos atributos sombra</span><span class="sxs-lookup"><span data-stu-id="142fd-106">Introducing shadow attributes</span></span>
<span data-ttu-id="142fd-107">Alguns atributos têm duas representações no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="142fd-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="142fd-108">O valor local e um valor calculado são armazenados.</span><span class="sxs-lookup"><span data-stu-id="142fd-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="142fd-109">Esses atributos adicionais são chamados de atributos sombra.</span><span class="sxs-lookup"><span data-stu-id="142fd-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="142fd-110">Os dois atributos mais comuns nos quais é possível ver esse comportamento são **userPrincipalName** e **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="142fd-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="142fd-111">A alteração nos valores de atributo ocorre quando há valores nesses atributos que representam domínios não verificados.</span><span class="sxs-lookup"><span data-stu-id="142fd-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="142fd-112">Mas o mecanismo de sincronização no Connect lê o valor do atributo sombra e, da perspectiva dele, o atributo foi confirmado pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="142fd-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="142fd-113">Não é possível ver os atributos sombra usando o portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="142fd-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="142fd-114">Mas entender o conceito ajuda você a solucionar determinados cenários nos quais o atributo tem valores diferentes no local e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="142fd-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="142fd-115">Para entender melhor o comportamento, veja este exemplo da Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="142fd-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![Domínios](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="142fd-117">Eles têm vários sufixos UPN no Active Directory local, mas verificaram apenas um.</span><span class="sxs-lookup"><span data-stu-id="142fd-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="142fd-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="142fd-118">userPrincipalName</span></span>
<span data-ttu-id="142fd-119">Um usuário tem os seguintes valores de atributo em um domínio não verificado:</span><span class="sxs-lookup"><span data-stu-id="142fd-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="142fd-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="142fd-120">Attribute</span></span> | <span data-ttu-id="142fd-121">Valor</span><span class="sxs-lookup"><span data-stu-id="142fd-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="142fd-122">userPrincipalName local</span><span class="sxs-lookup"><span data-stu-id="142fd-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="142fd-123">shadowUserPrincipalName do Azure AD</span><span class="sxs-lookup"><span data-stu-id="142fd-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="142fd-124">userPrincipalName do Azure AD</span><span class="sxs-lookup"><span data-stu-id="142fd-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="142fd-125">O atributo userPrincipalName é o valor que você vê ao usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="142fd-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="142fd-126">Como o valor do atributo real local é armazenado no Azure AD, quando você verifica o domínio fabrikam.com, o Azure AD atualiza o atributo userPrincipalName com o valor de shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="142fd-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="142fd-127">Não é necessário sincronizar as alterações no Azure AD Connect para que esses valores sejam atualizados.</span><span class="sxs-lookup"><span data-stu-id="142fd-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="142fd-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="142fd-128">proxyAddresses</span></span>
<span data-ttu-id="142fd-129">O mesmo processo para incluir somente os domínios verificados também ocorre para proxyAddresses, mas com alguma lógica adicional.</span><span class="sxs-lookup"><span data-stu-id="142fd-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="142fd-130">A verificação de domínios verificados ocorre apenas para usuários de caixa de correio.</span><span class="sxs-lookup"><span data-stu-id="142fd-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="142fd-131">Um usuário ou contato habilitado para email representa um usuário em outra organização do Exchange, e você pode adicionar quaisquer valores no proxyAddresses a esses objetos.</span><span class="sxs-lookup"><span data-stu-id="142fd-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="142fd-132">Para um usuário de caixa de correio, no local ou no Exchange Online, somente os valores de domínios verificados são exibidos.</span><span class="sxs-lookup"><span data-stu-id="142fd-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="142fd-133">O resultado pode ser este:</span><span class="sxs-lookup"><span data-stu-id="142fd-133">It could look like this:</span></span>

| <span data-ttu-id="142fd-134">Atributo</span><span class="sxs-lookup"><span data-stu-id="142fd-134">Attribute</span></span> | <span data-ttu-id="142fd-135">Valor</span><span class="sxs-lookup"><span data-stu-id="142fd-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="142fd-136">proxyAddresses local</span><span class="sxs-lookup"><span data-stu-id="142fd-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="142fd-137">proxyAddresses do Exchange Online</span><span class="sxs-lookup"><span data-stu-id="142fd-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="142fd-138">Nesse caso, **smtp:abbie.spencer@fabrikam.com** foi removido, pois esse domínio não foi verificado.</span><span class="sxs-lookup"><span data-stu-id="142fd-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="142fd-139">Mas o Exchange também adicionou **SIP:abbie.spencer@fabrikamonline.com**.</span><span class="sxs-lookup"><span data-stu-id="142fd-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="142fd-140">A Fabrikam não usou o Lync/Skype local, mas o Azure AD e o Exchange Online se preparam para isso.</span><span class="sxs-lookup"><span data-stu-id="142fd-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="142fd-141">Essa lógica para proxyAddresses é conhecida como **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="142fd-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="142fd-142">ProxyCalc é invocado a cada alteração em um usuário, quando:</span><span class="sxs-lookup"><span data-stu-id="142fd-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="142fd-143">O usuário tiver recebido um plano de serviço que inclua o Exchange Online mesmo não tendo licença para o Exchange.</span><span class="sxs-lookup"><span data-stu-id="142fd-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="142fd-144">Por exemplo, se o usuário receber a SKU do Office E3, mas só com o SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="142fd-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="142fd-145">Isso será verdadeiro mesmo se sua caixa de correio ainda for local.</span><span class="sxs-lookup"><span data-stu-id="142fd-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="142fd-146">O atributo msExchRecipientTypeDetails tem um valor.</span><span class="sxs-lookup"><span data-stu-id="142fd-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="142fd-147">Você faz uma alteração no proxyAddresses ou no userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="142fd-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="142fd-148">ProxyCalc pode levar algum tempo para processar uma alteração em um usuário, e não é síncrono com o processo de exportação do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="142fd-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="142fd-149">A lógica do ProxyCalc tem alguns comportamentos adicionais para cenários avançados não documentados neste tópico.</span><span class="sxs-lookup"><span data-stu-id="142fd-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="142fd-150">Este tópico é fornecido para você entender o comportamento, e não documentar toda a lógica interna.</span><span class="sxs-lookup"><span data-stu-id="142fd-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="142fd-151">Valores de atributo em quarentena</span><span class="sxs-lookup"><span data-stu-id="142fd-151">Quarantined attribute values</span></span>
<span data-ttu-id="142fd-152">Os atributos sombra também são usados quando há valores de atributo duplicados.</span><span class="sxs-lookup"><span data-stu-id="142fd-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="142fd-153">Para saber mais, veja [resiliência de atributo duplicada](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="142fd-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="142fd-154">Consulte também</span><span class="sxs-lookup"><span data-stu-id="142fd-154">See also</span></span>
* [<span data-ttu-id="142fd-155">Sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="142fd-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="142fd-156">[Integração de suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="142fd-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
