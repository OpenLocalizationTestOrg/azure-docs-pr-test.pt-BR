---
title: "contas de automação executar como do Azure aaaCreate | Microsoft Docs"
description: "Este artigo descreve como tooupdate à automação da conta e criar contas executar como com o PowerShell ou do portal de saudação."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="bba43-103">Atualizar a autenticação de conta de Automação com contas Executar como</span><span class="sxs-lookup"><span data-stu-id="bba43-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="bba43-104">Você pode atualizar sua conta de automação existente do portal de saudação ou usar o PowerShell se:</span><span class="sxs-lookup"><span data-stu-id="bba43-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="bba43-105">Criar uma conta de automação, mas recusar toocreate Olá executar como conta.</span><span class="sxs-lookup"><span data-stu-id="bba43-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="bba43-106">Você já usa uma recursos de Gerenciador de recursos de toomanage de conta de automação e deseja tooupdate Olá tooinclude Olá executar como conta para autenticação de runbook.</span><span class="sxs-lookup"><span data-stu-id="bba43-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="bba43-107">Você já usa uma automação conta toomanage os recursos clássicos e você deseja tooupdate-Olá toouse clássico executar como conta em vez de criar uma nova conta e migrar seu tooit runbooks e ativos.</span><span class="sxs-lookup"><span data-stu-id="bba43-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="bba43-108">Você quer toocreate executar como e uma conta clássico executar como usando um certificado emitido por sua autoridade de certificação (CA).</span><span class="sxs-lookup"><span data-stu-id="bba43-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bba43-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bba43-109">Prerequisites</span></span>

