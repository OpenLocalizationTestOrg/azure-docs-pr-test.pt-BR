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
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="66770-103">Perguntas frequentes sobre o Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="66770-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="66770-104">Instalação geral</span><span class="sxs-lookup"><span data-stu-id="66770-104">General installation</span></span>
<span data-ttu-id="66770-105">**P: a instalação funcionará se o Administrador Global do AD do Azure tem 2FA habilitado?**</span><span class="sxs-lookup"><span data-stu-id="66770-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="66770-106">Há suporte para isso nas compilações de fevereiro de 2016.</span><span class="sxs-lookup"><span data-stu-id="66770-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="66770-107">**P: existe uma forma de instalar o Azure Connect AD autônomo?**</span><span class="sxs-lookup"><span data-stu-id="66770-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="66770-108">Somente há suporte para instalar o Azure Connect AD usando o assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="66770-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="66770-109">Não há suporte para uma instalação silenciosa e autônoma.</span><span class="sxs-lookup"><span data-stu-id="66770-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="66770-110">**P: Eu tenho uma floresta em que um domínio não pode ser contatado. Como instalo o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="66770-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="66770-111">Há suporte para isso nas compilações de fevereiro de 2016.</span><span class="sxs-lookup"><span data-stu-id="66770-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="66770-112">**P: O agente de integridade do AD DS funciona no núcleo do servidor?**</span><span class="sxs-lookup"><span data-stu-id="66770-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="66770-113">Sim.</span><span class="sxs-lookup"><span data-stu-id="66770-113">Yes.</span></span> <span data-ttu-id="66770-114">Depois de instalar o agente, você pode concluir o processo de registro usando o seguinte cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66770-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="66770-115">Rede</span><span class="sxs-lookup"><span data-stu-id="66770-115">Network</span></span>
<span data-ttu-id="66770-116">**P: Tenho um firewall, dispositivo de rede ou outra coisa que limita o tempo máximo que as conexões podem permanecer abertas na minha rede. Qual deve ser o limiar de tempo limite no lado do cliente ao usar o Azure Connect AD?**</span><span class="sxs-lookup"><span data-stu-id="66770-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="66770-117">Todos os softwares de rede, dispositivos físicos ou qualquer outra coisa que limite o tempo máximo que as conexões podem permanecer abertas deve usar um limiar de pelo menos 5 minutos (300 segundos) para conectividade entre o servidor no qual o cliente do Azure AD Connect está instalado e o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="66770-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="66770-118">Isso também se aplica a todas as ferramentas de sincronização do Microsoft Identity lançadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66770-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="66770-119">**P: Os SLDs (domínios de rótulo único) têm suporte?**</span><span class="sxs-lookup"><span data-stu-id="66770-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="66770-120">Não, o Azure AD Connect não oferece suporte a florestas/domínios locais usando SLDs.</span><span class="sxs-lookup"><span data-stu-id="66770-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="66770-121">**P: Há suporte a nomes NetBios com pontos?**</span><span class="sxs-lookup"><span data-stu-id="66770-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="66770-122">Não, o Azure AD Connect não oferece suporte a florestas/domínios locais em que o nome NetBios contém um ponto "." no nome.</span><span class="sxs-lookup"><span data-stu-id="66770-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="66770-123">Federação</span><span class="sxs-lookup"><span data-stu-id="66770-123">Federation</span></span>
<span data-ttu-id="66770-124">**P: O que devo fazer se receber um email me pedindo para renovar o certificado do Office 365?**</span><span class="sxs-lookup"><span data-stu-id="66770-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="66770-125">Use as diretrizes descritas no tópico [Renovar certificados](active-directory-aadconnect-o365-certs.md) para saber como renovar o certificado.</span><span class="sxs-lookup"><span data-stu-id="66770-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="66770-126">**P: Defini a opção “Atualizar automaticamente terceira parte confiável” para a terceira parte confiável do O365. Preciso realizar alguma ação quando meu certificado de autenticação de tokens é substituído automaticamente?**</span><span class="sxs-lookup"><span data-stu-id="66770-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="66770-127">Use as diretrizes descritas no artigo [Renovar certificados](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="66770-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="66770-128">Ambiente</span><span class="sxs-lookup"><span data-stu-id="66770-128">Environment</span></span>
<span data-ttu-id="66770-129">**P: É possível renomear o servidor após a instalação do Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="66770-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="66770-130">Não.</span><span class="sxs-lookup"><span data-stu-id="66770-130">No.</span></span> <span data-ttu-id="66770-131">Alterar o nome do servidor fará com que o mecanismo de sincronização não consiga se conectar ao banco de dados SQL e o serviço não poderá iniciar.</span><span class="sxs-lookup"><span data-stu-id="66770-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="66770-132">Dados de identidade</span><span class="sxs-lookup"><span data-stu-id="66770-132">Identity data</span></span>
<span data-ttu-id="66770-133">**P: O atributo UPN (userPrincipalName) no AD do Azure não coincide com o UPN local - por quê?**</span><span class="sxs-lookup"><span data-stu-id="66770-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="66770-134">Consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="66770-134">See these articles:</span></span>

