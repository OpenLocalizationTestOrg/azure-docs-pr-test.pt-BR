---
title: "Configurar o LDAP Seguro (LDAPS) nos Serviços de Domínio do Azure AD |Microsoft Docs"
description: "Configurar o LDAP Seguro (LDAPS) para um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 3aafe209aad7383cd0610d147b5fdba673023c93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="9c346-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="9c346-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9c346-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="9c346-104">Before you begin</span></span>
<span data-ttu-id="9c346-105">Não deixe de concluir a [Tarefa 2 – exportar o certificado de LDAP seguro para um arquivo .PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="9c346-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="9c346-106">Escolha se deseja usar a experiência de versão prévia do portal do Azure ou o portal clássico do Azure para concluir esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="9c346-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9c346-107">**Portal do Azure (Versão prévia)**: [habilitar o LDAP seguro usando o portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="9c346-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="9c346-108">**Portal clássico do Azure**: [habilitar o LDAP seguro usando o portal do Azure clássico](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="9c346-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal"></a><span data-ttu-id="9c346-109">Tarefa 3 – habilitar o LDAP seguro para o domínio gerenciado usando o portal do Azure clássico</span><span class="sxs-lookup"><span data-stu-id="9c346-109">Task 3 - enable secure LDAP for the managed domain using the classic Azure portal</span></span>
<span data-ttu-id="9c346-110">Execute as seguintes etapas de configuração para habilitar o LDAP seguro:</span><span class="sxs-lookup"><span data-stu-id="9c346-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="9c346-111">Navegue até o **[portal clássico do Azure](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="9c346-111">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="9c346-112">No painel esquerdo, selecione o nó **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="9c346-112">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="9c346-113">Selecione o diretório do AD do Azure (também conhecido como “locatário”), para o qual você habilitou os Serviços de Domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c346-113">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Selecionar um diretório do AD do Azure](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="9c346-115">Clique na guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="9c346-115">Click the **Configure** tab.</span></span>

    ![Guia Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="9c346-117">Role para baixo até a seção chamada **serviços de domínio**.</span><span class="sxs-lookup"><span data-stu-id="9c346-117">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="9c346-118">Você verá uma opção chamada **LDAP Seguro (LDAPS)** , como mostra a captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c346-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![Seção Configuração dos Serviços de Domínio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="9c346-120">Clique no botão **Configurar certificado...** para exibir a caixa de diálogo **Configurar Certificado para LDAP Seguro**.</span><span class="sxs-lookup"><span data-stu-id="9c346-120">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configurar Certificado para LDAP Seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="9c346-122">Clique no ícone de pasta após **ARQUIVO PFX COM CERTIFICADO** para especificar o arquivo PFX que contém o certificado que você deseja usar para ter acesso LDAP seguro ao domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9c346-122">Click the folder icon following **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="9c346-123">Além disso, insira a senha que você especificou ao exportar o certificado para o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="9c346-123">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="9c346-124">Em seguida, clique no botão Concluído na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9c346-124">Then, click the done button on the bottom.</span></span>

    ![Especificar arquivo PFX e senha de LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="9c346-126">A seção **serviços de domínio** da guia **Configurar** deve ficar esmaecida e permanecerá no estado **Pendente...** por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9c346-126">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="9c346-127">Durante esse período, a precisão do certificado LDAPS é verificada e o LDAP seguro é configurado para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9c346-127">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP Seguro - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="9c346-129">Demora cerca de 10 a 15 minutos para habilitar o LDAP seguro para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9c346-129">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="9c346-130">Se o certificado LDAP seguro fornecido não corresponder aos critérios necessários, LDAP seguro não estará habilitado para o diretório e você verá uma falha.</span><span class="sxs-lookup"><span data-stu-id="9c346-130">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="9c346-131">Por exemplo, o nome de domínio está incorreto, o certificado expirou ou expirará em breve.</span><span class="sxs-lookup"><span data-stu-id="9c346-131">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="9c346-132">Quando o LDAP seguro for habilitado com êxito para o domínio gerenciado, a mensagem **Pendente...** desaparecerá.</span><span class="sxs-lookup"><span data-stu-id="9c346-132">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="9c346-133">Você deverá ver a impressão digital do certificado exibida.</span><span class="sxs-lookup"><span data-stu-id="9c346-133">You should see the thumbprint of the certificate displayed.</span></span>

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="9c346-135">Tarefa 4 – habilitar o acesso LDAP seguro pela Internet</span><span class="sxs-lookup"><span data-stu-id="9c346-135">Task 4 - enable secure LDAP access over the internet</span></span>
<span data-ttu-id="9c346-136">**Tarefa opcional** – Ignore esta tarefa de configuração se você não pretende acessar o domínio gerenciado usando LDAPS pela Internet.</span><span class="sxs-lookup"><span data-stu-id="9c346-136">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="9c346-137">Antes de iniciar esta tarefa, verifique se você concluiu as etapas descritas na [Tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9c346-137">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="9c346-138">Você verá uma opção para **HABILITAR O ACESSO LDAP SEGURO PELA INTERNET** na seção **serviços de domínio** da página **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="9c346-138">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="9c346-139">Isso será definido como **NÃO** por padrão, pois o acesso da Internet ao domínio gerenciado por meio de LDAP seguro está desabilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="9c346-139">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="9c346-141">Alterne **HABILITAR ACESSO LDAP SEGURO PELA INTERNET** para **SIM**.</span><span class="sxs-lookup"><span data-stu-id="9c346-141">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="9c346-142">Clique no botão **SALVAR** no painel inferior.</span><span class="sxs-lookup"><span data-stu-id="9c346-142">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="9c346-143">![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="9c346-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="9c346-144">A seção **serviços de domínio** da guia **Configurar** deve ficar esmaecida e permanecerá no estado **Pendente...** por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9c346-144">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="9c346-145">Após algum tempo, o acesso à Internet para seu domínio gerenciado por meio de LDAP seguro será habilitado.</span><span class="sxs-lookup"><span data-stu-id="9c346-145">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![LDAP Seguro - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="9c346-147">Demora cerca de 10 minutos para habilitar o acesso da Internet por meio de LDAP seguro para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9c346-147">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="9c346-148">Quando o acesso LDAP seguro para seu domínio gerenciado pela Internet for habilitado com êxito, a mensagem **Pendente...** desaparecerá.</span><span class="sxs-lookup"><span data-stu-id="9c346-148">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="9c346-149">Você deve ver o endereço IP externo que pode ser usado para acessar seu diretório por meio de LDAPS no campo **ENDEREÇO IP EXTERNO PARA ACESSO LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="9c346-149">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="9c346-151">Tarefa 5 – configurar o DNS para acessar o domínio gerenciado pela Internet</span><span class="sxs-lookup"><span data-stu-id="9c346-151">Task 5 - configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="9c346-152">**Tarefa opcional** – Ignore esta tarefa de configuração se você não pretende acessar o domínio gerenciado usando LDAPS pela Internet.</span><span class="sxs-lookup"><span data-stu-id="9c346-152">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="9c346-153">Antes de iniciar esta tarefa, verifique se você concluiu as etapas descritas na [Tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="9c346-153">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="9c346-154">Depois que você habilitar o acesso LDAP seguro pela Internet para seu domínio gerenciado, será necessário atualizar o DNS para que os computadores cliente possam localizar esse domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="9c346-154">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="9c346-155">No final da tarefa 4, um endereço IP externo é exibido na guia **Configurar**, em **ENDEREÇO IP EXTERNO PARA ACESSO LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="9c346-155">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="9c346-156">Configure seu provedor DNS externo para que o nome DNS do domínio gerenciado (por exemplo, 'ldaps.contoso100.com') aponte para esse endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="9c346-156">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="9c346-157">Em nosso exemplo, precisaremos criar a entrada DNS a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c346-157">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="9c346-158">Isso é tudo - agora você está pronto para se conectar ao domínio gerenciado usando LDAP seguro pela Internet.</span><span class="sxs-lookup"><span data-stu-id="9c346-158">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="9c346-159">Lembre-se de que os computadores cliente devem confiar no emissor do certificado LDAPS para poderem se conectar com êxito ao domínio gerenciado usando LDAPS.</span><span class="sxs-lookup"><span data-stu-id="9c346-159">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="9c346-160">Se você estiver usando uma autoridade de certificação corporativa ou uma autoridade de certificação confiável publicamente, não será necessário fazer qualquer coisa, pois os computadores clientes confiarão nesses emissores de certificado.</span><span class="sxs-lookup"><span data-stu-id="9c346-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="9c346-161">Se você estiver usando um certificado autoassinado, precisará instalar a parte pública do certificado autoassinado no repositório de certificados confiáveis no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="9c346-161">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="9c346-162">Bloquear o acesso LDAPS ao domínio gerenciado pela Internet</span><span class="sxs-lookup"><span data-stu-id="9c346-162">Lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="9c346-163">**Tarefa opcional** – ignore esta tarefa de configuração se você não tiver habilitado o acesso LDAPS ao domínio gerenciado pela Internet.</span><span class="sxs-lookup"><span data-stu-id="9c346-163">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="9c346-164">Antes de iniciar esta tarefa, verifique se você concluiu as etapas descritas na [Tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="9c346-164">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="9c346-165">Expor seu domínio gerenciado para acesso LDAPS pela Internet representa uma ameaça à segurança.</span><span class="sxs-lookup"><span data-stu-id="9c346-165">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="9c346-166">O domínio gerenciado é acessível pela Internet na porta usada para LDAP seguro (ou seja, a porta 636).</span><span class="sxs-lookup"><span data-stu-id="9c346-166">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="9c346-167">Portanto, você pode optar por restringir o acesso ao domínio gerenciado a endereços IP conhecidos específicos.</span><span class="sxs-lookup"><span data-stu-id="9c346-167">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="9c346-168">Para segurança aprimorada, crie um NSG (grupo de segurança de rede) e associe-o à sub-rede na qual você habilitou o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="9c346-168">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="9c346-169">A tabela a seguir ilustra um exemplo de NSG que você pode configurar para bloquear o acesso LDAP seguro pela Internet.</span><span class="sxs-lookup"><span data-stu-id="9c346-169">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="9c346-170">O NSG contém um conjunto de regras que permitem o acesso LDAPS de entrada pela porta TCP 636 somente de um conjunto especificado de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="9c346-170">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="9c346-171">A regra “DenyAll” padrão se aplica a todos os outros tráfegos de entrada da Internet.</span><span class="sxs-lookup"><span data-stu-id="9c346-171">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="9c346-172">A regra de NSG para permitir o acesso LDAPS pela Internet de endereços IP especificados tem prioridade mais alta que a regra de NSG DenyAll.</span><span class="sxs-lookup"><span data-stu-id="9c346-172">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Exemplo de NSG para acesso LDAPS seguro pela Internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="9c346-174">**Mais informações** - [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="9c346-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="9c346-175">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="9c346-175">Related content</span></span>
* [<span data-ttu-id="9c346-176">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="9c346-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="9c346-177">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c346-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="9c346-178">Administrar a política de grupo em um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="9c346-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="9c346-179">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="9c346-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="9c346-180">Criar um Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="9c346-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
