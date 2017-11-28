---
title: Perguntas frequentes sobre o Azure Active Directory | Microsoft Docs
description: "Esta página tem perguntas frequentes sobre o Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="94a13-103">Perguntas frequentes sobre o Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="94a13-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="94a13-104">Instalação geral</span><span class="sxs-lookup"><span data-stu-id="94a13-104">General installation</span></span>
<span data-ttu-id="94a13-105">**P: instalação funcionará se Olá Administrador Global do Azure AD tem 2FA habilitado?**</span><span class="sxs-lookup"><span data-stu-id="94a13-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="94a13-106">Com hello compilações de fevereiro de 2016, isso é suportado.</span><span class="sxs-lookup"><span data-stu-id="94a13-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="94a13-107">**P: há um tooinstall de forma autônoma o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="94a13-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="94a13-108">É apenas tooinstall com suporte do Azure AD Connect usando o Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="94a13-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="94a13-109">Não há suporte para uma instalação silenciosa e autônoma.</span><span class="sxs-lookup"><span data-stu-id="94a13-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="94a13-110">**P: Eu tenho uma floresta em que um domínio não pode ser contatado. Como instalo o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="94a13-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="94a13-111">Com hello compilações de fevereiro de 2016, isso é suportado.</span><span class="sxs-lookup"><span data-stu-id="94a13-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="94a13-112">**P: Olá trabalho de agente de integridade do AD DS no server core?**</span><span class="sxs-lookup"><span data-stu-id="94a13-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="94a13-113">Sim.</span><span class="sxs-lookup"><span data-stu-id="94a13-113">Yes.</span></span> <span data-ttu-id="94a13-114">Depois de instalar o agente de hello, você poderá concluir o processo de registro de hello usando Olá cmdlet do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="94a13-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="94a13-115">Rede</span><span class="sxs-lookup"><span data-stu-id="94a13-115">Network</span></span>
<span data-ttu-id="94a13-116">**P: tenho um firewall, o dispositivo de rede, ou algo que limita as conexões de tempo máximo de saudação pode permanecer aberto na rede. Qual deve ser o limiar de tempo limite no lado do cliente ao usar o Azure Connect AD?**</span><span class="sxs-lookup"><span data-stu-id="94a13-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="94a13-117">Todos os softwares de rede, dispositivos físicos ou qualquer outra coisa que o tempo máximo de saudação conexões podem permanecer abertos deve usar um limite de pelo menos 5 minutos (300 segundos) para conectividade entre os limites Olá servidor onde hello Azure AD Connect cliente está instalado e o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="94a13-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="94a13-118">Isso também se aplica a ferramentas de sincronização do Microsoft Identity tooall lançada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="94a13-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="94a13-119">**P: Os SLDs (domínios de rótulo único) têm suporte?**</span><span class="sxs-lookup"><span data-stu-id="94a13-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="94a13-120">Não, o Azure AD Connect não oferece suporte a florestas/domínios locais usando SLDs.</span><span class="sxs-lookup"><span data-stu-id="94a13-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="94a13-121">**P: Há suporte a nomes NetBios com pontos?**</span><span class="sxs-lookup"><span data-stu-id="94a13-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="94a13-122">Não, o AD do Azure Connect não oferece suporte a florestas/domínios do local onde o nome de NetBios Olá contém um ponto "." no nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="94a13-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="94a13-123">Federação</span><span class="sxs-lookup"><span data-stu-id="94a13-123">Federation</span></span>
<span data-ttu-id="94a13-124">**P: o que fazer se receber um email que me pedindo toorenew meu certificado do Office 365**</span><span class="sxs-lookup"><span data-stu-id="94a13-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="94a13-125">Usar as orientações de saudação descrita no hello [renovar certificados](active-directory-aadconnect-o365-certs.md) tópico sobre como toorenew Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="94a13-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="94a13-126">**P: Defini a opção “Atualizar automaticamente terceira parte confiável” para a terceira parte confiável do O365. É necessário tootake qualquer ação quando meu automaticamente o certificado de assinatura de token faz?**</span><span class="sxs-lookup"><span data-stu-id="94a13-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="94a13-127">Usar as orientações de saudação descrita no artigo Olá [renovar certificados](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="94a13-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="94a13-128">Ambiente</span><span class="sxs-lookup"><span data-stu-id="94a13-128">Environment</span></span>
<span data-ttu-id="94a13-129">**P: há suporte para toorename Olá servidor após a instalação do Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="94a13-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="94a13-130">Não.</span><span class="sxs-lookup"><span data-stu-id="94a13-130">No.</span></span> <span data-ttu-id="94a13-131">Alterando o nome do servidor de saudação causa toonot de mecanismo de sincronização de saudação será capaz de tooconnect toohello SQL banco de dados e serviço de saudação não será capaz de toostart.</span><span class="sxs-lookup"><span data-stu-id="94a13-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="94a13-132">Dados de identidade</span><span class="sxs-lookup"><span data-stu-id="94a13-132">Identity data</span></span>
<span data-ttu-id="94a13-133">**P: Olá o atributo UPN (userPrincipalName) no AD do Azure não corresponder Olá UPN local - por que?**</span><span class="sxs-lookup"><span data-stu-id="94a13-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="94a13-134">Consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="94a13-134">See these articles:</span></span>

