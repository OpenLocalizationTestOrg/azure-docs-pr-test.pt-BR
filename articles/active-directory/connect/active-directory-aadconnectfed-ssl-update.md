---
title: "Do Azure AD Connect: Certificado SSL de saudação atualização para um farm de serviços de Federação do Active Directory (AD FS) | Microsoft Docs"
description: "Este documento detalhes Olá etapas tooupdate Olá certificado SSL de um farm do AD FS usando o Azure AD Connect."
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
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="955c2-104">Atualizar o certificado SSL de saudação para um farm de serviços de Federação do Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="955c2-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="955c2-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="955c2-105">Overview</span></span>
<span data-ttu-id="955c2-106">Este artigo descreve como você pode usar o certificado SSL do Azure AD Connect tooupdate Olá para um farm de serviços de Federação do Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="955c2-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="955c2-107">Você pode usar o certificado SSL Olá AD do Azure Connect ferramenta tooeasily atualização Olá para o farm do hello AD FS mesmo se o usuário entrar método hello selecionado não é do AD FS.</span><span class="sxs-lookup"><span data-stu-id="955c2-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="955c2-108">Você pode executar a operação de inteiro de saudação de atualizar o certificado SSL para o farm do hello AD FS em todos os servidores de Proxy de aplicativo da Web (WAP) em três etapas simples e federação:</span><span class="sxs-lookup"><span data-stu-id="955c2-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Três etapas](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="955c2-110">toolearn mais sobre os certificados usados pelo AD FS, consulte [Noções básicas sobre os certificados usados pelo AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="955c2-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="955c2-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="955c2-111">Prerequisites</span></span>

