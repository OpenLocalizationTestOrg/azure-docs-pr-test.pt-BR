---
title: "atributos de sombra de serviço de sincronização do aaaAzure AD Connect | Microsoft Docs"
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
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="4d278-103">Atributos sombra do serviço de sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4d278-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="4d278-104">A maioria dos atributos são representados Olá mesma maneira no AD do Azure como estão no Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="4d278-104">Most attributes are represented hello same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="4d278-105">Mas alguns atributos têm algum tratamento especial e o valor do atributo Olá no AD do Azure pode ser diferente do que sincroniza o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4d278-105">But some attributes have some special handling and hello attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="4d278-106">Introdução aos atributos sombra</span><span class="sxs-lookup"><span data-stu-id="4d278-106">Introducing shadow attributes</span></span>
<span data-ttu-id="4d278-107">Alguns atributos têm duas representações no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d278-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="4d278-108">Valor de local de saudação e um valor calculado são armazenadas.</span><span class="sxs-lookup"><span data-stu-id="4d278-108">Both hello on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="4d278-109">Esses atributos adicionais são chamados de atributos sombra.</span><span class="sxs-lookup"><span data-stu-id="4d278-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="4d278-110">Olá dois atributos mais comuns em que você pode ver esse comportamento são **userPrincipalName** e **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="4d278-110">hello two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="4d278-111">Olá alterações em valores de atributos ocorre quando há valores nesses atributos que representam domínios não verificados.</span><span class="sxs-lookup"><span data-stu-id="4d278-111">hello change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="4d278-112">Mas o mecanismo de sincronização de saudação em conectar lê Olá valor no atributo de sombra Olá isso da sua perspectiva, o atributo de saudação foi confirmado pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d278-112">But hello sync engine in Connect reads hello value in hello shadow attribute so from its perspective, hello attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="4d278-113">Não é possível ver os atributos de sombra hello usando Olá portal do Azure ou com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d278-113">You cannot see hello shadow attributes using hello Azure portal or with PowerShell.</span></span> <span data-ttu-id="4d278-114">Mas o conceito de saudação Noções básicas sobre ajuda tootroubleshoot você determinados cenários onde o atributo de saudação tem valores diferentes no local e na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d278-114">But understanding hello concept helps you tootroubleshoot certain scenarios where hello attribute has different values on-premises and in hello cloud.</span></span>

