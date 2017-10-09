---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do AD do Azure | Microsoft Docs"
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
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="dba4d-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="dba4d-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dba4d-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="dba4d-104">Before you begin</span></span>
<span data-ttu-id="dba4d-105">Certifique-se de que você acabou de [tarefa 2 - Olá exportação tooa de certificado segura LDAP. Arquivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="dba4d-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="dba4d-106">Escolha se toouse Olá visualização experiência do portal do Azure ou Olá toocomplete de portal clássico do Azure essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="dba4d-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="dba4d-107">**Portal do Azure (visualização)**: [habilitar secure LDAP usando Olá portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="dba4d-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="dba4d-108">**Portal clássico do Azure**: [habilitar seguro usando o portal do Azure clássico de saudação do LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="dba4d-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="dba4d-109">Tarefa 3 - habilitar LDAP seguro para Olá domínio gerenciado usando o portal do Azure clássico de saudação</span><span class="sxs-lookup"><span data-stu-id="dba4d-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="dba4d-110">tooenable LDAP seguro, execute Olá etapas de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="dba4d-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="dba4d-111">Navegue toohello  **[portal clássico do Azure](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="dba4d-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="dba4d-112">Selecione Olá **do Active Directory** nó no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="dba4d-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="dba4d-113">Selecione o diretório de saudação do AD do Azure (também chamado tooas 'locatário'), para o qual você habilitou os serviços de domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dba4d-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Selecionar um diretório do AD do Azure](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="dba4d-115">Clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="dba4d-115">Click hello **Configure** tab.</span></span>

    ![Guia Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="dba4d-117">Role para baixo toohello seção **dos serviços de domínio**.</span><span class="sxs-lookup"><span data-stu-id="dba4d-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="dba4d-118">Você verá uma opção chamada **LDAP seguro (LDAPS)** conforme Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dba4d-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Seção Configuração dos Serviços de Domínio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="dba4d-120">Clique em Olá **configurar certificado...**  toobring botão backup Olá **Configure o certificado para LDAP seguro** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dba4d-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configurar Certificado para LDAP Seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="dba4d-122">Clique em seguinte de ícone de pasta Olá **arquivo com o certificado de PFX** toospecify Olá arquivo PFX que contém o certificado de saudação desejar toouse para toohello de acesso LDAP seguro gerenciados domínio.</span><span class="sxs-lookup"><span data-stu-id="dba4d-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="dba4d-123">Também Inserir senha Olá especificados ao exportar o arquivo PFX do hello certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="dba4d-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="dba4d-124">Clique em Olá feito botão na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="dba4d-124">Then, click hello done button on hello bottom.</span></span>

    ![Especificar arquivo PFX e senha de LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="dba4d-126">Olá **dos serviços de domínio** seção Olá **configurar** guia deve obter esmaecida e estiver em Olá **pendentes...**  estado por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="dba4d-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="dba4d-127">Durante esse período, o certificado LDAPS Olá é verificado quanto à precisão e LDAP seguro está configurado para o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="dba4d-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP Seguro - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="dba4d-129">Leva aproximadamente 10 minutos too15 tooenable LDAP seguro para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="dba4d-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="dba4d-130">Se Olá fornecida seguro de certificados LDAP não coincide com hello necessário critérios, LDAP seguro não está habilitado para seu diretório e você verá uma falha.</span><span class="sxs-lookup"><span data-stu-id="dba4d-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="dba4d-131">Por exemplo, nome de domínio hello está incorreta, certificado Olá já expirou ou expirará em breve.</span><span class="sxs-lookup"><span data-stu-id="dba4d-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="dba4d-132">Quando o LDAP seguro estiver habilitado com êxito para o domínio gerenciado, Olá **pendentes...**  mensagem deverá desaparecer.</span><span class="sxs-lookup"><span data-stu-id="dba4d-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="dba4d-133">Você deve ver a impressão digital de saudação do certificado Olá exibido.</span><span class="sxs-lookup"><span data-stu-id="dba4d-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="dba4d-135">Tarefa 4 - habilitar acesso LDAP seguro sobre Olá internet</span><span class="sxs-lookup"><span data-stu-id="dba4d-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="dba4d-136">**Tarefas opcionais** - se você não planeja tooaccess Olá domínio usando LDAPS Olá da internet, para ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="dba4d-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="dba4d-137">Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="dba4d-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="dba4d-138">Você verá uma opção muito**Olá permitem proteger LDAP acesso pela INTERNET** em Olá **dos serviços de domínio** seção Olá **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="dba4d-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="dba4d-139">Essa opção for definida muito**não** por padrão como toohello de acesso de internet gerenciado domínio sobre LDAP seguro é desabilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="dba4d-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="dba4d-141">Ativar/desativar **Olá permitem proteger LDAP acesso pela INTERNET** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="dba4d-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="dba4d-142">Clique em Olá **salvar** botão no painel inferior de saudação.</span><span class="sxs-lookup"><span data-stu-id="dba4d-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="dba4d-143">![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="dba4d-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="dba4d-144">Olá **dos serviços de domínio** seção Olá **configurar** guia deve obter esmaecida e estiver em Olá **pendentes...**  estado por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="dba4d-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="dba4d-145">Após algum tempo, é habilitado para internet acesso tooyour domínio gerenciados através de LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="dba4d-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![LDAP Seguro - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="dba4d-147">Ele leva cerca de 10 minutos tooenable acesso à internet através de LDAP seguro para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="dba4d-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="dba4d-148">Quando tooyour de acesso LDAP seguro gerenciados domínio pela Olá internet foi habilitado com êxito, Olá **pendentes...**  mensagem deverá desaparecer.</span><span class="sxs-lookup"><span data-stu-id="dba4d-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="dba4d-149">Você deve ver o IP externo de saudação de endereços que podem ser usados tooaccess seu diretório over LDAPS no campo Olá **endereço de IP externo para acesso de LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="dba4d-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="dba4d-151">Tarefa 5 - configurar DNS tooaccess Olá domínio gerenciado de saudação à internet</span><span class="sxs-lookup"><span data-stu-id="dba4d-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="dba4d-152">**Tarefas opcionais** - se você não planeja tooaccess Olá domínio usando LDAPS Olá da internet, para ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="dba4d-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="dba4d-153">Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="dba4d-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="dba4d-154">Depois que você tiver habilitado o acesso LDAP seguro através da internet de Olá para seu domínio gerenciado, você precisa tooupdate DNS para que os computadores cliente possam encontrar este domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="dba4d-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="dba4d-155">Final de saudação de tarefa 4, um endereço IP externo é exibido na Olá **configurar** guia **endereço de IP externo para acesso de LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="dba4d-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="dba4d-156">Configure seu provedor DNS externo para que o nome DNS Olá de saudação gerenciado endereço IP externo de pontos toothis domínio (por exemplo, ' ldaps.contoso100.com').</span><span class="sxs-lookup"><span data-stu-id="dba4d-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="dba4d-157">Em nosso exemplo, precisamos Olá toocreate entrada DNS a seguir:</span><span class="sxs-lookup"><span data-stu-id="dba4d-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="dba4d-158">É isso – agora você está pronto tooconnect toohello gerenciado Olá de domínio usando o LDAP seguro através da internet.</span><span class="sxs-lookup"><span data-stu-id="dba4d-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="dba4d-159">Lembre-se de que os computadores cliente devem confiar emissor Olá Olá LDAPS certificado toobe capaz de tooconnect com êxito toohello gerenciados usando LDAPS do domínio.</span><span class="sxs-lookup"><span data-stu-id="dba4d-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="dba4d-160">Se você estiver usando uma autoridade de certificação corporativa ou de uma autoridade de certificação publicamente confiável, você não precisa toodo nada desde que essas emissores de certificado de confiança de computadores cliente.</span><span class="sxs-lookup"><span data-stu-id="dba4d-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="dba4d-161">Se você estiver usando um certificado autoassinado, você precisa parte pública do tooinstall saudação do certificado autoassinado Olá no repositório de certificados confiáveis de saudação no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="dba4d-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="dba4d-162">Bloqueio LDAPS acessar o domínio gerenciado tooyour pela Olá internet</span><span class="sxs-lookup"><span data-stu-id="dba4d-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="dba4d-163">**Tarefas opcionais** - se você não tiver habilitado o LDAPS domínio gerenciado do acesso toohello Olá da internet, para ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="dba4d-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="dba4d-164">Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="dba4d-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="dba4d-165">Expondo o domínio gerenciado para acesso LDAPS sobre Olá internet representa uma ameaça à segurança.</span><span class="sxs-lookup"><span data-stu-id="dba4d-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="dba4d-166">Olá domínio gerenciado é acessível a partir do hello internet na porta Olá usada para LDAP seguro (ou seja, porta 636).</span><span class="sxs-lookup"><span data-stu-id="dba4d-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="dba4d-167">Portanto, você pode escolher toorestrict acesso toohello gerenciado domínio toospecific conhecido endereços IP.</span><span class="sxs-lookup"><span data-stu-id="dba4d-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="dba4d-168">Para maior segurança, crie um grupo de segurança de rede (NSG) e associá-lo a sub-rede Olá onde você habilitou os serviços de domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dba4d-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="dba4d-169">Olá, tabela a seguir ilustra um exemplo NSG que você pode configurar, toolock para acesso LDAP seguro através de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="dba4d-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="dba4d-170">Olá NSG contém um conjunto de regras que permitam o acesso LDAPS entrada pela porta TCP 636 somente de um conjunto especificado de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="dba4d-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="dba4d-171">Olá padrão 'DenyAll' regra se aplica tooall outro tráfego de entrada de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="dba4d-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="dba4d-172">Olá NSG regra tooallow LDAPS o acesso por Olá internet de endereços IP especificados tem uma prioridade mais alta que Olá regra DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="dba4d-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Acesso ao exemplo NSG toosecure LDAPS por Olá da internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="dba4d-174">**Mais informações** - [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="dba4d-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="dba4d-175">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="dba4d-175">Related content</span></span>
* [<span data-ttu-id="dba4d-176">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="dba4d-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="dba4d-177">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dba4d-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="dba4d-178">Administrar a política de grupo em um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="dba4d-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="dba4d-179">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="dba4d-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="dba4d-180">Criar um Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="dba4d-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
