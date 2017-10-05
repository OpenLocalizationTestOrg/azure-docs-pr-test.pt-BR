---
title: "Vários domínios do Azure AD Connect"
description: "Este documento descreve a instalação e a configuração de vários domínios de nível superior com o O365 e o Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="ad201-103">Suporte a Vários Domínios para Federação com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad201-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="ad201-104">A documentação a seguir fornece orientação sobre como usar vários domínios e subdomínios  de nível superior ao estabelecer uma federação com o Office 365 ou com domínios do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad201-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="ad201-105">Suporte para vários domínios de nível superior</span><span class="sxs-lookup"><span data-stu-id="ad201-105">Multiple top-level domain support</span></span>
<span data-ttu-id="ad201-106">A federação de vários domínios de nível superior com o Azure AD requer configuração adicional que não é necessária na federação de um único domínio de nível superior.</span><span class="sxs-lookup"><span data-stu-id="ad201-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="ad201-107">Quando um domínio é federado com o Azure AD, várias propriedades são definidas no domínio no Azure.</span><span class="sxs-lookup"><span data-stu-id="ad201-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="ad201-108">Uma delas é IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="ad201-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="ad201-109">Isso é um URI usado pelo Azure AD para identificar o domínio ao qual o token está associado.</span><span class="sxs-lookup"><span data-stu-id="ad201-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="ad201-110">O URI não precisa resolver para nada, mas deve ser um URI válido.</span><span class="sxs-lookup"><span data-stu-id="ad201-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="ad201-111">Por padrão, o Azure AD define isso como o valor do identificador do serviço de federação em sua configuração local do AD FS.</span><span class="sxs-lookup"><span data-stu-id="ad201-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="ad201-112">O identificador do serviço de federação é um URI que identifica exclusivamente um serviço de federação.</span><span class="sxs-lookup"><span data-stu-id="ad201-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="ad201-113">O serviço de federação é uma instância do AD FS que funciona como o serviço de token de segurança.</span><span class="sxs-lookup"><span data-stu-id="ad201-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="ad201-114">Você pode exibir o IssuerUri usando o comando `Get-MsolDomainFederationSettings -DomainName <your domain>`do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad201-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="ad201-116">Um problema surge quando queremos adicionar mais de um domínio de nível superior.</span><span class="sxs-lookup"><span data-stu-id="ad201-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="ad201-117">Por exemplo, digamos que você tenha configurado a federação entre o Azure AD e seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="ad201-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="ad201-118">Para este documento, estou usando bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="ad201-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="ad201-119">Agora adicionei um segundo domínio de nível superior, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="ad201-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domínios](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="ad201-121">Quando tentamos converter nosso domínio bmfabrikam.com em federado, recebemos um erro.</span><span class="sxs-lookup"><span data-stu-id="ad201-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="ad201-122">A razão para isso é que o Azure AD tem uma restrição que não permite que a propriedade IssuerUri tenha o mesmo valor para mais de um domínio.</span><span class="sxs-lookup"><span data-stu-id="ad201-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![Erro de federação](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="ad201-124">Parâmetro SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="ad201-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="ad201-125">Para solucionar isso, precisamos adicionar um IssuerUri diferente. Isso pode ser feito usando o parâmetro `-SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="ad201-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="ad201-126">Esse parâmetro é usado com os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="ad201-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="ad201-127">Esse parâmetro faz o Azure AD configurar o IssuerUri para se basear no nome do domínio.</span><span class="sxs-lookup"><span data-stu-id="ad201-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="ad201-128">Ele será exclusivo nos diretórios no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad201-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="ad201-129">O uso do parâmetro permite que o comando do PowerShell seja concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="ad201-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![Erro de federação](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="ad201-131">Observando as configurações do novo domínio bmfabrikam.com, você pode ver o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ad201-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![Erro de federação](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="ad201-133">Observe que `-SupportMultipleDomain` não altera os outros pontos de extremidade que ainda estão configurados para apontar para o serviço de federação em adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="ad201-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="ad201-134">O `-SupportMultipleDomain` também garante que o sistema de AD FS inclua o valor de emissor adequado em tokens emitidos para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad201-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="ad201-135">Ele faz isso usando a parte do domínio do UPN dos usuários e configurando isso como o domínio no IssuerUri, ou seja, https://{upn suffix}/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="ad201-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="ad201-136">Dessa forma, durante a autenticação no Azure AD ou Office 365, o elemento IssuerURI no token do usuário é usado para localizar o domínio no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad201-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="ad201-137">Se não houver correspondência, a autenticação falhará.</span><span class="sxs-lookup"><span data-stu-id="ad201-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="ad201-138">Por exemplo, se um usuário do UPN é bsimon@bmcontoso.com, o elemento IssuerUri os problemas do token AD FS será definido como http://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="ad201-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="ad201-139">Isso corresponderá à configuração do Azure AD, e a autenticação será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="ad201-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="ad201-140">Abaixo vemos a regra de declaração personalizada que implementa essa lógica:</span><span class="sxs-lookup"><span data-stu-id="ad201-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="ad201-141">Para usar a opção - SupportMultipleDomain quando tentar adicionar um novo domínio ou converter domínios já adicionados, você precisará ter sua confiança federada configurada para dar suporte a eles desde o início.</span><span class="sxs-lookup"><span data-stu-id="ad201-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="ad201-142">Como atualizar a relação de confiança entre o AD FS e o Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad201-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="ad201-143">Se você não tiver configurado a confiança federada entre o AD FS e a instância do Azure AD, será preciso recriá-la.</span><span class="sxs-lookup"><span data-stu-id="ad201-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="ad201-144">Isso ocorre porque, quando ela é originalmente configurada sem o parâmetro `-SupportMultipleDomain` , o IssuerUri é definido com o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="ad201-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="ad201-145">Na captura de tela abaixo, você pode ver que IssuerUri está definido como https://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="ad201-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="ad201-146">Agora, se adicionarmos um novo domínio no portal do Azure AD com êxito e tentarmos convertê-lo usando `Convert-MsolDomaintoFederated -DomainName <your domain>`, obteremos o seguinte erro.</span><span class="sxs-lookup"><span data-stu-id="ad201-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![Erro de federação](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="ad201-148">Se você tentar adicionar a opção `-SupportMultipleDomain` , receberá o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="ad201-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![Erro de federação](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="ad201-150">A simples tentativa de executar `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` no domínio original também resultará em erro.</span><span class="sxs-lookup"><span data-stu-id="ad201-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![Erro de federação](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="ad201-152">Use as etapas a seguir para adicionar mais um domínio de nível superior.</span><span class="sxs-lookup"><span data-stu-id="ad201-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="ad201-153">Se você já tiver adicionado um domínio e não usou o parâmetro `-SupportMultipleDomain` , utilize as etapas para remover e atualizar o domínio original.</span><span class="sxs-lookup"><span data-stu-id="ad201-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="ad201-154">Se você ainda não tiver adicionado um domínio de nível superior, poderá começar com as etapas para adicionar um domínio usando o PowerShell do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ad201-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="ad201-155">Use as etapas a seguir para remover a relação de confiança do Microsoft Online e atualizar seu domínio original.</span><span class="sxs-lookup"><span data-stu-id="ad201-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="ad201-156">No servidor de Federação do AD FS, abra **Gerenciamento do AD FS.**</span><span class="sxs-lookup"><span data-stu-id="ad201-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="ad201-157">À esquerda, expanda **Relações de Confiança** e **Terceira Parte Confiável**</span><span class="sxs-lookup"><span data-stu-id="ad201-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="ad201-158">À direita, exclua a entrada **Plataforma de Identidade do Microsoft Office 365** .</span><span class="sxs-lookup"><span data-stu-id="ad201-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="ad201-159">![Remover o Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="ad201-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="ad201-160">Em um computador que tenha o [Módulo do Azure Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado, execute o seguinte: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="ad201-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="ad201-161">Insira o nome de usuário e a senha de um administrador global para o domínio do Azure AD com o qual você está federando</span><span class="sxs-lookup"><span data-stu-id="ad201-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="ad201-162">No PowerShell, digite `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="ad201-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="ad201-163">No PowerShell, digite `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="ad201-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="ad201-164">Isso é para o domínio original.</span><span class="sxs-lookup"><span data-stu-id="ad201-164">This is for the original domain.</span></span>  <span data-ttu-id="ad201-165">Usando os domínios acima, seria: `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="ad201-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="ad201-166">Use as etapas a seguir para adicionar o novo domínio de nível superior usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad201-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="ad201-167">Em um computador que tenha o [Módulo do Azure Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado, execute o seguinte: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="ad201-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="ad201-168">Insira o nome de usuário e a senha de um administrador global para o domínio do Azure AD com o qual você está federando</span><span class="sxs-lookup"><span data-stu-id="ad201-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="ad201-169">No PowerShell, digite `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="ad201-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="ad201-170">No PowerShell, digite `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="ad201-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="ad201-171">Use as etapas a seguir para adicionar o novo domínio de nível superior usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ad201-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="ad201-172">Inicie o Azure AD Connect na área de trabalho ou no menu Iniciar</span><span class="sxs-lookup"><span data-stu-id="ad201-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="ad201-173">Escolha "Adicionar um domínio do Azure AD" ![Adicionar um domínio do Azure AD](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="ad201-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="ad201-174">Insira as credenciais do Azure AD e do Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad201-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="ad201-175">Escolha o segundo domínio que você deseja configurar para federação.</span><span class="sxs-lookup"><span data-stu-id="ad201-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="ad201-176">![Adicionar um domínio do Azure AD](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="ad201-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="ad201-177">Clique em Instalar</span><span class="sxs-lookup"><span data-stu-id="ad201-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="ad201-178">Verifique o novo domínio de nível superior</span><span class="sxs-lookup"><span data-stu-id="ad201-178">Verify the new top-level domain</span></span>
<span data-ttu-id="ad201-179">Usando o comando `Get-MsolDomainFederationSettings -DomainName <your domain>`do PowerShell, você pode exibir o IssuerUri atualizado.</span><span class="sxs-lookup"><span data-stu-id="ad201-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="ad201-180">A captura de tela abaixo mostra que as configurações de federação foram atualizadas no nosso domínio original http://bmcontoso.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="ad201-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="ad201-182">E IssuerUri em nosso novo domínio foi definido como https://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="ad201-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="ad201-184">Suporte para Subdomínios</span><span class="sxs-lookup"><span data-stu-id="ad201-184">Support for Sub-domains</span></span>
<span data-ttu-id="ad201-185">Quando você adiciona um subdomínio, devido à maneira usada pelo Azure AD para tratar domínios, ele herda as configurações do pai.</span><span class="sxs-lookup"><span data-stu-id="ad201-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="ad201-186">Isso significa que o IssuerUri precisa corresponder aos pais.</span><span class="sxs-lookup"><span data-stu-id="ad201-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="ad201-187">Digamos, por exemplo, que tenho bmcontoso.com e adiciono corp.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="ad201-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="ad201-188">Isso significa que o IssuerUri para um usuário do corp.bmcontoso.com precisará ser **http://bmcontoso.com/adfs/services/trust**.</span><span class="sxs-lookup"><span data-stu-id="ad201-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="ad201-189">No entanto, a regra padrão implementada acima para o Azure AD irá gerar um token com um emissor como **http://corp.bmcontoso.com/adfs/services/trust**.</span><span class="sxs-lookup"><span data-stu-id="ad201-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="ad201-190">, que não corresponderá ao domínio do valor obrigatório e fará com que a autenticação falhe.</span><span class="sxs-lookup"><span data-stu-id="ad201-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="ad201-191">Como habilitar o suporte para subdomínios</span><span class="sxs-lookup"><span data-stu-id="ad201-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="ad201-192">Para solucionar esse problema, a relação de confiança de terceira parte confiável do AD FS do Microsoft Online precisa ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="ad201-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="ad201-193">Para isso, você precisa configurar a regra de declaração personalizada para que ela ignore os subdomínios do sufixo UPN do usuário ao construir o valor de Issuer personalizado.</span><span class="sxs-lookup"><span data-stu-id="ad201-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="ad201-194">A declaração a seguir fará isso:</span><span class="sxs-lookup"><span data-stu-id="ad201-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="ad201-195">O último número na expressão regular define quantos domínios pai há no seu domínio raiz.</span><span class="sxs-lookup"><span data-stu-id="ad201-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="ad201-196">Aqui temos bmcontoso.com, então são necessários dois domínios pai.</span><span class="sxs-lookup"><span data-stu-id="ad201-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="ad201-197">Se você tiver três domínios pai (por exemplo: corp.bmcontoso.com), então o número seria três.</span><span class="sxs-lookup"><span data-stu-id="ad201-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="ad201-198">Eventualmente pode ser indicado um intervalo. A quantidade máxima sempre deve corresponder ao máximo de domínios.</span><span class="sxs-lookup"><span data-stu-id="ad201-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="ad201-199">"{2,3}" corresponderá a dois a três domínios (ou seja: bmfabrikam.com e corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="ad201-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="ad201-200">Use as etapas a seguir para adicionar uma declaração personalizada que dê suporte a subdomínios.</span><span class="sxs-lookup"><span data-stu-id="ad201-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="ad201-201">Abra o gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="ad201-201">Open AD FS Management</span></span>
2. <span data-ttu-id="ad201-202">Clique com botão direito do mouse na relação de confiança de terceira parte confiável do Microsoft Online e escolha Editar regras de declaração</span><span class="sxs-lookup"><span data-stu-id="ad201-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="ad201-203">Escolha a terceira regra de declaração e substitua ![Editar declaração](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="ad201-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="ad201-204">Substitua a declaração atual:</span><span class="sxs-lookup"><span data-stu-id="ad201-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Substituir declaração](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="ad201-206">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="ad201-206">Click Ok.</span></span>  <span data-ttu-id="ad201-207">Clique em Aplicar.</span><span class="sxs-lookup"><span data-stu-id="ad201-207">Click Apply.</span></span>  <span data-ttu-id="ad201-208">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="ad201-208">Click Ok.</span></span>  <span data-ttu-id="ad201-209">Feche o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="ad201-209">Close AD FS Management.</span></span>

