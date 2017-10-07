---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do AD do Azure | Microsoft Docs"
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
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="19ed7-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="19ed7-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="19ed7-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="19ed7-104">Before you begin</span></span>
<span data-ttu-id="19ed7-105">Certifique-se de que você acabou de [tarefa 2 - Olá exportação tooa de certificado segura LDAP. Arquivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="19ed7-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="19ed7-106">Escolha se toouse Olá visualização experiência do portal do Azure ou Olá toocomplete de portal clássico do Azure essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="19ed7-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="19ed7-107">**Portal do Azure (visualização)**: [habilitar secure LDAP usando Olá portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="19ed7-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="19ed7-108">**Portal clássico do Azure**: [habilitar seguro usando o portal do Azure clássico de saudação do LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="19ed7-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="19ed7-109">Tarefa 3 - habilitar LDAP seguro para Olá domínio gerenciado usando Olá portal do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="19ed7-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="19ed7-110">tooenable LDAP seguro, execute Olá etapas de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="19ed7-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="19ed7-111">Navegue toohello  **[portal do Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="19ed7-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="19ed7-112">Procure "serviços de domínio' hello **pesquisar recursos** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="19ed7-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="19ed7-113">Selecione **serviços de domínio do AD do Azure** Olá resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="19ed7-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="19ed7-114">Olá **serviços de domínio do AD do Azure** folha lista o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="19ed7-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Localize o domínio gerenciado que está sendo provisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="19ed7-116">Clique o nome de saudação do hello gerenciado toosee de domínio (por exemplo, ' contoso100.com') mais detalhes sobre o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="19ed7-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services – estado de provisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="19ed7-118">Clique em **LDAP seguro** no painel de navegação de saudação.</span><span class="sxs-lookup"><span data-stu-id="19ed7-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Domain Services – folha LDAP Seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="19ed7-120">Por padrão, o domínio seguro do LDAP acesso tooyour gerenciado está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="19ed7-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="19ed7-121">Ativar/desativar **LDAP seguro** muito**habilitar**.</span><span class="sxs-lookup"><span data-stu-id="19ed7-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Habilitar o LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="19ed7-123">Por padrão, o tooyour de acesso LDAP seguro gerenciados domínio pela Olá que Internet está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="19ed7-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="19ed7-124">Ativar/desativar **Olá de permissões de acesso LDAP seguro através da internet** muito**habilitar**, se desejado.</span><span class="sxs-lookup"><span data-stu-id="19ed7-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="19ed7-125">Clique em seguinte de ícone de pasta Olá **. O arquivo PFX com certificado LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="19ed7-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="19ed7-126">Especifica arquivo PFX do hello caminho toohello com certificado Olá para seguro LDAP acesso toohello domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="19ed7-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="19ed7-127">Especifique a saudação **toodecrypt de senha. Arquivo PFX**.</span><span class="sxs-lookup"><span data-stu-id="19ed7-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="19ed7-128">Fornecer Olá mesma senha usada ao exportar o arquivo PFX do hello certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="19ed7-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="19ed7-129">Quando terminar, clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="19ed7-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="19ed7-130">Você verá uma notificação informando que LDAP seguro está sendo configurado para o domínio gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="19ed7-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="19ed7-131">Até que essa operação for concluída, você não pode modificar outras configurações para o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="19ed7-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Configurar o LDAP seguro para o domínio gerenciado Olá](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="19ed7-133">Leva aproximadamente 10 minutos too15 tooenable LDAP seguro para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="19ed7-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="19ed7-134">Se Olá fornecida seguro de certificados LDAP não coincide com hello necessário critérios, LDAP seguro não está habilitado para seu diretório e você verá uma falha.</span><span class="sxs-lookup"><span data-stu-id="19ed7-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="19ed7-135">Por exemplo, nome de domínio hello está incorreta, certificado Olá já expirou ou expirará em breve.</span><span class="sxs-lookup"><span data-stu-id="19ed7-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="19ed7-136">Nesse caso, tente novamente com um certificado válido.</span><span class="sxs-lookup"><span data-stu-id="19ed7-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="19ed7-137">Tarefa 4 - configurar DNS tooaccess Olá domínio gerenciado de saudação à internet</span><span class="sxs-lookup"><span data-stu-id="19ed7-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="19ed7-138">**Tarefas opcionais** - se você não planeja tooaccess Olá domínio usando LDAPS Olá da internet, para ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="19ed7-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="19ed7-139">Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="19ed7-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="19ed7-140">Depois que você tiver habilitado o acesso LDAP seguro através da internet de Olá para seu domínio gerenciado, você precisa tooupdate DNS para que os computadores cliente possam encontrar este domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="19ed7-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="19ed7-141">Final de saudação de tarefa 3, um endereço IP externo é exibido na Olá **propriedades** folha em **endereço de IP externo para acesso de LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="19ed7-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="19ed7-142">Configure seu provedor DNS externo para que o nome DNS Olá de saudação gerenciado endereço IP externo de pontos toothis domínio (por exemplo, ' ldaps.contoso100.com').</span><span class="sxs-lookup"><span data-stu-id="19ed7-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="19ed7-143">Em nosso exemplo, precisamos Olá toocreate entrada DNS a seguir:</span><span class="sxs-lookup"><span data-stu-id="19ed7-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="19ed7-144">É isso – agora você está pronto tooconnect toohello gerenciado Olá de domínio usando o LDAP seguro através da internet.</span><span class="sxs-lookup"><span data-stu-id="19ed7-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="19ed7-145">Lembre-se de que os computadores cliente devem confiar emissor Olá Olá LDAPS certificado toobe capaz de tooconnect com êxito toohello gerenciados usando LDAPS do domínio.</span><span class="sxs-lookup"><span data-stu-id="19ed7-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="19ed7-146">Se você estiver usando uma autoridade de certificação publicamente confiável, você não é necessário toodo qualquer coisa desde que essas emissores de certificado de confiança de computadores cliente.</span><span class="sxs-lookup"><span data-stu-id="19ed7-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="19ed7-147">Se você estiver usando um certificado autoassinado, instale a parte pública de saudação do certificado autoassinado Olá no hello repositório de certificados confiáveis no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="19ed7-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="19ed7-148">Tarefa 5 - bloqueio LDAPS acesso tooyour gerenciado Olá de domínio através da internet</span><span class="sxs-lookup"><span data-stu-id="19ed7-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="19ed7-149">**Tarefas opcionais** - se você não tiver habilitado o LDAPS domínio gerenciado do acesso toohello Olá da internet, para ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="19ed7-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="19ed7-150">Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="19ed7-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="19ed7-151">Expondo o domínio gerenciado para acesso LDAPS sobre Olá internet representa uma ameaça à segurança.</span><span class="sxs-lookup"><span data-stu-id="19ed7-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="19ed7-152">Olá domínio gerenciado é acessível a partir do hello internet na porta Olá usada para LDAP seguro (ou seja, porta 636).</span><span class="sxs-lookup"><span data-stu-id="19ed7-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="19ed7-153">Portanto, você pode escolher toorestrict acesso toohello gerenciado domínio toospecific conhecido endereços IP.</span><span class="sxs-lookup"><span data-stu-id="19ed7-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="19ed7-154">Para maior segurança, crie um grupo de segurança de rede (NSG) e associá-lo a sub-rede Olá onde você habilitou os serviços de domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="19ed7-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="19ed7-155">Olá, tabela a seguir ilustra um exemplo NSG que você pode configurar, toolock para acesso LDAP seguro através de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="19ed7-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="19ed7-156">Olá NSG contém um conjunto de regras que permitam o acesso LDAPS entrada pela porta TCP 636 somente de um conjunto especificado de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="19ed7-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="19ed7-157">Olá padrão 'DenyAll' regra se aplica tooall outro tráfego de entrada de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="19ed7-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="19ed7-158">Olá NSG regra tooallow LDAPS o acesso por Olá internet de endereços IP especificados tem uma prioridade mais alta que Olá regra DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="19ed7-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Acesso ao exemplo NSG toosecure LDAPS por Olá da internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="19ed7-160">**Mais informações** - [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="19ed7-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="19ed7-161">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="19ed7-161">Related content</span></span>
* [<span data-ttu-id="19ed7-162">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="19ed7-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="19ed7-163">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="19ed7-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="19ed7-164">Administrar a política de grupo em um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="19ed7-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="19ed7-165">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="19ed7-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="19ed7-166">Criar um Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="19ed7-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
