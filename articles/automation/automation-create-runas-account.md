---
title: "Criar contas Executar como da Automação do Azure | Microsoft Docs"
description: "Este artigo descreve como atualizar sua conta de Automação e criar contas Executar como com o PowerShell ou a partir do portal."
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
ms.openlocfilehash: eaf6eb49bbfe4572827fcc101d1f552b48ab91e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="7c443-103">Atualizar a autenticação de conta de Automação com contas Executar como</span><span class="sxs-lookup"><span data-stu-id="7c443-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="7c443-104">Você pode atualizar sua conta de Automação existente no portal ou usando o PowerShell se:</span><span class="sxs-lookup"><span data-stu-id="7c443-104">You can update your existing Automation account from the portal or use PowerShell if:</span></span>

* <span data-ttu-id="7c443-105">Você criar uma conta de Automação, mas se recusar a criar a conta Executar como.</span><span class="sxs-lookup"><span data-stu-id="7c443-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="7c443-106">Você já usa uma conta de Automação para gerenciar recursos do Resource Manager e quer atualizá-la para incluir a conta Executar como para autenticação de runbook.</span><span class="sxs-lookup"><span data-stu-id="7c443-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="7c443-107">Você já usar uma conta de Automação para gerenciar os recursos clássicos e quiser atualizá-la para usar a conta Executar como Clássica em vez de criar uma nova conta e migrar seus runbooks e ativos para ela.</span><span class="sxs-lookup"><span data-stu-id="7c443-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="7c443-108">Você quiser criar uma conta Executar como e uma conta Clássica Executar como usando um certificado emitido por sua CA (Autoridade de Certificação).</span><span class="sxs-lookup"><span data-stu-id="7c443-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c443-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c443-109">Prerequisites</span></span>

* <span data-ttu-id="7c443-110">O script só pode ser executado no Windows 10 e no Windows Server 2016 com módulos do Azure Resource Manager 3.0.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="7c443-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="7c443-111">Não há suporte nas versões anteriores do Windows.</span><span class="sxs-lookup"><span data-stu-id="7c443-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="7c443-112">Azure PowerShell 1.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="7c443-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="7c443-113">Para obter informações sobre a versão 1.0 do PowerShell, confira [Como instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="7c443-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="7c443-114">Uma conta de Automação, que é referenciada como o valor para os parâmetros *–AutomationAccountName* e *-pplicationDisplayName* no script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="7c443-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="7c443-115">Para obter os valores para *SubscriptionID*, *ResourceGroup* e *AutomationAccountName*, que são parâmetros obrigatórios para o script, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7c443-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="7c443-116">No portal do Azure, selecione a conta de Automação na folha **Conta de Automação** e selecione **Todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="7c443-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="7c443-117">Na folha **Todas as configurações**, em **Configurações de Conta**, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="7c443-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="7c443-118">Observe os valores na folha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="7c443-118">Note the values on the **Properties** blade.</span></span><br><br> <span data-ttu-id="7c443-119">![A folha "Propriedades" da conta de Automação](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="7c443-119">![The Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-to-update-your-automation-account"></a><span data-ttu-id="7c443-120">Permissões necessárias para atualizar sua conta da Automação</span><span class="sxs-lookup"><span data-stu-id="7c443-120">Required permissions to update your Automation account</span></span>
<span data-ttu-id="7c443-121">Para atualizar uma conta da Automação, você deve ter os seguintes privilégios e permissões específicas necessárias para concluir este tópico.</span><span class="sxs-lookup"><span data-stu-id="7c443-121">To update an Automation account, you must have the following specific privileges and permissions required to complete this topic.</span></span>   
 
