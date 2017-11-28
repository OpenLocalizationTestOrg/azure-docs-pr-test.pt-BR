---
title: "aaaManage conta de automação do Azure | Microsoft Docs"
description: "Este artigo descreve como toomanage Olá a configuração de sua conta de automação, como uma configuração incorreta, a exclusão e a renovação de certificados."
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
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="e673e-103">Como gerenciar uma conta de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="e673e-103">Manage Azure Automation account</span></span>
<span data-ttu-id="e673e-104">Em algum momento antes de sua conta de automação expira, você precisará toorenew Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="e673e-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="e673e-105">Se você acredita que Olá conta executar como foi comprometida, você pode excluir e recriá-la.</span><span class="sxs-lookup"><span data-stu-id="e673e-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="e673e-106">Esta seção discute como tooperform essas operações.</span><span class="sxs-lookup"><span data-stu-id="e673e-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="e673e-107">Renovação do certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="e673e-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="e673e-108">Olá o certificado autoassinado que você criou para a conta executar como de saudação expira um ano da data de saudação da criação.</span><span class="sxs-lookup"><span data-stu-id="e673e-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="e673e-109">Você pode renová-lo a qualquer momento antes que ele expire.</span><span class="sxs-lookup"><span data-stu-id="e673e-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="e673e-110">Quando você renová-la, o certificado de válido atual Olá é retido tooensure que todos os runbooks que são enfileiradas até ou ativamente em execução e que pode autenticar com hello conta executar como, não são afetados negativamente.</span><span class="sxs-lookup"><span data-stu-id="e673e-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="e673e-111">certificado Olá permanece válido até a data de expiração.</span><span class="sxs-lookup"><span data-stu-id="e673e-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="e673e-112">Se você tiver configurado seu toouse de conta executar como automação um certificado emitido por sua autoridade de certificação corporativa e você usar essa opção, o certificado corporativo de saudação será substituído por um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="e673e-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="e673e-113">Olá toorenew do certificado, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e673e-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="e673e-114">No portal do Azure de Olá, abra conta de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e673e-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="e673e-115">Em Olá **conta de automação** folha em Olá **propriedades de conta** painel, em **configurações de conta**, selecione **contas executar como**.</span><span class="sxs-lookup"><span data-stu-id="e673e-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Painel de propriedades da conta de Automação](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="e673e-117">Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou Olá clássico conta executar como que você deseja toorenew Olá certificado para.</span><span class="sxs-lookup"><span data-stu-id="e673e-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="e673e-118">Em Olá **propriedades** folha para Olá selecionada conta, clique em **Renovar certificado**.</span><span class="sxs-lookup"><span data-stu-id="e673e-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Renovar o certificado da conta Executar como](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="e673e-120">Enquanto o certificado hello está sendo renovado, você pode acompanhar o progresso de saudação em **notificações** menu hello.</span><span class="sxs-lookup"><span data-stu-id="e673e-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="e673e-121">Excluir uma conta Executar como ou Executar como Clássica</span><span class="sxs-lookup"><span data-stu-id="e673e-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="e673e-122">Esta seção descreve como toodelete e crie novamente uma conta executar como ou clássico executar como.</span><span class="sxs-lookup"><span data-stu-id="e673e-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="e673e-123">Ao executar esta ação, Olá conta de automação é mantida.</span><span class="sxs-lookup"><span data-stu-id="e673e-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="e673e-124">Depois de excluir uma conta executar como ou clássico executar como, você poderá recriá-la em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e673e-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="e673e-125">No portal do Azure de Olá, abra conta de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e673e-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="e673e-126">Em Olá **conta de automação** folha, no painel de propriedades da conta hello, selecione **contas executar como**.</span><span class="sxs-lookup"><span data-stu-id="e673e-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="e673e-127">Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou clássico executar como da conta que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="e673e-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="e673e-128">Em seguida, na Olá **propriedades** folha para Olá selecionada conta, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="e673e-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Excluir Conta Executar como](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="e673e-130">Enquanto a conta de hello está sendo excluída, você pode acompanhar o progresso de saudação em **notificações** menu hello.</span><span class="sxs-lookup"><span data-stu-id="e673e-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="e673e-131">Após a exclusão de conta hello, você pode criá-lo novamente no hello **contas executar como** opção de criação de folha de propriedades selecionando Olá **Azure conta executar como**.</span><span class="sxs-lookup"><span data-stu-id="e673e-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Recriar Olá automação executar como conta](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="e673e-133">Configuração incorreta</span><span class="sxs-lookup"><span data-stu-id="e673e-133">Misconfiguration</span></span>
<span data-ttu-id="e673e-134">Alguns itens de configuração necessárias para toofunction de conta executar como ou clássico executar como Olá corretamente podem foram excluídos ou incorretamente criados durante a instalação inicial.</span><span class="sxs-lookup"><span data-stu-id="e673e-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="e673e-135">Olá itens incluem:</span><span class="sxs-lookup"><span data-stu-id="e673e-135">hello items include:</span></span>

* <span data-ttu-id="e673e-136">Ativo de certificado</span><span class="sxs-lookup"><span data-stu-id="e673e-136">Certificate asset</span></span>
* <span data-ttu-id="e673e-137">Ativo de conexão</span><span class="sxs-lookup"><span data-stu-id="e673e-137">Connection asset</span></span>
* <span data-ttu-id="e673e-138">Conta executar como foi removida da função de Colaborador Olá</span><span class="sxs-lookup"><span data-stu-id="e673e-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="e673e-139">Entidade de serviço ou aplicativo no Azure AD</span><span class="sxs-lookup"><span data-stu-id="e673e-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="e673e-140">Olá anterior e outras instâncias de uma configuração incorreta, Olá conta de automação detecta Olá altera e exibe o status de *incompleta* em Olá **contas executar como** folha de propriedades para Olá conta.</span><span class="sxs-lookup"><span data-stu-id="e673e-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Status incompleto de configuração de conta Executar como](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="e673e-142">Quando você selecionar a conta executar como do hello, Olá conta **propriedades** painel exibe o saudação a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="e673e-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Mensagem de aviso incompleto da configuração da conta Executar como](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="e673e-144">.</span><span class="sxs-lookup"><span data-stu-id="e673e-144">.</span></span>

<span data-ttu-id="e673e-145">Rapidamente, você pode resolver esses problemas de conta executar como, excluindo e recriando conta hello.</span><span class="sxs-lookup"><span data-stu-id="e673e-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e673e-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e673e-146">Next steps</span></span>
* <span data-ttu-id="e673e-147">Para obter mais informações sobre entidades de serviço, consulte muito[objetos Application e entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="e673e-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="e673e-148">Para obter mais informações sobre o controle de acesso baseado em função na automação do Azure, consulte muito[controle de acesso baseado em função no Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="e673e-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="e673e-149">Para obter mais informações sobre certificados e serviços do Azure, consulte muito[visão geral de certificados para serviços de nuvem do Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="e673e-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