* <span data-ttu-id="bba43-110">script Hello pode ser executada somente no Windows 10 e Windows Server 2016 com módulos do Azure Resource Manager 3.0.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="bba43-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="bba43-111">Não há suporte nas versões anteriores do Windows.</span><span class="sxs-lookup"><span data-stu-id="bba43-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="bba43-112">Azure PowerShell 1.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="bba43-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="bba43-113">Para obter informações sobre versão Olá PowerShell 1.0, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="bba43-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="bba43-114">Uma conta de automação, que é referenciada como valor Olá Olá *– AutomationAccountName* e *- ApplicationDisplayName* parâmetros em Olá script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="bba43-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="bba43-115">Olá tooget valores para *SubscriptionID*, *ResourceGroup*, e *AutomationAccountName*, que são parâmetros obrigatórios para o script hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bba43-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="bba43-116">No hello portal do Azure, selecione sua conta de automação Olá **conta de automação** folha e, em seguida, selecione **todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="bba43-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="bba43-117">Em Olá **todas as configurações** folha, em **configurações de conta**, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="bba43-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="bba43-118">Observe os valores hello Olá **propriedades** folha.</span><span class="sxs-lookup"><span data-stu-id="bba43-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="bba43-119">![folha de "Propriedades" Hello automação conta](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="bba43-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="bba43-120">Necessário tooupdate permissões de sua conta de automação</span><span class="sxs-lookup"><span data-stu-id="bba43-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="bba43-121">tooupdate uma conta de automação, você deve ter Olá privilégios específicos a seguir e as permissões necessárias toocomplete neste tópico.</span><span class="sxs-lookup"><span data-stu-id="bba43-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="bba43-122">Sua conta de usuário do AD precisa toobe tooa adicionado função com a função de Colaborador de toohello equivalente de permissões para recursos do Microsoft conforme descrito no artigo [controle de acesso baseado em função no Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="bba43-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="bba43-123">Usuários não administrativos em seu locatário do AD do Azure podem [registrar aplicativos AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se registros do aplicativo hello configuração está definido muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="bba43-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="bba43-124">Se os registros do aplicativo hello configuração está definido muito**não**, usuário Olá executar essa ação deve ser um administrador global no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba43-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="bba43-125">Se você não for um membro da instância do Active Directory da assinatura Olá antes que sejam adicionadas toohello administrador/coadministrador função global da assinatura hello, são adicionados o tooActive diretório como convidado.</span><span class="sxs-lookup"><span data-stu-id="bba43-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="bba43-126">Nessa situação, você receberá um "você não tem permissões toocreate..."</span><span class="sxs-lookup"><span data-stu-id="bba43-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="bba43-127">saudação de aviso **adicionar conta de automação** folha.</span><span class="sxs-lookup"><span data-stu-id="bba43-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="bba43-128">Os usuários que foram adicionados toohello administrador/coadministrador função global primeiro pode ser removida da instância do Active Directory da assinatura hello e adicionado novamente toomake-los como um usuário completo no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bba43-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="bba43-129">tooverify nesta situação, do hello **Active Directory do Azure** painel Olá portal do Azure, selecione **usuários e grupos**, selecione **todos os usuários** e, depois de selecionar Olá usuário específico, selecione **perfil**.</span><span class="sxs-lookup"><span data-stu-id="bba43-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="bba43-130">Olá valor Olá **o tipo de usuário** atributo sob o perfil de usuários Olá não deve ser iguais **convidado**.</span><span class="sxs-lookup"><span data-stu-id="bba43-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="bba43-131">Criar conta executar como do portal de saudação</span><span class="sxs-lookup"><span data-stu-id="bba43-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="bba43-132">Nesta seção, execute Olá tooupdate as etapas a seguir sua conta de automação do Azure da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba43-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="bba43-133">Você cria Olá contas executar como e clássico executar como individualmente, e se não precisar de recursos toomanage no portal do Azure clássico de hello, assim você pode criar conta executar como do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba43-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="bba43-134">processo de saudação cria Olá itens a seguir na sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="bba43-135">**Para contas Executar como:**</span><span class="sxs-lookup"><span data-stu-id="bba43-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="bba43-136">Cria um aplicativo do AD do Azure com um certificado autoassinado, cria uma conta de serviço principal para o aplicativo hello no AD do Azure e atribui a função de Colaborador de saudação para conta de saudação em sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="bba43-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="bba43-137">Você pode alterar essa configuração tooOwner ou qualquer outra função.</span><span class="sxs-lookup"><span data-stu-id="bba43-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="bba43-138">Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="bba43-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="bba43-139">Cria um ativo de certificado de automação chamado *AzureRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-140">ativo de certificado Olá mantém Olá chave privada do certificado que é usado pelo aplicativo hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba43-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="bba43-141">Cria um ativo de conexão de automação chamado *AzureRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-142">ativo de conexão Olá mantém applicationId hello, tenantId, subscriptionId e a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="bba43-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="bba43-143">**Para contas Executar como clássicas:**</span><span class="sxs-lookup"><span data-stu-id="bba43-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="bba43-144">Cria um ativo de certificado de automação chamado *AzureClassicRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-145">ativo de certificado Olá mantém a chave privada do certificado Olá usado pelo certificado de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba43-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="bba43-146">Cria um ativo de conexão de automação chamado *AzureClassicRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-147">ativo de conexão Olá contém o nome da assinatura hello, subscriptionId e nome do ativo de certificado.</span><span class="sxs-lookup"><span data-stu-id="bba43-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="bba43-148">Entrar toohello portal do Azure com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba43-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="bba43-149">Na folha de conta de automação hello, selecione **contas executar como** na seção Olá **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="bba43-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="bba43-150">Dependendo da conta de que você precisa, selecione **Conta Executar como do Azure** ou **Conta Executar como Clássica do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bba43-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="bba43-151">Depois de selecionar qualquer Olá **adicionar executar como do Azure** ou **adicionar Azure clássico conta executar como** lâmina aparece e depois de revisar as informações de visão geral de saudação, clique em **criar** tooproceed com a criação da conta executar como.</span><span class="sxs-lookup"><span data-stu-id="bba43-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="bba43-152">Enquanto o Azure cria uma conta executar como do hello, você pode acompanhar o progresso de saudação em **notificações** de saudação menu e uma faixa é exibida informando Olá conta está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="bba43-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="bba43-153">Esse processo pode levar alguns toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="bba43-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="bba43-154">Criar conta Executar como usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="bba43-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="bba43-155">Este script do PowerShell inclui suporte para Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="bba43-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="bba43-156">Crie uma conta Executar como usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="bba43-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="bba43-157">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="bba43-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="bba43-158">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo.</span><span class="sxs-lookup"><span data-stu-id="bba43-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="bba43-159">Crie uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem do Azure governamental.</span><span class="sxs-lookup"><span data-stu-id="bba43-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="bba43-160">Dependendo da opção de configuração de saudação que selecionar script hello cria Olá itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="bba43-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="bba43-161">**Para contas Executar como:**</span><span class="sxs-lookup"><span data-stu-id="bba43-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="bba43-162">Cria um Azure AD aplicativo toobe exportado com a saudação autoassinada ou chave pública do certificado da empresa, cria uma conta de serviço principal para o aplicativo hello no AD do Azure e atribui Olá função Colaborador para conta Olá no seu atual assinatura.</span><span class="sxs-lookup"><span data-stu-id="bba43-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="bba43-163">Você pode alterar essa configuração tooOwner ou qualquer outra função.</span><span class="sxs-lookup"><span data-stu-id="bba43-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="bba43-164">Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="bba43-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="bba43-165">Cria um ativo de certificado de automação chamado *AzureRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-166">ativo de certificado Olá mantém Olá chave privada do certificado que é usado pelo aplicativo hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba43-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="bba43-167">Cria um ativo de conexão de automação chamado *AzureRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-168">ativo de conexão Olá mantém applicationId hello, tenantId, subscriptionId e a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="bba43-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="bba43-169">**Para contas Executar como clássicas:**</span><span class="sxs-lookup"><span data-stu-id="bba43-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="bba43-170">Cria um ativo de certificado de automação chamado *AzureClassicRunAsCertificate* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-171">ativo de certificado Olá mantém a chave privada do certificado Olá usado pelo certificado de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba43-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="bba43-172">Cria um ativo de conexão de automação chamado *AzureClassicRunAsConnection* em Olá especificado na conta de automação.</span><span class="sxs-lookup"><span data-stu-id="bba43-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="bba43-173">ativo de conexão Olá contém o nome da assinatura hello, subscriptionId e nome do ativo de certificado.</span><span class="sxs-lookup"><span data-stu-id="bba43-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="bba43-174">Se você selecionar a opção para criar uma conta clássico executar como, após a execução do script hello, carregamento Olá pública repositório de certificados gerenciamento de toohello (extensão de nome de arquivo. cer) para a assinatura de saudação que Olá conta de automação foi criado no.</span><span class="sxs-lookup"><span data-stu-id="bba43-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="bba43-175">Salve Olá script a seguir em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bba43-175">Save hello following script on your computer.</span></span> <span data-ttu-id="bba43-176">Neste exemplo, salve-o com o nome de arquivo hello *RunAsAccount.ps1 novo*.</span><span class="sxs-lookup"><span data-stu-id="bba43-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="bba43-177">Em seu computador, inicie **do Windows PowerShell** de saudação **iniciar** tela com direitos de usuário elevados.</span><span class="sxs-lookup"><span data-stu-id="bba43-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="bba43-178">De saudação elevado shell de linha de comando, vá toohello pasta que contém o script hello criado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="bba43-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="bba43-179">Execute script hello usando valores de parâmetro de saudação para configuração Olá que precisar.</span><span class="sxs-lookup"><span data-stu-id="bba43-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="bba43-180">**Criar uma conta Executar como usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="bba43-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="bba43-181">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="bba43-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="bba43-182">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo**</span><span class="sxs-lookup"><span data-stu-id="bba43-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="bba43-183">**Criar uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem Azure Government**</span><span class="sxs-lookup"><span data-stu-id="bba43-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="bba43-184">Depois que o script hello executado, será tooauthenticate solicitado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="bba43-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="bba43-185">Entrar com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba43-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="bba43-186">Depois que o script hello foi executada com êxito, observe o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="bba43-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="bba43-187">Se você criou uma conta clássico executar como com um certificado autoassinado público (arquivo. cer), script hello cria e salva-a pasta de arquivos temporários toohello no computador em que o perfil de usuário Olá *%USERPROFILE%\AppData\Local\Temp*, que você usou a sessão do PowerShell Olá tooexecute.</span><span class="sxs-lookup"><span data-stu-id="bba43-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="bba43-188">Se tiver criado uma conta Executar como Clássica com um certificado público corporativo (arquivo .cer), use este certificado.</span><span class="sxs-lookup"><span data-stu-id="bba43-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="bba43-189">Siga as instruções de saudação de [carregar um certificado de API de gerenciamento toohello portal clássico do Azure](../azure-api-management-certs.md)e, em seguida, validar a configuração de credencial de saudação com recursos de implantação clássico usando Olá [código de exemplo tooauthenticate com recursos de implantação clássico do Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="bba43-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="bba43-190">Se você fez *não* criar uma conta clássico executar como, autenticar com recursos de Gerenciador de recursos e validar a configuração de credencial de saudação usando Olá [código para autenticar com o serviço de gerenciamento de exemplo recursos](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="bba43-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bba43-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bba43-191">Next steps</span></span>
* <span data-ttu-id="bba43-192">Para obter mais informações sobre entidades de serviço, consulte muito[objetos Application e entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="bba43-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="bba43-193">Para obter mais informações sobre certificados e serviços do Azure, consulte muito[visão geral de certificados para serviços de nuvem do Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="bba43-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