* <span data-ttu-id="955c2-112">**Farm do AD FS**: certifique-se de que seu farm do AD FS seja baseado no Windows Server 2012 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="955c2-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="955c2-113">**Azure AD Connect**: Certifique-se de que Olá versão do Azure AD Connect é 1.1.443.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="955c2-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="955c2-114">Você usará a tarefa Olá **atualização AD certificado SSL FS**.</span><span class="sxs-lookup"><span data-stu-id="955c2-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![Atualizar a tarefa SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="955c2-116">Etapa 1: fornecer informações do farm do AD FS</span><span class="sxs-lookup"><span data-stu-id="955c2-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="955c2-117">Azure AD Connect tentativas tooobtain informações sobre o farm do hello AD FS automaticamente pelo:</span><span class="sxs-lookup"><span data-stu-id="955c2-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="955c2-118">Consultando informações de saudação do farm do AD FS (Windows Server 2016 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="955c2-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="955c2-119">Informações de referência Olá de execuções anteriores, que são armazenados localmente com o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="955c2-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="955c2-120">Você pode modificar a lista de saudação de servidores que são exibidas adicionando ou removendo Olá Olá servidores tooreflect atual configuração de farm do hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="955c2-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="955c2-121">Assim como informações de saudação do servidor for fornecidas, o Azure AD Connect exibe conectividade hello e o status atual do certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="955c2-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![Informações do servidor AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="955c2-123">Se a lista de saudação contém um servidor que não faz parte do farm do hello AD FS, clique em **remover** toodelete servidor de saudação da lista de saudação de servidores no farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="955c2-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![Servidor offline na lista](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="955c2-125">Removendo um servidor na lista de saudação de servidores para um AD FS farm no Azure AD Connect é uma operação de local e atualizações Olá informações para Olá farm do AD FS que mantém a conexão do AD do Azure localmente.</span><span class="sxs-lookup"><span data-stu-id="955c2-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="955c2-126">Azure AD Connect não modifica a configuração de Olá no AD FS tooreflect Olá alteração.</span><span class="sxs-lookup"><span data-stu-id="955c2-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="955c2-127">Etapa 2: Fornecer um novo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="955c2-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="955c2-128">Após ter confirmado informações Olá sobre servidores do farm do AD FS, o Azure AD Connect solicita novo certificado SSL Olá.</span><span class="sxs-lookup"><span data-stu-id="955c2-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="955c2-129">Forneça uma instalação do hello toocontinue do certificado, protegido por senha PFX.</span><span class="sxs-lookup"><span data-stu-id="955c2-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![Certificado SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="955c2-131">Depois que você fornecer um certificado hello, Azure AD Connect passa por uma série de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="955c2-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="955c2-132">Verifique se Olá certificado tooensure que Olá certificado está correta para o farm de saudação do AD FS:</span><span class="sxs-lookup"><span data-stu-id="955c2-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="955c2-133">Olá nome de entidade de nome/alternativo de assunto para o certificado de saudação é Olá mesmo como o nome do serviço de Federação hello, ou é um certificado curinga.</span><span class="sxs-lookup"><span data-stu-id="955c2-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="955c2-134">certificado de saudação é válido por mais de 30 dias.</span><span class="sxs-lookup"><span data-stu-id="955c2-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="955c2-135">cadeia de confiança de certificado Olá é válida.</span><span class="sxs-lookup"><span data-stu-id="955c2-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="955c2-136">certificado de saudação é protegido por senha.</span><span class="sxs-lookup"><span data-stu-id="955c2-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="955c2-137">Etapa 3: Selecionar servidores para atualização Olá</span><span class="sxs-lookup"><span data-stu-id="955c2-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="955c2-138">Na próxima etapa de hello, selecione servidores de saudação que precisam de certificado SSL Olá toohave atualizado.</span><span class="sxs-lookup"><span data-stu-id="955c2-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="955c2-139">Servidores que estejam offline não podem ser selecionados para atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="955c2-139">Servers that are offline can't be selected for hello update.</span></span>

![Selecione os servidores tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="955c2-141">Depois de concluir a configuração de hello, Azure AD Connect exibe a mensagem de saudação que indica o status de saudação da atualização de saudação e fornece uma opção tooverify saudação do AD FS entrar.</span><span class="sxs-lookup"><span data-stu-id="955c2-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Configuração concluída](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="955c2-143">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="955c2-143">FAQs</span></span>

* <span data-ttu-id="955c2-144">**O que deve ser o nome da entidade do certificado de saudação Olá para o novo certificado de SSL do AD FS Olá?**</span><span class="sxs-lookup"><span data-stu-id="955c2-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="955c2-145">Azure AD Connect verifica se Olá entidade alternativa de nome/nome da entidade Olá certificado contém nome de serviço de Federação hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="955c2-146">Por exemplo, se o nome do seu serviço de Federação for fs.contoso.com, o nome de entidade alternativo/nome da entidade de Olá deve ser fs.contoso.com.  Certificados curinga também são aceitos.</span><span class="sxs-lookup"><span data-stu-id="955c2-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="955c2-147">**Por que estou, precisará fornecer as credenciais novamente na página de servidor WAP Olá?**</span><span class="sxs-lookup"><span data-stu-id="955c2-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="955c2-148">Se credenciais Olá fornecidas para conectar tooAD FS servidores também não tem servidores WAP Olá privilégio toomanage hello, Azure AD Connect solicita credenciais que tenham privilégios administrativos nos servidores WAP hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="955c2-149">**servidor de saudação é mostrado como offline. O que devo fazer?**</span><span class="sxs-lookup"><span data-stu-id="955c2-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="955c2-150">Azure AD Connect não pode executar qualquer operação se Olá servidor estiver offline.</span><span class="sxs-lookup"><span data-stu-id="955c2-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="955c2-151">Se o servidor de saudação fizer parte de saudação farm do AD FS, em seguida, verifique o servidor de toohello de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="955c2-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="955c2-152">Depois que você resolveu o problema de hello, pressione status de Olá Olá atualização ícone tooupdate no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="955c2-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="955c2-153">Se o servidor de saudação fazia parte da saudação farm anteriormente, mas agora não existe mais, clique em **remover** toodelete da lista de saudação de servidores do Azure AD Connect mantém.</span><span class="sxs-lookup"><span data-stu-id="955c2-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="955c2-154">Remover servidor de saudação da lista de saudação no Azure AD Connect não altera Olá configuração do AD FS em si.</span><span class="sxs-lookup"><span data-stu-id="955c2-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="955c2-155">Se você estiver usando o AD FS no Windows Server 2016 ou posterior, Olá servidor permanece nas definições de configuração de saudação e será exibido novamente hello próxima vez hello tarefa é executada.</span><span class="sxs-lookup"><span data-stu-id="955c2-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="955c2-156">**Pode atualizar um subconjunto dos meus servidores do farm com o novo certificado SSL Olá?**</span><span class="sxs-lookup"><span data-stu-id="955c2-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="955c2-157">Sim.</span><span class="sxs-lookup"><span data-stu-id="955c2-157">Yes.</span></span> <span data-ttu-id="955c2-158">Você também pode executar a tarefa de saudação **certificado de SSL da atualização** novamente Olá tooupdate restantes servidores.</span><span class="sxs-lookup"><span data-stu-id="955c2-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="955c2-159">Em Olá **atualização de certificados de servidores selecionados para SSL** página, você pode classificar a lista Olá de servidores **data de expiração de SSL** tooeasily acessar Olá servidores que ainda não estão atualizados.</span><span class="sxs-lookup"><span data-stu-id="955c2-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="955c2-160">**Eu removi servidor Olá no hello anterior executar, mas ainda está sendo mostrado como offline e listados na página do hello AD FS servidores. Por que é servidor offline Olá ainda existe mesmo depois que removê-lo?**</span><span class="sxs-lookup"><span data-stu-id="955c2-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="955c2-161">Remover servidor de saudação da lista de saudação no Azure AD Connect não removê-lo no hello configuração do AD FS.</span><span class="sxs-lookup"><span data-stu-id="955c2-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="955c2-162">Conexão do AD do Azure faz referência para todas as informações sobre o farm de saudação do AD FS (Windows Server 2016 ou superior).</span><span class="sxs-lookup"><span data-stu-id="955c2-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="955c2-163">Se o servidor de saudação ainda está presente no hello configuração do AD FS, ele será listado em lista hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="955c2-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="955c2-164">Next steps</span></span>

- [<span data-ttu-id="955c2-165">Azure AD Connect e federação</span><span class="sxs-lookup"><span data-stu-id="955c2-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="955c2-166">Gerenciamento e personalização dos Serviços de Federação do Active Directory (AD FS) com o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="955c2-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
