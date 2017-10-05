---
title: "Azure AD Connect: atualize o certificado SSL para um farm dos Serviços de Federação do Active Directory (AD FS) | Microsoft Docs"
description: Este documento detalha as etapas para atualizar o certificado SSL de um farm do AD FS usando o Azure AD Connect.
services: active-directory
keywords: "azure ad connect, atualizar ssl do adfs, atualização do certificado do adfs, alterar certificado do adfs, novo certificado do adfs, certificado do adfs, atualizar certificado ssl do adfs, atualizar adfs do certificado ssl, configurar certificado ssl do adfs, adfs, ssl, certificado, certificado de comunicação do serviço adfs, atualizar federação, configurar federação, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: 87807a203d71b3abfe3e93132eb7d0b82b14b4ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="a4d94-104">Atualizar o certificado SSL para um farm dos Serviços de Federação do Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="a4d94-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="a4d94-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a4d94-105">Overview</span></span>
<span data-ttu-id="a4d94-106">Este artigo descreve como usar o Azure AD Connect para atualizar o certificado SSL para um farm do AD FS (Serviços de Federação do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a4d94-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="a4d94-107">Você pode usar a ferramenta Azure AD Connect para atualizar facilmente o certificado SSL para o farm do AD FS, mesmo que o método selecionado de conexão do usuário não seja o AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4d94-107">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="a4d94-108">Você pode realizar toda a operação de atualização do certificado SSL para o farm do AD FS em todos os servidores de federação e de WAP (Proxy de aplicativo Web) em três etapas simples:</span><span class="sxs-lookup"><span data-stu-id="a4d94-108">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Três etapas](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="a4d94-110">Para saber mais sobre os certificados usados pelo AD FS, confira [Noções básicas sobre os certificados usados pelo AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4d94-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4d94-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4d94-111">Prerequisites</span></span>

* <span data-ttu-id="a4d94-112">**Farm do AD FS**: certifique-se de que seu farm do AD FS seja baseado no Windows Server 2012 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a4d94-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="a4d94-113">**Azure AD Connect**: certifique-se de que a versão do Azure AD Connect seja 1.1.443.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a4d94-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="a4d94-114">Você usará a tarefa **Atualizar certificado SSL do AD FS**.</span><span class="sxs-lookup"><span data-stu-id="a4d94-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![Atualizar a tarefa SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="a4d94-116">Etapa 1: fornecer informações do farm do AD FS</span><span class="sxs-lookup"><span data-stu-id="a4d94-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="a4d94-117">O Azure AD Connect tenta obter as informações sobre o farm do AD FS automaticamente por:</span><span class="sxs-lookup"><span data-stu-id="a4d94-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="a4d94-118">Consulta das informações do farm do AD FS (Windows Server 2016 ou superior).</span><span class="sxs-lookup"><span data-stu-id="a4d94-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="a4d94-119">Referência às informações de execuções anteriores, armazenadas localmente com o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a4d94-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="a4d94-120">Modifique a lista de servidores exibida adicionando ou removendo os servidores para refletir a configuração atual do farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4d94-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="a4d94-121">Assim que as informações do servidor são fornecidas, o Azure AD Connect exibe a conectividade e o status atual do certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="a4d94-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![Informações do servidor AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="a4d94-123">Se a lista contiver um servidor que não faz mais parte do farm do AD FS, clique em **Remover** para excluir o servidor da lista de servidores no farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4d94-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![Servidor offline na lista](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="a4d94-125">A remoção de um servidor da lista de servidores do farm do AD FS no Azure AD Connect é uma operação local e atualiza as informações para o farm do AD FS que o Azure AD Connect mantém localmente.</span><span class="sxs-lookup"><span data-stu-id="a4d94-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="a4d94-126">O Azure AD Connect não modificará à configuração no AD FS para refletir a alteração.</span><span class="sxs-lookup"><span data-stu-id="a4d94-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="a4d94-127">Etapa 2: Fornecer um novo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="a4d94-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="a4d94-128">Depois de confirmar as informações sobre os servidores do farm do AD FS, o Azure AD Connect solicitará o novo certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="a4d94-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="a4d94-129">Forneça um certificado PFX protegido por senha para continuar a instalação.</span><span class="sxs-lookup"><span data-stu-id="a4d94-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![Certificado SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="a4d94-131">Depois de fornecer o certificado, o Azure AD Connect passará por uma série de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="a4d94-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="a4d94-132">Verifique o certificado para garantir que esteja correto para o farm do AD FS:</span><span class="sxs-lookup"><span data-stu-id="a4d94-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="a4d94-133">O nome da entidade/nome alternativo da entidade do certificado é o mesmo que o nome do serviço de federação, ou é um certificado curinga.</span><span class="sxs-lookup"><span data-stu-id="a4d94-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="a4d94-134">O certificado é válido por mais de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="a4d94-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="a4d94-135">A cadeia confiável de certificado é válida.</span><span class="sxs-lookup"><span data-stu-id="a4d94-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="a4d94-136">O certificado é protegido por senha.</span><span class="sxs-lookup"><span data-stu-id="a4d94-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="a4d94-137">Etapa 3: Selecionar servidores para atualização</span><span class="sxs-lookup"><span data-stu-id="a4d94-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="a4d94-138">Na próxima etapa, selecione os servidores que precisam do certificado SSL atualizado.</span><span class="sxs-lookup"><span data-stu-id="a4d94-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="a4d94-139">Servidores offline não podem ser selecionados para a atualização.</span><span class="sxs-lookup"><span data-stu-id="a4d94-139">Servers that are offline can't be selected for the update.</span></span>

![Selecionar servidores para atualizar](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="a4d94-141">Após a conclusão da configuração, o Azure AD Connect exibirá a mensagem que indica o status da atualização e fornece uma opção para verificar a entrada do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4d94-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![Configuração concluída](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="a4d94-143">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="a4d94-143">FAQs</span></span>

* <span data-ttu-id="a4d94-144">**Qual deve ser o nome da entidade do certificado para o novo certificado SSL do AD FS?**</span><span class="sxs-lookup"><span data-stu-id="a4d94-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="a4d94-145">O Azure AD Connect verifica se o nome da entidade/nome da entidade alternativo do certificado contém o nome do serviço de federação.</span><span class="sxs-lookup"><span data-stu-id="a4d94-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="a4d94-146">Por exemplo, se o nome do seu serviço de Federação for fs.contoso.com, o nome da entidade alternativo/nome da entidade deverá ser fs.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a4d94-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="a4d94-147">Certificados curinga também são aceitos.</span><span class="sxs-lookup"><span data-stu-id="a4d94-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="a4d94-148">**Por que as credenciais estão sendo solicitadas novamente na página do servidor WAP?**</span><span class="sxs-lookup"><span data-stu-id="a4d94-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="a4d94-149">Se as credenciais fornecidas para conexão com servidores do AD FS também não tiverem o privilégio para gerenciar os servidores WAP, o Azure AD Connect solicitará credenciais que tenham privilégio administrativo nos servidores WAP.</span><span class="sxs-lookup"><span data-stu-id="a4d94-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="a4d94-150">**O servidor é mostrado como offline. O que devo fazer?**</span><span class="sxs-lookup"><span data-stu-id="a4d94-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="a4d94-151">O Azure AD Connect não poderá executar nenhuma operação se o servidor estiver offline.</span><span class="sxs-lookup"><span data-stu-id="a4d94-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="a4d94-152">Se o servidor fizer parte do farm do AD FS, verifique a conectividade com o servidor.</span><span class="sxs-lookup"><span data-stu-id="a4d94-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="a4d94-153">Depois de resolver o problema, pressione o ícone de atualização para atualizar o status no assistente.</span><span class="sxs-lookup"><span data-stu-id="a4d94-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="a4d94-154">Se o servidor fazia parte do farm, mas agora não existe mais, clique em **Remover** para excluí-lo da lista de servidores que o Azure AD Connect mantém.</span><span class="sxs-lookup"><span data-stu-id="a4d94-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="a4d94-155">Remover o servidor da lista no Azure AD Connect não altera a própria configuração do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4d94-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="a4d94-156">Se você estiver usando o AD FS no Windows Server 2016 ou posterior, o servidor permanecerá nas definições de configuração e será exibido na próxima vez em que a tarefa for executada.</span><span class="sxs-lookup"><span data-stu-id="a4d94-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="a4d94-157">**Posso atualizar um subconjunto dos meus servidores do farm com o novo certificado SSL?**</span><span class="sxs-lookup"><span data-stu-id="a4d94-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="a4d94-158">Sim.</span><span class="sxs-lookup"><span data-stu-id="a4d94-158">Yes.</span></span> <span data-ttu-id="a4d94-159">Você também pode executar a tarefa **Atualizar certificado SSL** novamente para atualizar os servidores restantes.</span><span class="sxs-lookup"><span data-stu-id="a4d94-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="a4d94-160">Na página **Selecionar servidores para atualização de certificado SSL**, você pode classificar a lista de servidores na **Data de expiração do SSL** para acessar facilmente os servidores que ainda não foram atualizados.</span><span class="sxs-lookup"><span data-stu-id="a4d94-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="a4d94-161">**Eu removi o servidor na execução anterior, mas ele ainda está sendo mostrado como offline e listado na página de servidores do AD FS. Por que o servidor offline ainda está lá mesmo após a remoção?**</span><span class="sxs-lookup"><span data-stu-id="a4d94-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="a4d94-162">Remover o servidor da lista no Azure AD Connect não o remove na configuração do AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4d94-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="a4d94-163">O Azure AD Connect consulta o AD FS (Windows Server 2016 ou posterior) para saber quaisquer informações sobre o farm.</span><span class="sxs-lookup"><span data-stu-id="a4d94-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="a4d94-164">Se o servidor ainda estiver presente na configuração do AD FS, ele será relacionado novamente na lista.</span><span class="sxs-lookup"><span data-stu-id="a4d94-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a4d94-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4d94-165">Next steps</span></span>

- [<span data-ttu-id="a4d94-166">Azure AD Connect e federação</span><span class="sxs-lookup"><span data-stu-id="a4d94-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="a4d94-167">Gerenciamento e personalização dos Serviços de Federação do Active Directory (AD FS) com o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="a4d94-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