* [<span data-ttu-id="66770-135">Os nomes de usuário no Office 365, Azure ou Intune não coincidem com o UPN local ou a ID de logon alternativa</span><span class="sxs-lookup"><span data-stu-id="66770-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="66770-136">As alterações não são sincronizadas pela ferramenta de sincronização do Azure Active Directory depois que você altera o UPN de uma conta de usuário para usar um domínio federado diferente</span><span class="sxs-lookup"><span data-stu-id="66770-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="66770-137">Você também pode configurar o Azure AD para permitir que o mecanismo de sincronização atualize o userPrincipalName da forma descrita em [Azure AD Connect sync service features (Recursos do serviço de sincronização do Azure AD Connect)](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="66770-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="66770-138">**P: Há suporte para a correspondência suave de objetos de Grupo/Contato do Azure AD no local com objetos de Grupo/Contato existentes do Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="66770-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="66770-139">Não, não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="66770-139">No, this is currently not supported.</span></span>

<span data-ttu-id="66770-140">**P: Há suporte para o atributo ImmutableId definido manualmente em objetos de Grupo/Contato existentes do Azure AD para correspondência rígida com objetos de Grupo/Contato do AD locais?**</span><span class="sxs-lookup"><span data-stu-id="66770-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="66770-141">Não, não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="66770-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="66770-142">Configuração personalizada</span><span class="sxs-lookup"><span data-stu-id="66770-142">Custom configuration</span></span>
<span data-ttu-id="66770-143">**P: Onde os cmdlets do PowerShell para o Azure AD Connect estão documentados?**</span><span class="sxs-lookup"><span data-stu-id="66770-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="66770-144">Com exceção dos cmdlets documentados neste site, não há suporte para outros cmdlets do PowerShell encontrados no Azure AD Connect para uso do cliente.</span><span class="sxs-lookup"><span data-stu-id="66770-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="66770-145">**P: Posso usar a opção "Exportação do servidor/importação do servidor" encontrada no *Synchronization Service Manager* para mover a configuração entre servidores?**</span><span class="sxs-lookup"><span data-stu-id="66770-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="66770-146">Não.</span><span class="sxs-lookup"><span data-stu-id="66770-146">No.</span></span> <span data-ttu-id="66770-147">Essa opção não irá recuperar todos os parâmetros de configuração e não deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="66770-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="66770-148">Em vez disso, você deve usar o assistente para criar a configuração básica no segundo servidor e usar o editor de regra de sincronização para gerar scripts do PowerShell para mover qualquer regra personalizada entre servidores.</span><span class="sxs-lookup"><span data-stu-id="66770-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="66770-149">Confira [Migração Swing](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="66770-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="66770-150">**P: As senhas podem ser armazenadas em cache para a página de entrada do Azure, e isso pode ser evitado, já que contém um elemento de entrada de senha com o atributo de preenchimento automático = "false"?**</span><span class="sxs-lookup"><span data-stu-id="66770-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="66770-151">No momento, não há suporte para a modificação dos atributos HTML do campo de entrada de Senha, incluindo a marca de preenchimento automático.</span><span class="sxs-lookup"><span data-stu-id="66770-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="66770-152">Estamos trabalhando em um recurso que permitirá Javascript personalizado, e permitirá que você adicione qualquer atributo ao campo de senha.</span><span class="sxs-lookup"><span data-stu-id="66770-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="66770-153">Isso deve ser disponibilizado no último semestre de 2017.</span><span class="sxs-lookup"><span data-stu-id="66770-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="66770-154">**P: Na página de entrada do Azure, aparecem os nomes de usuários que se conectaram anteriormente com êxito.  Esse comportamento pode ser desativado?**</span><span class="sxs-lookup"><span data-stu-id="66770-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="66770-155">Atualmente, não há suporte para a modificação dos atributos HTML da página de entrada.</span><span class="sxs-lookup"><span data-stu-id="66770-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="66770-156">Estamos trabalhando em um recurso que permitirá Javascript personalizado, e permitirá que você adicione qualquer atributo ao campo de senha.</span><span class="sxs-lookup"><span data-stu-id="66770-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="66770-157">Isso deve ser disponibilizado no último semestre de 2017.</span><span class="sxs-lookup"><span data-stu-id="66770-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="66770-158">**P: Existe uma maneira de evitar sessões simultâneas?**</span><span class="sxs-lookup"><span data-stu-id="66770-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="66770-159">Não.</span><span class="sxs-lookup"><span data-stu-id="66770-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="66770-160">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="66770-160">Troubleshooting</span></span>
<span data-ttu-id="66770-161">**P: Como posso obter ajuda com o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="66770-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="66770-162">Pesquise a Base de Dados de Conhecimento (KB) Microsoft</span><span class="sxs-lookup"><span data-stu-id="66770-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="66770-163">Pesquise a KB (Base de Dados de Conhecimento) da Microsoft para obter soluções técnicas de conserto de problemas comuns de suporte ao Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="66770-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="66770-164">Fóruns do Active Directory do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="66770-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="66770-165">Você pode pesquisar e procurar perguntas e respostas técnicas na comunidade ou fazer sua própria pergunta clicando [aqui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="66770-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="66770-166">Atendimento ao cliente do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="66770-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="66770-167">Use este link para obter suporte por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="66770-167">Use this link to get support through the Azure portal.</span></span>

