---
title: "Conecte-se vários domínios aaaAzure AD"
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
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="20b42-103">Suporte a Vários Domínios para Federação com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="20b42-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="20b42-104">Olá documentação a seguir fornece orientação sobre como toouse vários domínios de nível superior e subdomínios quando federar com domínios do Office 365 ou Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20b42-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="20b42-105">Suporte para vários domínios de nível superior</span><span class="sxs-lookup"><span data-stu-id="20b42-105">Multiple top-level domain support</span></span>
<span data-ttu-id="20b42-106">A federação de vários domínios de nível superior com o Azure AD requer configuração adicional que não é necessária na federação de um único domínio de nível superior.</span><span class="sxs-lookup"><span data-stu-id="20b42-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="20b42-107">Quando um domínio é federado com o Azure AD, várias propriedades são definidas no domínio Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="20b42-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="20b42-108">Uma delas é IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="20b42-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="20b42-109">Esse é um URI que é usado pelo AD do Azure tooidentify domínio Olá Olá token está associado.</span><span class="sxs-lookup"><span data-stu-id="20b42-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="20b42-110">Olá URI não precisa tooresolve tooanything, mas ele deve ser um URI válido.</span><span class="sxs-lookup"><span data-stu-id="20b42-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="20b42-111">Por padrão, o AD do Azure define esse toohello valor do identificador do serviço de Federação Olá em seu local do AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="20b42-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="20b42-112">Identificador do serviço de Federação Olá é um URI que identifica exclusivamente um serviço de Federação.</span><span class="sxs-lookup"><span data-stu-id="20b42-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="20b42-113">serviço de Federação Olá é uma instância do AD FS que funciona como um serviço de token de segurança de saudação.</span><span class="sxs-lookup"><span data-stu-id="20b42-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="20b42-114">Você pode IssuerUri de exibição usando o comando do PowerShell Olá `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="20b42-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="20b42-116">Um problema surge quando queremos tooadd mais de um domínio de nível superior.</span><span class="sxs-lookup"><span data-stu-id="20b42-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="20b42-117">Por exemplo, digamos que você tenha configurado a federação entre o Azure AD e seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="20b42-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="20b42-118">Para este documento, estou usando bmcontoso.com.  Agora adicionei um segundo domínio de nível superior, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="20b42-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domínios](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="20b42-120">Quando tentar tooconvert nosso toobe de domínio bmfabrikam.com federado, recebemos um erro.</span><span class="sxs-lookup"><span data-stu-id="20b42-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="20b42-121">Olá motivo isso é que o AD do Azure tem uma restrição que não permite Olá Olá de toohave propriedade IssuerUri mesmo valor para mais de um domínio.</span><span class="sxs-lookup"><span data-stu-id="20b42-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Erro de federação](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="20b42-123">Parâmetro SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="20b42-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="20b42-124">tooworkaround isso, precisamos tooadd um IssuerUri diferente, que pode ser feito usando Olá `-SupportMultipleDomain` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="20b42-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="20b42-125">Esse parâmetro é usado com hello cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="20b42-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="20b42-126">Esse parâmetro faz o AD do Azure configurar Olá IssuerUri para que ele se baseia no nome de saudação do domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="20b42-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="20b42-127">Ele será exclusivo nos diretórios no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20b42-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="20b42-128">Usar o parâmetro hello permite toocomplete de comando do PowerShell Olá com êxito.</span><span class="sxs-lookup"><span data-stu-id="20b42-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Erro de federação](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="20b42-130">Examinar as configurações de saudação do nosso novo domínio bmfabrikam.com você pode ver o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="20b42-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Erro de federação](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="20b42-132">Observe que `-SupportMultipleDomain` não altera Olá outros pontos de extremidade que são ainda configurado o serviço de Federação tooour toopoint em adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="20b42-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="20b42-133">Outra coisa que `-SupportMultipleDomain` does é que ele verifica se o sistema do hello AD FS inclui valor de emissor correto Olá em tokens emitidos para o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="20b42-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="20b42-134">Isso é feito por fazer parte do domínio de saudação do usuários Olá UPN e configurá-lo como domínio Olá Olá IssuerUri, ou seja, o sufixo https://{upn} / adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="20b42-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="20b42-135">Assim, durante a autenticação tooAzure AD ou o Office 365, Olá IssuerUri elemento token saudação do usuário é domínio de saudação toolocate usado no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="20b42-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="20b42-136">Se uma correspondência não for encontrada Olá autenticação falhará.</span><span class="sxs-lookup"><span data-stu-id="20b42-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="20b42-137">Por exemplo, se um usuário do UPN é bsimon@bmcontoso.com, elemento IssuerUri Olá problemas no AD FS token Olá definirá toohttp://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="20b42-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="20b42-138">Isso corresponderá a configuração do AD do Azure hello e autenticação será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="20b42-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="20b42-139">seguinte Olá é a regra de declaração personalizada de saudação que implementa essa lógica:</span><span class="sxs-lookup"><span data-stu-id="20b42-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="20b42-140">Em ordem toouse Olá - SupportMultipleDomain alternar durante a tentativa de tooadd nova ou converter já adicionado domínios, você precisa toohave configurar sua confiança federada toosupport-los originalmente.</span><span class="sxs-lookup"><span data-stu-id="20b42-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="20b42-141">Como tooupdate Olá confiança entre AD FS e Azure AD</span><span class="sxs-lookup"><span data-stu-id="20b42-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="20b42-142">Se você sem configurar Olá federada de confiança entre AD FS e a instância do AD do Azure, talvez seja necessário toore-criar essa relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="20b42-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="20b42-143">Isso ocorre porque, quando ele é originalmente instalação sem Olá `-SupportMultipleDomain` parâmetro, Olá IssuerUri é definido com o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="20b42-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="20b42-144">Olá captura de tela abaixo, você verá Olá IssuerUri é definido toohttps://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="20b42-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="20b42-145">Agora, se adicionou com êxito um novo domínio no portal de saudação do AD do Azure e, em seguida, tente tooconvert usando `Convert-MsolDomaintoFederated -DomainName <your domain>`, obtemos Olá erro a seguir.</span><span class="sxs-lookup"><span data-stu-id="20b42-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Erro de federação](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="20b42-147">Se você tentar tooadd Olá `-SupportMultipleDomain` switch receberemos Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="20b42-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Erro de federação](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="20b42-149">Simplesmente tentar toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` em Olá domínio original também resultará em erro.</span><span class="sxs-lookup"><span data-stu-id="20b42-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Erro de federação](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="20b42-151">Use as etapas de saudação abaixo tooadd um domínio de nível superior adicional.</span><span class="sxs-lookup"><span data-stu-id="20b42-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="20b42-152">Se você já tiver adicionado um domínio e não tiver usado a saudação `-SupportMultipleDomain` início do parâmetro com etapas Olá para remover e atualizar o domínio original.</span><span class="sxs-lookup"><span data-stu-id="20b42-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="20b42-153">Se você não adicionou um domínio de nível superior ainda você pode iniciar com etapas de saudação para adicionar um domínio usando o PowerShell do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="20b42-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="20b42-154">Use Olá seguindo as etapas tooremove Olá Online da Microsoft confiança e atualizar o domínio original.</span><span class="sxs-lookup"><span data-stu-id="20b42-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="20b42-155">No servidor de Federação do AD FS, abra **Gerenciamento do AD FS.**</span><span class="sxs-lookup"><span data-stu-id="20b42-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="20b42-156">Olá esquerda, expanda **relações de confiança** e **terceira parte confiável**</span><span class="sxs-lookup"><span data-stu-id="20b42-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="20b42-157">Em Olá à direita, exclua Olá **plataforma de identidade do Microsoft Office 365** entrada.</span><span class="sxs-lookup"><span data-stu-id="20b42-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="20b42-158">![Remover o Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="20b42-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="20b42-159">Em um computador que tenha [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado execute seguinte Olá: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="20b42-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="20b42-160">Insira a saudação de nome de usuário e senha de um administrador global para o domínio do AD do Azure Olá com que você está associando</span><span class="sxs-lookup"><span data-stu-id="20b42-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="20b42-161">No PowerShell, digite `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="20b42-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="20b42-162">No PowerShell, digite `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="20b42-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="20b42-163">Isso é para o domínio original hello.</span><span class="sxs-lookup"><span data-stu-id="20b42-163">This is for hello original domain.</span></span>  <span data-ttu-id="20b42-164">Portanto, usar Olá acima domínios seria:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="20b42-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="20b42-165">Use Olá seguindo as etapas tooadd Olá novo domínio de nível superior usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="20b42-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="20b42-166">Em um computador que tenha [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado execute seguinte Olá: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="20b42-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="20b42-167">Insira a saudação de nome de usuário e senha de um administrador global para o domínio do AD do Azure Olá com que você está associando</span><span class="sxs-lookup"><span data-stu-id="20b42-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="20b42-168">No PowerShell, digite `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="20b42-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="20b42-169">No PowerShell, digite `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="20b42-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="20b42-170">Use Olá seguindo as etapas tooadd Olá novo domínio de nível superior usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="20b42-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="20b42-171">Inicie o Azure AD Connect da área de trabalho de saudação ou menu Iniciar</span><span class="sxs-lookup"><span data-stu-id="20b42-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="20b42-172">Escolha "Adicionar um domínio do Azure AD" ![Adicionar um domínio do Azure AD](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="20b42-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="20b42-173">Insira as credenciais do Azure AD e do Active Directory</span><span class="sxs-lookup"><span data-stu-id="20b42-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="20b42-174">Selecione o domínio de segundo Olá desejar tooconfigure para federação.</span><span class="sxs-lookup"><span data-stu-id="20b42-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="20b42-175">![Adicionar um domínio do Azure AD](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="20b42-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="20b42-176">Clique em Instalar</span><span class="sxs-lookup"><span data-stu-id="20b42-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="20b42-177">Verifique se o novo domínio de nível superior Olá</span><span class="sxs-lookup"><span data-stu-id="20b42-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="20b42-178">Usando o comando do PowerShell Olá `Get-MsolDomainFederationSettings -DomainName <your domain>`você pode exibir hello atualizado IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="20b42-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="20b42-179">saudação de captura de tela abaixo mostra as configurações de Federação Olá foram atualizadas no nosso http://bmcontoso.com/adfs/services/trust domínio original</span><span class="sxs-lookup"><span data-stu-id="20b42-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="20b42-181">E Olá IssuerUri em nosso novo domínio tiver sido definido toohttps://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="20b42-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="20b42-183">Suporte para Subdomínios</span><span class="sxs-lookup"><span data-stu-id="20b42-183">Support for Sub-domains</span></span>
<span data-ttu-id="20b42-184">Quando você adiciona um subdomínio, devido a saudação do AD do Azure forma manipuladas domínios, ele herdará as configurações de saudação do pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="20b42-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="20b42-185">Isso significa que Olá IssuerUri precisa toomatch pais de saudação.</span><span class="sxs-lookup"><span data-stu-id="20b42-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="20b42-186">Digamos, por exemplo, que tenho bmcontoso.com e adiciono corp.bmcontoso.com.  Isso significa que Olá IssuerUri para um usuário de corp.bmcontoso.com, será preciso toobe **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="20b42-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="20b42-187">No entanto, regra padrão Olá implementado acima do AD do Azure, irá gerar um token com um emissor como **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="20b42-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="20b42-188">que não irão corresponder o valor necessário do domínio hello e a autenticação falhará.</span><span class="sxs-lookup"><span data-stu-id="20b42-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="20b42-189">Como o suporte a tooenable de subdomínios</span><span class="sxs-lookup"><span data-stu-id="20b42-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="20b42-190">Em ordem toowork em todo este Olá terceira parte confiável para o Microsoft Online do AD FS precisa toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="20b42-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="20b42-191">toodo isso, você deve configurar uma regra de declaração personalizada para que ele ignora quaisquer subdomínios de sufixo UPN do usuário Olá ao construir o valor de emissor personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="20b42-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="20b42-192">Olá declaração a seguir faz isso:</span><span class="sxs-lookup"><span data-stu-id="20b42-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="20b42-193">último número de saudação em expressão regular Olá definir Olá quantos domínios pai no seu domínio raiz.</span><span class="sxs-lookup"><span data-stu-id="20b42-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="20b42-194">Aqui temos bmcontoso.com, então são necessários dois domínios pai.</span><span class="sxs-lookup"><span data-stu-id="20b42-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="20b42-195">Se três pai domínios foram toobe mantido (ou seja: corp.bmcontoso.com), em seguida, o número de saudação teria sido três.</span><span class="sxs-lookup"><span data-stu-id="20b42-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="20b42-196">Eventualy um intervalo pode ser indicado, correspondência de saudação sempre será feita no máximo toomatch Olá domínios.</span><span class="sxs-lookup"><span data-stu-id="20b42-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="20b42-197">"{2,3}" corresponderá a dois domínios toothree (ou seja: bmfabrikam.com e corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="20b42-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="20b42-198">As etapas a seguir do uso Olá tooadd um subdomínios de toosupport declaração personalizada.</span><span class="sxs-lookup"><span data-stu-id="20b42-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="20b42-199">Abra o gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="20b42-199">Open AD FS Management</span></span>
2. <span data-ttu-id="20b42-200">Clique com botão direito Olá RP Online da Microsoft de confiança e escolha as regras de declaração editar</span><span class="sxs-lookup"><span data-stu-id="20b42-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="20b42-201">Selecione a terceira regra de declaração hello e substitua ![declaração de edição](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="20b42-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="20b42-202">Substitua a declaração atual hello:</span><span class="sxs-lookup"><span data-stu-id="20b42-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Substituir declaração](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="20b42-204">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="20b42-204">Click Ok.</span></span>  <span data-ttu-id="20b42-205">Clique em Aplicar.</span><span class="sxs-lookup"><span data-stu-id="20b42-205">Click Apply.</span></span>  <span data-ttu-id="20b42-206">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="20b42-206">Click Ok.</span></span>  <span data-ttu-id="20b42-207">Feche o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="20b42-207">Close AD FS Management.</span></span>