<span data-ttu-id="4d278-115">toobetter compreender o comportamento de hello, veja este exemplo da Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="4d278-115">toobetter understand hello behavior, look at this example from Fabrikam:</span></span>  
![Domínios](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="4d278-117">Eles têm vários sufixos UPN no Active Directory local, mas verificaram apenas um.</span><span class="sxs-lookup"><span data-stu-id="4d278-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="4d278-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="4d278-118">userPrincipalName</span></span>
<span data-ttu-id="4d278-119">Um usuário tem Olá valores de atributo em um domínio não verificado a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d278-119">A user has hello following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="4d278-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="4d278-120">Attribute</span></span> | <span data-ttu-id="4d278-121">Valor</span><span class="sxs-lookup"><span data-stu-id="4d278-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d278-122">userPrincipalName local</span><span class="sxs-lookup"><span data-stu-id="4d278-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="4d278-123">shadowUserPrincipalName do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d278-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="4d278-124">userPrincipalName do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d278-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="4d278-125">atributo de userPrincipalName Olá é o valor de saudação que consulte ao usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d278-125">hello userPrincipalName attribute is hello value you see when using PowerShell.</span></span>

<span data-ttu-id="4d278-126">Como valor do atributo Olá local real é armazenado no AD do Azure, quando você verificar o domínio fabrikam.com de Olá, AD do Azure atualiza o atributo userPrincipalName de saudação com valor de saudação do hello shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="4d278-126">Since hello real on-premises attribute value is stored in Azure AD, when you verify hello fabrikam.com domain, Azure AD updates hello userPrincipalName attribute with hello value from hello shadowUserPrincipalName.</span></span> <span data-ttu-id="4d278-127">Você não tem toosynchronize as alterações do Azure AD Connect para esses toobe valores atualizados.</span><span class="sxs-lookup"><span data-stu-id="4d278-127">You do not have toosynchronize any changes from Azure AD Connect for these values toobe updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="4d278-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="4d278-128">proxyAddresses</span></span>
<span data-ttu-id="4d278-129">Olá mesmo processo para incluir somente os domínios verificados também ocorre proxyAddresses, mas com lógica adicional.</span><span class="sxs-lookup"><span data-stu-id="4d278-129">hello same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="4d278-130">seleção de saudação para domínios verificados ocorre apenas para usuários de caixa de correio.</span><span class="sxs-lookup"><span data-stu-id="4d278-130">hello check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="4d278-131">Um usuário habilitado para email ou contato representar um usuário em outra organização do Exchange e você pode adicionar todos os valores em objetos de toothese proxyAddresses.</span><span class="sxs-lookup"><span data-stu-id="4d278-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses toothese objects.</span></span>

<span data-ttu-id="4d278-132">Para um usuário de caixa de correio, no local ou no Exchange Online, somente os valores de domínios verificados são exibidos.</span><span class="sxs-lookup"><span data-stu-id="4d278-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="4d278-133">O resultado pode ser este:</span><span class="sxs-lookup"><span data-stu-id="4d278-133">It could look like this:</span></span>

| <span data-ttu-id="4d278-134">Atributo</span><span class="sxs-lookup"><span data-stu-id="4d278-134">Attribute</span></span> | <span data-ttu-id="4d278-135">Valor</span><span class="sxs-lookup"><span data-stu-id="4d278-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d278-136">proxyAddresses local</span><span class="sxs-lookup"><span data-stu-id="4d278-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="4d278-137">proxyAddresses do Exchange Online</span><span class="sxs-lookup"><span data-stu-id="4d278-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="4d278-138">Nesse caso, **smtp:abbie.spencer@fabrikam.com** foi removido, pois esse domínio não foi verificado.</span><span class="sxs-lookup"><span data-stu-id="4d278-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="4d278-139">Mas o Exchange também adicionou **SIP:abbie.spencer@fabrikamonline.com**. A Fabrikam não usou o Lync/Skype local, mas o Azure AD e o Exchange Online se preparam para isso.</span><span class="sxs-lookup"><span data-stu-id="4d278-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="4d278-140">Essa lógica para proxyAddresses é chamado tooas **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="4d278-140">This logic for proxyAddresses is referred tooas **ProxyCalc**.</span></span> <span data-ttu-id="4d278-141">ProxyCalc é invocado a cada alteração em um usuário, quando:</span><span class="sxs-lookup"><span data-stu-id="4d278-141">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="4d278-142">usuário Olá recebeu um plano de serviço que inclui o Exchange Online, mesmo se o usuário Olá não licenciado para o Exchange.</span><span class="sxs-lookup"><span data-stu-id="4d278-142">hello user has been assigned a service plan that includes Exchange Online even if hello user was not licensed for Exchange.</span></span> <span data-ttu-id="4d278-143">Por exemplo, se o usuário Olá é atribuído Olá Office E3 SKU, mas só foi atribuído o SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4d278-143">For example, if hello user is assigned hello Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="4d278-144">Isso será verdadeiro mesmo se sua caixa de correio ainda for local.</span><span class="sxs-lookup"><span data-stu-id="4d278-144">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="4d278-145">Olá msExchRecipientTypeDetails de atributo tem um valor.</span><span class="sxs-lookup"><span data-stu-id="4d278-145">hello attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="4d278-146">Você faz uma alteração tooproxyAddresses ou o userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="4d278-146">You make a change tooproxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="4d278-147">ProxyCalc pode levar algum tempo tooprocess uma alteração em um usuário e não é síncrono com o processo de exportação hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4d278-147">ProxyCalc might take some time tooprocess a change on a user and is not synchronous with hello Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="4d278-148">Olá ProxyCalc lógica tem alguns comportamentos adicionais para cenários avançados não são documentados neste tópico.</span><span class="sxs-lookup"><span data-stu-id="4d278-148">hello ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="4d278-149">Este tópico é fornecido para você toounderstand Olá comportamento e não toda a lógica interna de documento.</span><span class="sxs-lookup"><span data-stu-id="4d278-149">This topic is provided for you toounderstand hello behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="4d278-150">Valores de atributo em quarentena</span><span class="sxs-lookup"><span data-stu-id="4d278-150">Quarantined attribute values</span></span>
<span data-ttu-id="4d278-151">Os atributos sombra também são usados quando há valores de atributo duplicados.</span><span class="sxs-lookup"><span data-stu-id="4d278-151">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="4d278-152">Para saber mais, veja [resiliência de atributo duplicada](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="4d278-152">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4d278-153">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4d278-153">See also</span></span>
* [<span data-ttu-id="4d278-154">Sincronização do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4d278-154">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="4d278-155">[Integração de suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="4d278-155">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