* <span data-ttu-id="7c443-122">Sua conta de usuário do AD precisa ser adicionada a uma função com permissões equivalentes à função de Colaborador para recursos Microsoft.Automation conforme descrito no artigo [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="7c443-122">Your AD user account needs to be added to a role with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="7c443-123">Usuários não administrativos em seu locatário do Azure AD podem [registrar aplicativos AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se os registros do aplicativo configuração estão definidos como **Sim**.</span><span class="sxs-lookup"><span data-stu-id="7c443-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the App registrations setting is set to **Yes**.</span></span>  <span data-ttu-id="7c443-124">Se a configuração de registros do aplicativo estiver definido como **Não**, o usuário que executa esta ação deverá ser um administrador global no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c443-124">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="7c443-125">Caso não seja membro da instância do Active Directory da assinatura antes de ser adicionados à função de administrador global/coadministrador da assinatura, você será adicionado ao Active Directory como convidado.</span><span class="sxs-lookup"><span data-stu-id="7c443-125">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="7c443-126">Nesse caso, você receberá um aviso "Você não tem permissões para criar..."</span><span class="sxs-lookup"><span data-stu-id="7c443-126">In this situation, you receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="7c443-127">na folha **Adicionar Conta de Automação**.</span><span class="sxs-lookup"><span data-stu-id="7c443-127">warning on the **Add Automation Account** blade.</span></span> <span data-ttu-id="7c443-128">Os usuários adicionados à função de administrador global/coadministrador primeiro podem ser removidos das assinaturas da instância do Active Directory e adicionados novamente para torná-los Usuários completos no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c443-128">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="7c443-129">Para verificar essa situação, no painel **Azure Active Directory** no portal do Azure, selecione **Usuários e grupos**, selecione **Todos os usuários** e, depois de selecionar o usuário específico, selecione **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="7c443-129">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="7c443-130">O valor do atributo **Tipo de usuário** sob o perfil de usuários não deve ser igual a **Convidado**.</span><span class="sxs-lookup"><span data-stu-id="7c443-130">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-the-portal"></a><span data-ttu-id="7c443-131">Criar a conta Executar como no portal</span><span class="sxs-lookup"><span data-stu-id="7c443-131">Create Run As account from the portal</span></span>
<span data-ttu-id="7c443-132">Nesta seção, execute as seguintes etapas para atualizar sua conta de automação do Azure no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c443-132">In this section, perform the following steps to update your Azure Automation account from  the Azure portal.</span></span>  <span data-ttu-id="7c443-133">Você cria as contas Executar como e Executar como Clássica individualmente, e se não precisar gerenciar recursos no portal clássico do Azure, poderá criar apenas a conta Executar como do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c443-133">You create the Run As and Classic Run As accounts individually, and if you don't need to manage resources in the classic Azure portal, you can just create the Azure Run As account.</span></span>  

<span data-ttu-id="7c443-134">O processo cria os seguintes itens na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="7c443-134">The process creates the following items in your Automation account.</span></span>

<span data-ttu-id="7c443-135">**Para contas Executar como:**</span><span class="sxs-lookup"><span data-stu-id="7c443-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="7c443-136">Cria um aplicativo do Azure AD com um certificado autoassinado, cria uma conta de entidade de serviço para o aplicativo no Azure AD e atribui a função de Colaborador à conta na assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="7c443-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="7c443-137">Você pode alterar essa configuração para Proprietário ou qualquer outra função.</span><span class="sxs-lookup"><span data-stu-id="7c443-137">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="7c443-138">Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7c443-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="7c443-139">Cria um ativo de certificado de Automação chamado *AzureRunAsCertificate* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="7c443-140">O ativo de certificado contém a chave privada do certificado que é usada pelo aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c443-140">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="7c443-141">Cria um ativo de conexão de Automação chamado *AzureRunAsConnection* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-141">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="7c443-142">O ativo de conexão contém applicationId, tenantId, subscriptionId e a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="7c443-142">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="7c443-143">**Para contas Executar como clássicas:**</span><span class="sxs-lookup"><span data-stu-id="7c443-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="7c443-144">Cria um ativo de certificado de Automação chamado *AzureClassicRunAsCertificate* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="7c443-145">O ativo de certificado contém a chave privada do certificado usada pelo certificado de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="7c443-145">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="7c443-146">Cria um ativo de conexão de Automação chamado *AzureClassicRunAsConnection* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="7c443-147">O ativo de conexão contém o nome da assinatura, subscriptionId e o nome do ativo de certificado.</span><span class="sxs-lookup"><span data-stu-id="7c443-147">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="7c443-148">Conecte-se no Portal do Azure com uma conta que seja membro da função Administradores da Assinatura e coadministradora da assinatura.</span><span class="sxs-lookup"><span data-stu-id="7c443-148">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
2. <span data-ttu-id="7c443-149">Na folha da conta de Automação, selecione **Contas Executar como** na seção **Configurações de Conta**.</span><span class="sxs-lookup"><span data-stu-id="7c443-149">From the Automation account blade, select **Run As Accounts** under the section **Account Settings**.</span></span>  
3. <span data-ttu-id="7c443-150">Dependendo da conta de que você precisa, selecione **Conta Executar como do Azure** ou **Conta Executar como Clássica do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7c443-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="7c443-151">Após a seleção, a folha **Adicionar Executar como do Azure** ou a folha **Adicionar Conta Executar como Clássica do Azure** aparecerá e após a revisão das informações de visão geral, clique em **Criar** para prosseguir com a criação da conta Executar como.</span><span class="sxs-lookup"><span data-stu-id="7c443-151">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
4. <span data-ttu-id="7c443-152">Enquanto o Azure cria a conta Executar como, você pode acompanhar o progresso em **Notificações** no menu e uma faixa é exibida informando que a conta está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="7c443-152">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu and a banner is displayed stating the account is being created.</span></span>  <span data-ttu-id="7c443-153">A conclusão desse processo pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="7c443-153">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="7c443-154">Criar conta Executar como usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c443-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="7c443-155">Este script do PowerShell inclui suporte para as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="7c443-155">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="7c443-156">Crie uma conta Executar como usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="7c443-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="7c443-157">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="7c443-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="7c443-158">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo.</span><span class="sxs-lookup"><span data-stu-id="7c443-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="7c443-159">Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado na nuvem do Azure Governamental.</span><span class="sxs-lookup"><span data-stu-id="7c443-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="7c443-160">Dependendo da opção de configuração que você selecionar, o script criará os itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="7c443-160">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="7c443-161">**Para contas Executar como:**</span><span class="sxs-lookup"><span data-stu-id="7c443-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="7c443-162">Cria um aplicativo do Azure AD para ser exportado com a chave pública autoassinada ou de certificado corporativo ou cria uma conta de entidade de serviço para o aplicativo no Azure AD e atribui a função de Colaborador à conta na assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="7c443-162">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="7c443-163">Você pode alterar essa configuração para Proprietário ou qualquer outra função.</span><span class="sxs-lookup"><span data-stu-id="7c443-163">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="7c443-164">Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7c443-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="7c443-165">Cria um ativo de certificado de Automação chamado *AzureRunAsCertificate* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="7c443-166">O ativo de certificado contém a chave privada do certificado que é usada pelo aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c443-166">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="7c443-167">Cria um ativo de conexão de Automação chamado *AzureRunAsConnection* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-167">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="7c443-168">O ativo de conexão contém applicationId, tenantId, subscriptionId e a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="7c443-168">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="7c443-169">**Para contas Executar como clássicas:**</span><span class="sxs-lookup"><span data-stu-id="7c443-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="7c443-170">Cria um ativo de certificado de Automação chamado *AzureClassicRunAsCertificate* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="7c443-171">O ativo de certificado contém a chave privada do certificado usada pelo certificado de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="7c443-171">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="7c443-172">Cria um ativo de conexão de Automação chamado *AzureClassicRunAsConnection* na conta de Automação especificada.</span><span class="sxs-lookup"><span data-stu-id="7c443-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="7c443-173">O ativo de conexão contém o nome da assinatura, subscriptionId e o nome do ativo de certificado.</span><span class="sxs-lookup"><span data-stu-id="7c443-173">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="7c443-174">Se selecionar a opção para criar uma conta Executar como Clássica, depois que o script for executado, carregue o certificado público (extensão de nome de arquivo .cer) para o repositório de gerenciamento da assinatura em que a conta de Automação foi criada.</span><span class="sxs-lookup"><span data-stu-id="7c443-174">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="7c443-175">Salve o script a seguir em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7c443-175">Save the following script on your computer.</span></span> <span data-ttu-id="7c443-176">Neste exemplo, salve-o com o nome de arquivo *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="7c443-176">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
            Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                     "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="7c443-177">Em sua máquina, inicie o **Windows PowerShell** na tela **Iniciar** com direitos de usuário elevados.</span><span class="sxs-lookup"><span data-stu-id="7c443-177">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="7c443-178">A partir do shell da linha de comando com privilégios elevados, acesse a pasta que contém o script que você criou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="7c443-178">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="7c443-179">Execute o script usando os valores de parâmetro para a configuração necessária.</span><span class="sxs-lookup"><span data-stu-id="7c443-179">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="7c443-180">**Criar uma conta Executar como usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="7c443-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="7c443-181">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado**</span><span class="sxs-lookup"><span data-stu-id="7c443-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="7c443-182">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo**</span><span class="sxs-lookup"><span data-stu-id="7c443-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="7c443-183">**Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado na nuvem do Azure Governamental**</span><span class="sxs-lookup"><span data-stu-id="7c443-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="7c443-184">Depois que o script for executado, você deverá se autenticar no Azure.</span><span class="sxs-lookup"><span data-stu-id="7c443-184">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="7c443-185">Ente com uma conta que seja membro da função de administradores de assinatura e coadministrador da assinatura.</span><span class="sxs-lookup"><span data-stu-id="7c443-185">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="7c443-186">Depois que o script for executado com êxito, observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7c443-186">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="7c443-187">Se você tiver criado uma conta Executar como Clássica com um certificado autoassinado público (arquivo .cer), o script a criará e salvará na pasta de arquivos temporários no computador sob o perfil de usuário *%USERPROFILE%\AppData\Local\Temp*, que é usado para executar a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c443-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="7c443-188">Se tiver criado uma conta Executar como Clássica com um certificado público corporativo (arquivo .cer), use este certificado.</span><span class="sxs-lookup"><span data-stu-id="7c443-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="7c443-189">Siga as instruções para [carregar um certificado de API de gerenciamento no portal clássico do Azure](../azure-api-management-certs.md) e, então, valide a configuração de credencial com recursos de implantação clássicos usando o [código de exemplo para se autenticar com os Recursos de implantação clássica do Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="7c443-189">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="7c443-190">Se *não* criou uma conta Executar como Clássica, autentique-se com os recursos do Resource Manager e valide a configuração de credenciais usando o [código de exemplo para autenticação com recursos de Gerenciamento de Serviços](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="7c443-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c443-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c443-191">Next steps</span></span>
* <span data-ttu-id="7c443-192">Para saber mais sobre Entidades de Serviço, veja [Objetos de aplicativo e objetos de entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="7c443-192">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="7c443-193">Para saber mais sobre certificados e serviços do Azure, confira [Visão geral dos certificados de serviços de nuvem do Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="7c443-193">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>