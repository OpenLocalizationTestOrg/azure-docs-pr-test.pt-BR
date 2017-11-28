---
title: aaaConfigure um Azure conta executar como | Microsoft Docs
description: "Este tutorial orienta você através do uso de criação, teste e exemplo hello de autenticação de entidade de segurança na automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nome principal do serviço, setspn, autenticação do azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="6d6a1-104">Autenticar runbooks com uma conta Executar como do Azure</span><span class="sxs-lookup"><span data-stu-id="6d6a1-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="6d6a1-105">Este artigo mostra como a conta no portal do Azure de saudação tooconfigure um objeto de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="6d6a1-106">toodo assim, você pode usar Olá executar como conta recurso tooauthenticate runbooks gerenciar recursos no Gerenciador de recursos do Azure ou gerenciamento de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="6d6a1-107">Quando você cria uma conta de automação em Olá portal do Azure, criar automaticamente duas contas:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="6d6a1-108">Uma conta Executar como.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-108">A Run As account.</span></span> <span data-ttu-id="6d6a1-109">Essa conta cria uma entidade de serviço no Azure AD (Azure Active Directory) e um certificado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="6d6a1-110">Ele também atribui Olá Colaborador acesso baseado em função RBAC (controle), que gerencia os recursos do Gerenciador de recursos por meio de runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="6d6a1-111">Uma conta Executar como clássica.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-111">A Classic Run As account.</span></span> <span data-ttu-id="6d6a1-112">Essa conta carrega um certificado de gerenciamento, que é usada toomanage gerenciamento de serviços ou recursos clássicos por meio de runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="6d6a1-113">Criar uma conta simplifica o processo de saudação para você e ajuda a que iniciar rapidamente criando e implantando toosupport runbooks de automação a automação precisa.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="6d6a1-114">Com contas Executar como e Executar como Clássica, você pode:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="6d6a1-115">Fornecem uma maneira padronizada tooauthenticate com o Azure ao gerenciar o Gerenciador de recursos ou recursos de gerenciamento de serviços de runbooks em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="6d6a1-116">Automatize o uso de saudação do runbooks global, o que você pode configurar alertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="6d6a1-117">Olá [recurso de integração do Azure alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) com automação runbooks global exige uma conta de automação que é configurada com uma conta executar como e uma conta clássico executar como.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="6d6a1-118">Você pode selecionar uma conta de automação que já tenha definido as contas executar como e clássico executar como ou, você pode escolher toocreate uma nova conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="6d6a1-119">Este artigo mostra como toocreate uma conta de automação da saudação portal do Azure, atualizar uma conta de automação usando o PowerShell do Azure, gerenciar a configuração de conta hello e autenticar em seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="6d6a1-120">Antes de começar a criar uma conta de automação, ele é uma boa ideia toounderstand e considere Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="6d6a1-121">Criar uma conta de automação não afeta as contas de automação, que você pode ter já criado em Olá clássico ou modelo de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="6d6a1-122">processo de saudação funciona apenas para contas de automação que você cria no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="6d6a1-123">Tentativa de toocreate uma conta de saudação portal clássico do Azure não replicar configuração Executar como conta hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="6d6a1-124">Se você já tiver runbooks e ativos (como agendas ou variáveis) em vigor toomanage os recursos clássicos e deseja tooauthenticate runbooks com hello nova clássico conta executar como, siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="6d6a1-125">toocreate uma conta clássico executar como, siga as instruções de saudação na seção de "Gerenciando sua conta executar como" hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="6d6a1-126">tooupdate sua conta existente, use Olá PowerShell script na seção de "Atualizar sua conta de automação usando o PowerShell" hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="6d6a1-127">tooauthenticate usando Olá nova conta executar como e a conta de execução clássico como automação, você precisa toomodify seus runbooks existentes com hello código de exemplo fornecido na seção Olá [exemplos de código de autenticação](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="6d6a1-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="6d6a1-128">Olá conta executar como é para autenticação com base nos recursos do Gerenciador de recursos usando Olá entidade de serviço baseada em certificado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="6d6a1-129">Olá clássico executar como conta é para autenticação com base nos recursos de gerenciamento de serviço com um certificado de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="6d6a1-130">Criar uma conta de automação de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6d6a1-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="6d6a1-131">Nesta seção, você pode criar uma conta de automação do Azure de saudação portal do Azure, que por sua vez, cria uma conta executar como e uma conta clássico executar como.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="6d6a1-132">toocreate uma conta de automação, você deve ser um membro da função de administradores de serviço hello ou coadministrador da assinatura de saudação que está concedendo acesso toohello assinatura.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="6d6a1-133">Você também deve ser adicionado como instância de Active Directory da assinatura de toothat um usuário padrão.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="6d6a1-134">Olá conta não precisa toobe atribuído a uma função com privilégios.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="6d6a1-135">Se você não for um membro da instância do Active Directory da assinatura Olá antes que sejam adicionadas toohello função de coadministrador da assinatura hello, serão adicionados tooActive diretório como convidado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="6d6a1-136">Nesse caso, você receberá um "você não tem permissões toocreate..."</span><span class="sxs-lookup"><span data-stu-id="6d6a1-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="6d6a1-137">saudação de aviso **adicionar conta de automação** folha.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="6d6a1-138">Os usuários que foram adicionados a função de coadministrador toohello primeiro pode ser removida da instância do Active Directory da assinatura hello e adicionado novamente toomake-los como um usuário completo no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="6d6a1-139">tooverify essa situação de saudação **Active Directory do Azure** painel Olá portal do Azure, selecionando **usuários e grupos**, selecionando **todos os usuários** e, depois de selecionar usuário específico do Hello, selecionando **perfil**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="6d6a1-140">Olá valor Olá **o tipo de usuário** atributo sob o perfil de usuários Olá não deve ser iguais **convidado**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="6d6a1-141">Entrar no portal do Azure com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação do toohello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="6d6a1-142">Selecione **Contas de Automação**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="6d6a1-143">Em Olá **contas de automação** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="6d6a1-144">Olá **adicionar conta de automação** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-144">hello **Add Automation Account** blade opens.</span></span>

 ![folha de "Adicionar conta de automação" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="6d6a1-146">Se sua conta não é um membro da função de administradores de assinatura hello e coadministrador da assinatura hello, Olá aviso a seguir será exibida em Olá **adicionar conta de automação** folha:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Aviso Adicionar Conta de Automação](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="6d6a1-148">Em Olá **adicionar conta de automação** folha em Olá **nome** , digite um nome para sua nova conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="6d6a1-149">Se você tiver mais de uma assinatura, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="6d6a1-150">a.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-150">a.</span></span> <span data-ttu-id="6d6a1-151">Em **assinatura**, especifique uma nova conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="6d6a1-152">b.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-152">b.</span></span> <span data-ttu-id="6d6a1-153">Em **Grupo de Recursos**, clique em **Criar novo** ou **Usar existente**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="6d6a1-154">c.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-154">c.</span></span> <span data-ttu-id="6d6a1-155">Em **Local**, especifique um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="6d6a1-156">Em **Criar conta Executar como do Azure**, selecione **Sim**e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6d6a1-157">Se você escolher não toocreate Olá conta executar como selecionando **não**, será exibida uma mensagem de aviso Olá **adicionar conta de automação** folha.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="6d6a1-158">Embora Olá conta é criada no hello portal do Azure, ele não tem uma identidade de autenticação correspondente dentro de sua clássico ou serviço de diretório de assinatura do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="6d6a1-159">Consequentemente, a conta de saudação não tem tooresources nenhum acesso em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="6d6a1-160">Este cenário impede que todos os runbooks que fazem referência a essa conta se autenticaquem e executem tarefas em recursos nesses modelos de implantação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Mensagem de aviso na folha de "Adicionar conta de automação" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="6d6a1-162">Além disso, como entidade de serviço Olá não é criada, função de Colaborador Olá não está atribuída.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="6d6a1-163">Enquanto o Azure cria a conta de automação hello, você pode acompanhar o progresso de saudação em **notificações** menu hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="6d6a1-164">Recursos</span><span class="sxs-lookup"><span data-stu-id="6d6a1-164">Resources</span></span>
<span data-ttu-id="6d6a1-165">Quando a conta de automação de saudação é criada com êxito, vários recursos são criados automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="6d6a1-166">recursos de saudação estão resumidos na Olá duas tabelas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="6d6a1-167">Recursos da conta Executar como</span><span class="sxs-lookup"><span data-stu-id="6d6a1-167">Run As account resources</span></span>

| <span data-ttu-id="6d6a1-168">Recurso</span><span class="sxs-lookup"><span data-stu-id="6d6a1-168">Resource</span></span> | <span data-ttu-id="6d6a1-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="6d6a1-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d6a1-170">Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="6d6a1-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="6d6a1-171">Um runbook gráfico de exemplo que demonstra como tooauthenticate usando Olá conta executar como e obtém todos os recursos do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="6d6a1-172">Runbook do AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="6d6a1-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="6d6a1-173">Um runbook do PowerShell de exemplo que demonstra como tooauthenticate usando Olá conta executar como e obtém todos os recursos do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="6d6a1-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="6d6a1-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="6d6a1-175">ativo de certificado da saudação que é criado automaticamente quando você criar uma conta de automação ou usar Olá seguinte script do PowerShell para uma conta existente.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="6d6a1-176">Olá certificado permite que você tooauthenticate com o Azure para que você possa gerenciar recursos do Gerenciador de recursos do Azure de runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="6d6a1-177">certificado de saudação tem um tempo de vida de um ano.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="6d6a1-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="6d6a1-178">AzureRunAsConnection</span></span> | <span data-ttu-id="6d6a1-179">ativo de conexão de saudação que é criado automaticamente quando você criar uma conta de automação ou usar o script do PowerShell Olá para uma conta existente.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="6d6a1-180">Recursos de conta Executar como clássica</span><span class="sxs-lookup"><span data-stu-id="6d6a1-180">Classic Run As account resources</span></span>

| <span data-ttu-id="6d6a1-181">Recurso</span><span class="sxs-lookup"><span data-stu-id="6d6a1-181">Resource</span></span> | <span data-ttu-id="6d6a1-182">Descrição</span><span class="sxs-lookup"><span data-stu-id="6d6a1-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d6a1-183">Runbook do AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="6d6a1-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="6d6a1-184">Um exemplo de runbook gráfico que obtém todas as VMs de saudação que são criados usando o modelo de implantação clássico Olá em uma assinatura usando Olá clássico executar como conta (certificado) e grava status e nome VM hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="6d6a1-185">Runbook do script AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="6d6a1-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="6d6a1-186">Um exemplo de runbook do PowerShell que obtém todos os Olá clássicas VMs em uma assinatura usando Olá clássico executar como conta (certificado) e, em seguida, grava Olá status e nome VM.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="6d6a1-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="6d6a1-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="6d6a1-188">ativo de certificado Olá criado automaticamente usar tooauthenticate com o Azure, para que você possa gerenciar recursos clássicos do Azure de runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="6d6a1-189">certificado de saudação tem um tempo de vida de um ano.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="6d6a1-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="6d6a1-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="6d6a1-191">ativo de conexão criadas automaticamente Olá usar tooauthenticate com o Azure, para que você possa gerenciar recursos clássicos do Azure de runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="6d6a1-192">Verificar a autenticação de Executar como</span><span class="sxs-lookup"><span data-stu-id="6d6a1-192">Verify Run As authentication</span></span>
<span data-ttu-id="6d6a1-193">Execute um tooconfirm de teste pequena que pode autenticar com êxito usando Olá nova conta executar como.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="6d6a1-194">No portal do Azure de Olá, abra conta de automação de saudação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="6d6a1-195">Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="6d6a1-196">Selecione Olá **AzureAutomationTutorialScript** runbook e, em seguida, clique em **iniciar** toostart Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="6d6a1-197">Olá eventos a seguir ocorre:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-197">hello following events occur:</span></span>
 * <span data-ttu-id="6d6a1-198">Um [trabalho de runbook](automation-runbook-execution.md) é criado, hello **trabalho** folha é exibida, e o status do trabalho Olá é exibido na Olá **resumo do trabalho** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="6d6a1-199">status do trabalho Olá começa como **na fila**, indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="6d6a1-200">o status de saudação se torna **iniciando** quando um trabalhador declarações trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="6d6a1-201">Olá status se torna **executando** quando Olá runbook é iniciado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="6d6a1-202">Quando a execução do trabalho de runbook Olá for concluída, você verá um status de **concluído**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="6d6a1-203">toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="6d6a1-204">Olá **saída** folha é exibida, mostrando esse runbook Olá autenticado e retornou uma lista de todos os recursos disponíveis no grupo de recursos de saudação com êxito.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="6d6a1-205">Olá fechar **saída** folha tooreturn toohello **resumo do trabalho** folha.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="6d6a1-206">Olá fechar **resumo do trabalho** folha e Olá correspondente **AzureAutomationTutorialScript** folha do runbook.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="6d6a1-207">Verificar a autenticação de Executar como Clássica</span><span class="sxs-lookup"><span data-stu-id="6d6a1-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="6d6a1-208">Executar um pequeno semelhante testar tooconfirm que você pode autenticar com êxito usando Olá nova clássico conta executar como.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="6d6a1-209">No portal do Azure de Olá, abra conta de automação de saudação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="6d6a1-210">Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="6d6a1-211">Selecione Olá **AzureClassicAutomationTutorialScript** runbook e, em seguida, clique em **iniciar** muito iniciar runbook hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="6d6a1-212">Olá eventos a seguir ocorre:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-212">hello following events occur:</span></span>

 * <span data-ttu-id="6d6a1-213">Um [trabalho de runbook](automation-runbook-execution.md) é criado, hello **trabalho** folha é exibida, e o status do trabalho Olá é exibido na Olá **resumo do trabalho** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="6d6a1-214">status do trabalho Olá começa como **na fila**, indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="6d6a1-215">o status de saudação se torna **iniciando** quando um trabalhador declarações trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="6d6a1-216">Olá status se torna **executando** quando Olá runbook é iniciado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="6d6a1-217">Quando a execução do trabalho de runbook Olá for concluída, você verá um status de **concluído**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Teste de runbook da entidade de segurança](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="6d6a1-219">toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="6d6a1-220">Olá **saída** folha é exibida, mostrando esse runbook Olá autenticado e retornou uma lista de todas as VMs clássicas na assinatura Olá com êxito.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="6d6a1-221">Olá fechar **saída** folha tooreturn toohello **resumo do trabalho** folha.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="6d6a1-222">Olá fechar **resumo do trabalho** folha e Olá correspondente **AzureAutomationTutorialScript** folha do runbook.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="6d6a1-223">Gerenciando a conta Executar como</span><span class="sxs-lookup"><span data-stu-id="6d6a1-223">Managing your Run As account</span></span>
<span data-ttu-id="6d6a1-224">Em algum momento antes de sua conta de automação expira, você precisará toorenew Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="6d6a1-225">Se você acredita que Olá conta executar como foi comprometida, você pode excluir e recriá-la.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="6d6a1-226">Esta seção discute como tooperform essas operações.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="6d6a1-227">Renovação do certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="6d6a1-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="6d6a1-228">Olá o certificado autoassinado que você criou para a conta executar como de saudação expira um ano da data de saudação da criação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="6d6a1-229">Você pode renová-lo a qualquer momento antes que ele expire.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="6d6a1-230">Quando você renová-la, o certificado de válido atual Olá é retido tooensure que todos os runbooks que são enfileiradas até ou ativamente em execução e que pode autenticar com hello conta executar como, não são afetados negativamente.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="6d6a1-231">certificado Olá permanece válido até a data de expiração.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="6d6a1-232">Se você tiver configurado seu toouse de conta executar como automação um certificado emitido por sua autoridade de certificação corporativa e você usar essa opção, o certificado corporativo de saudação será substituído por um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="6d6a1-233">Olá toorenew do certificado, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="6d6a1-234">No portal do Azure de Olá, abra conta de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="6d6a1-235">Em Olá **conta de automação** folha em Olá **propriedades de conta** painel, em **configurações de conta**, selecione **contas executar como**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Painel de propriedades da conta de Automação](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="6d6a1-237">Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou Olá clássico conta executar como que você deseja toorenew Olá certificado para.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="6d6a1-238">Em Olá **propriedades** folha para Olá selecionada conta, clique em **Renovar certificado**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Renovar o certificado da conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="6d6a1-240">Enquanto o certificado hello está sendo renovado, você pode acompanhar o progresso de saudação em **notificações** menu hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="6d6a1-241">Excluir uma conta Executar como ou Executar como Clássica</span><span class="sxs-lookup"><span data-stu-id="6d6a1-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="6d6a1-242">Esta seção descreve como toodelete e crie novamente uma conta executar como ou clássico executar como.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="6d6a1-243">Ao executar esta ação, Olá conta de automação é mantida.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="6d6a1-244">Depois de excluir uma conta executar como ou clássico executar como, você poderá recriá-la em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="6d6a1-245">No portal do Azure de Olá, abra conta de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="6d6a1-246">Em Olá **conta de automação** folha, no painel de propriedades da conta hello, selecione **contas executar como**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="6d6a1-247">Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou clássico executar como da conta que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="6d6a1-248">Em seguida, na Olá **propriedades** folha para Olá selecionada conta, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Excluir Conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="6d6a1-250">Enquanto a conta de hello está sendo excluída, você pode acompanhar o progresso de saudação em **notificações** menu hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="6d6a1-251">Após a exclusão de conta hello, você pode criá-lo novamente no hello **contas executar como** opção de criação de folha de propriedades selecionando Olá **Azure conta executar como**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Recriar Olá automação executar como conta](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="6d6a1-253">Configuração incorreta</span><span class="sxs-lookup"><span data-stu-id="6d6a1-253">Misconfiguration</span></span>
<span data-ttu-id="6d6a1-254">Alguns itens de configuração necessárias para toofunction de conta executar como ou clássico executar como Olá corretamente podem foram excluídos ou incorretamente criados durante a instalação inicial.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="6d6a1-255">Olá itens incluem:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-255">hello items include:</span></span>

* <span data-ttu-id="6d6a1-256">Ativo de certificado</span><span class="sxs-lookup"><span data-stu-id="6d6a1-256">Certificate asset</span></span>
* <span data-ttu-id="6d6a1-257">Ativo de conexão</span><span class="sxs-lookup"><span data-stu-id="6d6a1-257">Connection asset</span></span>
* <span data-ttu-id="6d6a1-258">Conta executar como foi removida da função de Colaborador Olá</span><span class="sxs-lookup"><span data-stu-id="6d6a1-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="6d6a1-259">Entidade de serviço ou aplicativo no Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d6a1-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="6d6a1-260">Olá anterior e outras instâncias de uma configuração incorreta, Olá conta de automação detecta Olá altera e exibe o status de *incompleta* em Olá **contas executar como** folha de propriedades para Olá conta.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Status incompleto de configuração de conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="6d6a1-262">Quando você selecionar a conta executar como do hello, Olá conta **propriedades** painel exibe o saudação a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Mensagem de aviso incompleto da configuração da conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="6d6a1-264">.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-264">.</span></span>

<span data-ttu-id="6d6a1-265">Rapidamente, você pode resolver esses problemas de conta executar como, excluindo e recriando conta hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="6d6a1-266">Atualizar sua conta de Automação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d6a1-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="6d6a1-267">Você pode usar sua conta de automação existente de PowerShell tooupdate se:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="6d6a1-268">Criar uma conta de automação, mas recusar toocreate Olá executar como conta.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="6d6a1-269">Você já usa uma recursos de Gerenciador de recursos de toomanage de conta de automação e deseja tooupdate Olá tooinclude Olá executar como conta para autenticação de runbook.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="6d6a1-270">Você já usa uma automação conta toomanage os recursos clássicos e você deseja tooupdate-Olá toouse clássico executar como conta em vez de criar uma nova conta e migrar seu tooit runbooks e ativos.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="6d6a1-271">Você quer toocreate executar como e uma conta clássico executar como usando um certificado emitido por sua autoridade de certificação (CA).</span><span class="sxs-lookup"><span data-stu-id="6d6a1-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="6d6a1-272">script Hello tem Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="6d6a1-273">script Hello pode ser executado somente no Windows 10 e Windows Server 2016 com módulos do Azure Resource Manager 2.01 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="6d6a1-274">Não há suporte nas versões anteriores do Windows.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="6d6a1-275">Azure PowerShell 1.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="6d6a1-276">Para obter informações sobre versão Olá PowerShell 1.0, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d6a1-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="6d6a1-277">Uma conta de automação, que é referenciada como valor Olá Olá *– AutomationAccountName* e *- ApplicationDisplayName* parâmetros em Olá script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="6d6a1-278">Olá tooget valores para *SubscriptionID*, *ResourceGroup*, e *AutomationAccountName*, que são parâmetros obrigatórios para scripts hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="6d6a1-279">No hello portal do Azure, selecione sua conta de automação Olá **conta de automação** folha e, em seguida, selecione **todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="6d6a1-280">Em Olá **todas as configurações** folha, em **configurações de conta**, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="6d6a1-281">Observe os valores hello Olá **propriedades** folha.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-281">Note hello values on hello **Properties** blade.</span></span>

![folha de "Propriedades" Hello automação conta](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="6d6a1-283">Criar o script do PowerShell da conta Executar como</span><span class="sxs-lookup"><span data-stu-id="6d6a1-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="6d6a1-284">Este script do PowerShell inclui suporte para Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="6d6a1-285">Crie uma conta Executar como usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="6d6a1-286">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="6d6a1-287">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="6d6a1-288">Crie uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem do Azure governamental.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="6d6a1-289">Dependendo da opção de configuração de saudação que selecionar script hello cria Olá itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="6d6a1-290">**Para contas Executar como:**</span><span class="sxs-lookup"><span data-stu-id="6d6a1-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="6d6a1-291">Cria um Azure AD aplicativo toobe exportado com a saudação autoassinada ou chave pública do certificado da empresa, cria uma conta de serviço principal para o aplicativo hello no AD do Azure e atribui Olá função Colaborador para conta Olá no seu atual assinatura.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="6d6a1-292">Você pode alterar essa configuração tooOwner ou qualquer outra função.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="6d6a1-293">Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="6d6a1-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="6d6a1-294">Cria um ativo de certificado de automação chamado *AzureRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="6d6a1-295">ativo de certificado Olá mantém Olá chave privada do certificado que é usado pelo aplicativo hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="6d6a1-296">Cria um ativo de conexão de automação chamado *AzureRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="6d6a1-297">ativo de conexão Olá mantém applicationId hello, tenantId, subscriptionId e a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="6d6a1-298">**Para contas Executar como clássicas:**</span><span class="sxs-lookup"><span data-stu-id="6d6a1-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="6d6a1-299">Cria um ativo de certificado de automação chamado *AzureClassicRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="6d6a1-300">ativo de certificado Olá mantém a chave privada do certificado Olá usado pelo certificado de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="6d6a1-301">Cria um ativo de conexão de automação chamado *AzureClassicRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="6d6a1-302">ativo de conexão Olá contém o nome da assinatura hello, subscriptionId e nome do ativo de certificado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="6d6a1-303">Se você selecionar a opção para criar uma conta clássico executar como, após a execução do script hello, carregamento Olá pública repositório de certificados gerenciamento de toohello (extensão de nome de arquivo. cer) para a assinatura de saudação que Olá conta de automação foi criado no.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="6d6a1-304">tooexecute Olá scripts e carregar certificado hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="6d6a1-305">Salve Olá script a seguir em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-305">Save hello following script on your computer.</span></span> <span data-ttu-id="6d6a1-306">Neste exemplo, salve-o com o nome de arquivo hello *RunAsAccount.ps1 novo*.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="6d6a1-307">No computador, clique em **Iniciar** e inicie o **Windows PowerShell** com direitos de usuário elevados.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="6d6a1-308">De saudação elevado shell de linha de comando do PowerShell, vá toohello pasta que contém o script hello criado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="6d6a1-309">Execute script hello usando valores de parâmetro de saudação para configuração Olá que precisar.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="6d6a1-310">**Criar uma conta Executar como usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="6d6a1-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="6d6a1-311">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="6d6a1-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="6d6a1-312">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo**</span><span class="sxs-lookup"><span data-stu-id="6d6a1-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="6d6a1-313">**Criar uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem Azure Government**</span><span class="sxs-lookup"><span data-stu-id="6d6a1-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="6d6a1-314">Depois que o script hello executado, será tooauthenticate solicitado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="6d6a1-315">Entrar com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="6d6a1-316">Depois que o script hello foi executada com êxito, observe o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="6d6a1-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="6d6a1-317">Se você criou uma conta clássico executar como com um certificado autoassinado público (arquivo. cer), script hello cria e salva-a pasta de arquivos temporários toohello no computador em que o perfil de usuário Olá *%USERPROFILE%\AppData\Local\Temp*, que você usou a sessão do PowerShell Olá tooexecute.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="6d6a1-318">Se tiver criado uma conta Executar como Clássica com um certificado público corporativo (arquivo .cer), use este certificado.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="6d6a1-319">Siga as instruções de saudação de [carregar um certificado de API de gerenciamento toohello portal clássico do Azure](../azure-api-management-certs.md)e, em seguida, validar a configuração de credencial de saudação com recursos de gerenciamento de serviço usando Olá [código de exemplo tooauthenticate com recursos de gerenciamento do serviço](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="6d6a1-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="6d6a1-320">Se você fez *não* criar uma conta clássico executar como, autenticar com recursos de Gerenciador de recursos e validar a configuração de credencial de saudação usando Olá [código para autenticar com o serviço de gerenciamento de exemplo recursos](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="6d6a1-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="6d6a1-321">Tooauthenticate de código de exemplo com os recursos do Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="6d6a1-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="6d6a1-322">Você pode usar o seguinte Olá atualizado código de exemplo, obtido Olá *AzureAutomationTutorialScript* exemplo de runbook, tooauthenticate usando Olá executar como conta toomanage Gerenciador de recursos recursos com seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="6d6a1-323">toohelp você tooeasily de trabalho entre várias assinaturas, o script hello inclui duas linhas de código adicionais que dão suporte ao fazer referência a um contexto de assinatura.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="6d6a1-324">Um ativo variável denominado *SubscriptionId* contém Olá ID de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="6d6a1-325">Depois de saudação `Add-AzureRmAccount` cmdlet instrução, Olá [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet é declarado com o conjunto de parâmetros de saudação *- SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="6d6a1-326">Se o nome da variável Olá é muito genérico, você pode revisá-lo tooinclude um prefixo ou usar outro toomake de convenção de nomenclatura-tooidentify mais fácil.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="6d6a1-327">Como alternativa, você pode usar o conjunto de parâmetros de saudação *- SubscriptionName* em vez de *- SubscriptionId* com um ativo de variável correspondente.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="6d6a1-328">Olá cmdlet que você pode usar para autenticar no runbook hello, `Add-AzureRmAccount`, Olá usa *ServicePrincipalCertificate* conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="6d6a1-329">Ele autentica usando Olá serviço certificado principal, não as credenciais do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="6d6a1-330">Tooauthenticate de código de exemplo com os recursos de gerenciamento de serviço</span><span class="sxs-lookup"><span data-stu-id="6d6a1-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="6d6a1-331">Você pode usar o hello após o código de exemplo atualizado, o que é obtido da saudação *AzureClassicAutomationTutorialScript* exemplo de runbook, tooauthenticate usando Olá clássico conta executar como toomanage recursos clássicos com seu runbooks.</span><span class="sxs-lookup"><span data-stu-id="6d6a1-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="6d6a1-332">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d6a1-332">Next steps</span></span>
* [<span data-ttu-id="6d6a1-333">Objetos de aplicativo e entidade de serviço no Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d6a1-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="6d6a1-334">Controle de acesso com base em função na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="6d6a1-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="6d6a1-335">Visão geral sobre certificados para os Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="6d6a1-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
