---
title: "Configurar o LDAP Seguro (LDAPS) nos Serviços de Domínio do Azure AD |Microsoft Docs"
description: "Configurar o LDAP Seguro (LDAPS) para um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="97386-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="97386-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="97386-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="97386-104">Before you begin</span></span>
<span data-ttu-id="97386-105">Não deixe de concluir a [Tarefa 2 – exportar o certificado de LDAP seguro para um arquivo .PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="97386-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="97386-106">Escolha se deseja usar a experiência de versão prévia do portal do Azure ou o portal clássico do Azure para concluir esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="97386-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="97386-107">**Portal do Azure (Versão prévia)**: [habilitar o LDAP seguro usando o portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="97386-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="97386-108">**Portal clássico do Azure**: [habilitar o LDAP seguro usando o portal do Azure clássico](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="97386-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a><span data-ttu-id="97386-109">Tarefa 3 – habilitar o LDAP seguro para o domínio gerenciado usando o portal do Azure (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="97386-109">Task 3 - enable secure LDAP for the managed domain using the Azure portal (Preview)</span></span>
<span data-ttu-id="97386-110">Execute as seguintes etapas de configuração para habilitar o LDAP seguro:</span><span class="sxs-lookup"><span data-stu-id="97386-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="97386-111">Navegue até o **[Portal do Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="97386-111">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="97386-112">Pesquise por “domain services” na caixa de pesquisa **Pesquisar recursos**.</span><span class="sxs-lookup"><span data-stu-id="97386-112">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="97386-113">Selecione **Azure AD Domain Services** nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="97386-113">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="97386-114">A folha **Azure AD Domain Services** lista seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="97386-114">The **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Localize o domínio gerenciado que está sendo provisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="97386-116">Clique no nome do domínio gerenciado (por exemplo, "contoso100.com") para ver mais detalhes sobre ele.</span><span class="sxs-lookup"><span data-stu-id="97386-116">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services – estado de provisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="97386-118">Clique em **LDAP Seguro** no painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="97386-118">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Domain Services – folha LDAP Seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="97386-120">Por padrão, o acesso LDAP seguro ao seu domínio gerenciado fica desabilitado.</span><span class="sxs-lookup"><span data-stu-id="97386-120">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="97386-121">Posicione a tecla de alternância **LDAP Seguro** em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="97386-121">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![Habilitar o LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="97386-123">Por padrão, o acesso LDAP seguro ao seu domínio gerenciado pela Internet fica desabilitado.</span><span class="sxs-lookup"><span data-stu-id="97386-123">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="97386-124">Posicione a tecla de alternância **Permitir acesso LDAP seguro na Internet** em **Habilitar**, se desejar.</span><span class="sxs-lookup"><span data-stu-id="97386-124">Toggle **Allow secure LDAP access over the internet** to **Enable**, if desired.</span></span> 

6. <span data-ttu-id="97386-125">Clique no ícone de pasta após **Arquivo .PFX com certificado LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="97386-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="97386-126">Especifique o caminho para o arquivo PFX com o certificado para acesso LDAP seguro ao domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="97386-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="97386-127">Especifique a **Senha para descriptografar o arquivo PFX**.</span><span class="sxs-lookup"><span data-stu-id="97386-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="97386-128">Insira a mesma senha que você usou ao exportar o certificado para o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="97386-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="97386-129">Quando tiver terminado, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="97386-129">When you are done, click the **Save** button.</span></span>

9. <span data-ttu-id="97386-130">Você verá uma notificação informando que o LDAP seguro está sendo configurado para o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="97386-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="97386-131">Até que essa operação seja concluída, você não poderá modificar outras configurações do domínio.</span><span class="sxs-lookup"><span data-stu-id="97386-131">Until this operation is complete, you cannot modify other settings for the domain.</span></span>

    ![Configurando LDAP seguro para o domínio gerenciado](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="97386-133">Demora cerca de 10 a 15 minutos para habilitar o LDAP seguro para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="97386-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="97386-134">Se o certificado LDAP seguro fornecido não corresponder aos critérios necessários, LDAP seguro não estará habilitado para o diretório e você verá uma falha.</span><span class="sxs-lookup"><span data-stu-id="97386-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="97386-135">Por exemplo, o nome de domínio está incorreto, o certificado expirou ou expirará em breve.</span><span class="sxs-lookup"><span data-stu-id="97386-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="97386-136">Nesse caso, tente novamente com um certificado válido.</span><span class="sxs-lookup"><span data-stu-id="97386-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="97386-137">Tarefa 4 – configurar o DNS para acessar o domínio gerenciado pela Internet</span><span class="sxs-lookup"><span data-stu-id="97386-137">Task 4 - configure DNS to access the managed domain from the internet</span></span>
> [!NOTE]
> <span data-ttu-id="97386-138">**Tarefa opcional** – Ignore esta tarefa de configuração se você não pretende acessar o domínio gerenciado usando LDAPS pela Internet.</span><span class="sxs-lookup"><span data-stu-id="97386-138">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="97386-139">Antes de iniciar esta tarefa, verifique se você concluiu as etapas descritas na [Tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="97386-139">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="97386-140">Depois que você habilitar o acesso LDAP seguro pela Internet para seu domínio gerenciado, será necessário atualizar o DNS para que os computadores cliente possam localizar esse domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="97386-140">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="97386-141">No final da tarefa 3, um endereço IP externo é exibido na folha **Propriedades**, em **ENDEREÇO IP EXTERNO PARA ACESSO LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="97386-141">At the end of task 3, an external IP address is displayed on the **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="97386-142">Configure seu provedor DNS externo para que o nome DNS do domínio gerenciado (por exemplo, 'ldaps.contoso100.com') aponte para esse endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="97386-142">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="97386-143">Em nosso exemplo, precisaremos criar a entrada DNS a seguir:</span><span class="sxs-lookup"><span data-stu-id="97386-143">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="97386-144">Isso é tudo - agora você está pronto para se conectar ao domínio gerenciado usando LDAP seguro pela Internet.</span><span class="sxs-lookup"><span data-stu-id="97386-144">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="97386-145">Lembre-se de que os computadores cliente devem confiar no emissor do certificado LDAPS para poderem se conectar com êxito ao domínio gerenciado usando LDAPS.</span><span class="sxs-lookup"><span data-stu-id="97386-145">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="97386-146">Se estiver usando uma autoridade de certificação confiável publicamente, você não precisará fazer nada, pois os computadores cliente confiarão nesses emissores de certificado.</span><span class="sxs-lookup"><span data-stu-id="97386-146">If you are using a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="97386-147">Se estiver usando um certificado autoassinado, instale a parte pública do certificado autoassinado no repositório de certificados confiáveis no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="97386-147">If you are using a self-signed certificate, install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="97386-148">Tarefa 5 – bloquear o acesso LDAPS ao domínio gerenciado pela Internet</span><span class="sxs-lookup"><span data-stu-id="97386-148">Task 5 - lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="97386-149">**Tarefa opcional** – ignore esta tarefa de configuração se você não tiver habilitado o acesso LDAPS ao domínio gerenciado pela Internet.</span><span class="sxs-lookup"><span data-stu-id="97386-149">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="97386-150">Antes de iniciar esta tarefa, verifique se você concluiu as etapas descritas na [Tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="97386-150">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="97386-151">Expor seu domínio gerenciado para acesso LDAPS pela Internet representa uma ameaça à segurança.</span><span class="sxs-lookup"><span data-stu-id="97386-151">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="97386-152">O domínio gerenciado é acessível pela Internet na porta usada para LDAP seguro (ou seja, a porta 636).</span><span class="sxs-lookup"><span data-stu-id="97386-152">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="97386-153">Portanto, você pode optar por restringir o acesso ao domínio gerenciado a endereços IP conhecidos específicos.</span><span class="sxs-lookup"><span data-stu-id="97386-153">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="97386-154">Para segurança aprimorada, crie um NSG (grupo de segurança de rede) e associe-o à sub-rede na qual você habilitou o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="97386-154">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="97386-155">A tabela a seguir ilustra um exemplo de NSG que você pode configurar para bloquear o acesso LDAP seguro pela Internet.</span><span class="sxs-lookup"><span data-stu-id="97386-155">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="97386-156">O NSG contém um conjunto de regras que permitem o acesso LDAPS de entrada pela porta TCP 636 somente de um conjunto especificado de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="97386-156">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="97386-157">A regra “DenyAll” padrão se aplica a todos os outros tráfegos de entrada da Internet.</span><span class="sxs-lookup"><span data-stu-id="97386-157">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="97386-158">A regra de NSG para permitir o acesso LDAPS pela Internet de endereços IP especificados tem prioridade mais alta que a regra de NSG DenyAll.</span><span class="sxs-lookup"><span data-stu-id="97386-158">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Exemplo de NSG para acesso LDAPS seguro pela Internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="97386-160">**Mais informações** - [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="97386-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="97386-161">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="97386-161">Related content</span></span>
* [<span data-ttu-id="97386-162">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="97386-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="97386-163">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="97386-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="97386-164">Administrar a política de grupo em um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="97386-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="97386-165">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="97386-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="97386-166">Criar um Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="97386-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