* [<span data-ttu-id="94a13-135">Olá de nomes de usuário no Office 365, Azure ou Intune não correspondem ao UPN local ou ID de logon alternativo</span><span class="sxs-lookup"><span data-stu-id="94a13-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="94a13-136">As alterações não são sincronizadas pela ferramenta de sincronização do Active Directory do Azure de Olá depois de alterar Olá UPN de uma conta de usuário toouse um domínio federado diferente</span><span class="sxs-lookup"><span data-stu-id="94a13-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="94a13-137">Você também pode configurar o AD do Azure tooallow Olá sincronização mecanismo tooupdate Olá userPrincipalName conforme descrito em [recursos de serviço de sincronização do Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="94a13-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="94a13-138">**P: há suporte para toosoft correspondência local objetos AD/contato de um grupo com objetos de contato/grupo do AD do Azure existente?**</span><span class="sxs-lookup"><span data-stu-id="94a13-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="94a13-139">Não, não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="94a13-139">No, this is currently not supported.</span></span>

<span data-ttu-id="94a13-140">**P: há suporte para toomanually define atributo de ImmutableId no Azure AD grupo/contato existente objetos toohard correspondência local tooon objetos de grupo do AD/contato?**</span><span class="sxs-lookup"><span data-stu-id="94a13-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="94a13-141">Não, não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="94a13-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="94a13-142">Configuração personalizada</span><span class="sxs-lookup"><span data-stu-id="94a13-142">Custom configuration</span></span>
<span data-ttu-id="94a13-143">**P: onde estão Olá cmdlets do PowerShell para Azure AD Connect documentado?**</span><span class="sxs-lookup"><span data-stu-id="94a13-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="94a13-144">Com exceção de Olá Olá cmdlets documentados neste site, não há suporte para outros cmdlets do PowerShell encontrados na conexão do AD do Azure para uso do cliente.</span><span class="sxs-lookup"><span data-stu-id="94a13-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="94a13-145">**P: posso usar "Servidor de exportação/importação do servidor" encontrada em *Synchronization Service Manager* toomove configuração entre servidores?**</span><span class="sxs-lookup"><span data-stu-id="94a13-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="94a13-146">Não.</span><span class="sxs-lookup"><span data-stu-id="94a13-146">No.</span></span> <span data-ttu-id="94a13-147">Essa opção não irá recuperar todos os parâmetros de configuração e não deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="94a13-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="94a13-148">Em vez disso, você deve usar a configuração básica do Olá Olá Assistente toocreate no segundo servidor de saudação e usar regra de sincronização Olá editor toogenerate PowerShell scripts toomove qualquer regra personalizada entre servidores.</span><span class="sxs-lookup"><span data-stu-id="94a13-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="94a13-149">Confira [Migração Swing](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="94a13-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="94a13-150">**P: senhas armazenadas de página Olá entrada do Azure e pode isso impedida, pois ele contém um elemento de entrada de senha com preenchimento automático de hello = "false" atributo?**</span><span class="sxs-lookup"><span data-stu-id="94a13-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="94a13-151">No momento não oferecemos suporte modificados atributos HTML Olá Olá senha do campo de entrada, incluindo a marca de preenchimento automático de saudação.</span><span class="sxs-lookup"><span data-stu-id="94a13-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="94a13-152">Atualmente estamos trabalhando em um recurso que permite o uso de Javascript personalizado que permitirá que você tooadd qualquer campo de senha do atributo toohello.</span><span class="sxs-lookup"><span data-stu-id="94a13-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="94a13-153">Isso deve ser disponibilizado no último semestre de 2017.</span><span class="sxs-lookup"><span data-stu-id="94a13-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="94a13-154">**P: no hello Azure na página de entrada, nomes de usuário para usuários que se conectaram anteriormente com êxito são mostradas.  Esse comportamento pode ser desativado?**</span><span class="sxs-lookup"><span data-stu-id="94a13-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="94a13-155">No momento não oferecemos suporte modificados atributos HTML de saudação da página de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="94a13-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="94a13-156">Atualmente estamos trabalhando em um recurso que permite o uso de Javascript personalizado que permitirá que você tooadd qualquer campo de senha do atributo toohello.</span><span class="sxs-lookup"><span data-stu-id="94a13-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="94a13-157">Isso deve ser disponibilizado no último semestre de 2017.</span><span class="sxs-lookup"><span data-stu-id="94a13-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="94a13-158">**P: há uma maneira tooprevent sessões simultâneas?**</span><span class="sxs-lookup"><span data-stu-id="94a13-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="94a13-159">Não.</span><span class="sxs-lookup"><span data-stu-id="94a13-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="94a13-160">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="94a13-160">Troubleshooting</span></span>
<span data-ttu-id="94a13-161">**P: Como posso obter ajuda com o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="94a13-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="94a13-162">Saudação de pesquisa da Base de dados de Conhecimento Microsoft (KB)</span><span class="sxs-lookup"><span data-stu-id="94a13-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="94a13-163">Saudação de pesquisa da Base de dados de Conhecimento Microsoft (KB) para problemas de conserto toocommon soluções técnicas sobre o suporte para conexão do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="94a13-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="94a13-164">Fóruns do Active Directory do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="94a13-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="94a13-165">Você pode pesquisar e navegar para técnico de perguntas e respostas de comunidade hello ou faça sua pergunta, clicando em [aqui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="94a13-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="94a13-166">Atendimento ao cliente do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="94a13-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="94a13-167">Use esse suporte de tooget link por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94a13-167">Use this link tooget support through hello Azure portal.</span></span>

