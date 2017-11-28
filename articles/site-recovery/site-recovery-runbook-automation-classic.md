---
title: "planos de toorecovery de runbooks de automação do Azure de aaaAdd no portal clássico Olá | Microsoft Docs"
description: "Este artigo descreve como recuperação de Site do Azure agora permite que você tooextend planos de recuperação usando tarefas complexas de toocomplete de automação do Azure durante a recuperação tooAzure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="641f2-103">Adicionar planos de toorecovery de runbooks de automação do Azure no portal clássico Olá</span><span class="sxs-lookup"><span data-stu-id="641f2-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="641f2-104">Este tutorial descreve como o Azure Site Recovery integra-se a automação do Azure tooprovide extensibilidade toorecovery planos.</span><span class="sxs-lookup"><span data-stu-id="641f2-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="641f2-105">Planos de recuperação podem coordenar a recuperação das máquinas virtuais protegidas usando o Azure Site Recovery para a nuvem de toosecondary de replicação e cenários de tooAzure de replicação.</span><span class="sxs-lookup"><span data-stu-id="641f2-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="641f2-106">Eles também ajudam a fazer a recuperação de saudação **precisas**, **repeatable**, e **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="641f2-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="641f2-107">Se você estiver realizando o failover tooAzure suas máquinas virtuais, integração com a automação do Azure estende os planos de recuperação e fornece funcionalidade tooexecute runbooks, permitindo assim que as tarefas de automação avançada.</span><span class="sxs-lookup"><span data-stu-id="641f2-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="641f2-108">Se você ainda não souber o que é a Automação do Azure, inscreva-se [aqui](https://azure.microsoft.com/services/automation/) e baixe os exemplos de script [aqui](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="641f2-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="641f2-109">Leia mais sobre [do Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) e como os planos de tooorchestrate tooAzure de recuperação com a recuperação de [aqui](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="641f2-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="641f2-110">Neste breve tutorial, veremos como você pode integrar os runbooks de automação do Azure aos planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="641f2-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="641f2-111">Vamos automatizar tarefas simples, que anteriormente necessária intervenção manual e veja como um múltiplo de tooconvert intervir recuperação uma ação de recuperação de único clique.</span><span class="sxs-lookup"><span data-stu-id="641f2-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="641f2-112">Também veremos como você pode solucionar problemas de um script simples, caso ocorra algum erro.</span><span class="sxs-lookup"><span data-stu-id="641f2-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="641f2-113">Proteger a saudação aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="641f2-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="641f2-114">Vamos começa com um aplicativo simples composto por duas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="641f2-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="641f2-115">Aqui, temos um aplicativo HRweb da Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="641f2-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="641f2-116">A Fabrikam de HRweb de front-end e Fabrikam-Hrweb-back-end são Olá duas VMs protegidas tooAzure usando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="641f2-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="641f2-117">tooprotect Olá VMs usando o Azure Site Recovery, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="641f2-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="641f2-118">Habilite a proteção para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="641f2-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="641f2-119">Verifique se as máquinas virtuais de saudação concluiu a replicação inicial e estiver replicando.</span><span class="sxs-lookup"><span data-stu-id="641f2-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="641f2-120">Aguarde até que Olá a replicação inicial for concluída e status de replicação de saudação diz protegidos.</span><span class="sxs-lookup"><span data-stu-id="641f2-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="641f2-121">Neste tutorial, vamos criar um plano de recuperação para Olá Fabrikam HRweb aplicativo toofailover Olá aplicativo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="641f2-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="641f2-122">Em seguida, integraremos-lo com um runbook que criará um ponto de extremidade em Olá failover da máquina virtual do Azure tooserve web páginas na porta 80.</span><span class="sxs-lookup"><span data-stu-id="641f2-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="641f2-123">Primeiro, vamos criar um plano de recuperação para nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="641f2-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="641f2-124">Criar plano de recuperação de saudação</span><span class="sxs-lookup"><span data-stu-id="641f2-124">Create hello recovery plan</span></span>
<span data-ttu-id="641f2-125">toorecover tooAzure de aplicativo hello, você precisa toocreate um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="641f2-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="641f2-126">Usando um plano de recuperação que você pode especificar a ordem de saudação da recuperação das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="641f2-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="641f2-127">máquina virtual de saudação colocada no grupo 1 será recuperar e inicie o primeiro e depois de máquina virtual de saudação no grupo 2.</span><span class="sxs-lookup"><span data-stu-id="641f2-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="641f2-128">Crie um Plano de recuperação parecido com o exibido abaixo.</span><span class="sxs-lookup"><span data-stu-id="641f2-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="641f2-129">mais informações sobre planos de recuperação, leia a documentação do tooread [aqui](https://msdn.microsoft.com/library/azure/dn788799.aspx "aqui").</span><span class="sxs-lookup"><span data-stu-id="641f2-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="641f2-130">Em seguida, vamos criar hello artefatos necessários na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="641f2-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="641f2-131">Criar conta de automação hello e seus ativos</span><span class="sxs-lookup"><span data-stu-id="641f2-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="641f2-132">É necessário um runbooks de toocreate de conta de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="641f2-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="641f2-133">Se você não tiver uma conta, navegar pelo guia de tooAzure de automação ![](media/site-recovery-runbook-automation/02.png)e criar uma nova conta.</span><span class="sxs-lookup"><span data-stu-id="641f2-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="641f2-134">Dar conta Olá tooidentify um nome com.</span><span class="sxs-lookup"><span data-stu-id="641f2-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="641f2-135">Especifique uma região geográfica onde deseja que a conta de saudação tooplace.</span><span class="sxs-lookup"><span data-stu-id="641f2-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="641f2-136">É recomendável tooplace conta Olá Olá mesma região do cofre Olá ASR.</span><span class="sxs-lookup"><span data-stu-id="641f2-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="641f2-137">Em seguida, crie Olá ativos em Olá conta a seguir.</span><span class="sxs-lookup"><span data-stu-id="641f2-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="641f2-138">Adicionar um nome de assinatura como ativo</span><span class="sxs-lookup"><span data-stu-id="641f2-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="641f2-139">Adicionar uma nova configuração ![](media/site-recovery-runbook-automation/04.png) em Olá ativos de automação do Azure e selecione muito![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="641f2-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="641f2-140">Selecione o tipo de variável hello como **cadeia de caracteres**</span><span class="sxs-lookup"><span data-stu-id="641f2-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="641f2-141">Especifique o nome da variável como **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="641f2-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="641f2-142">Especifique o nome real da assinatura do Azure como o valor da variável hello.</span><span class="sxs-lookup"><span data-stu-id="641f2-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="641f2-143">Você pode identificar o nome de saudação da sua assinatura na página de configurações de saudação da sua conta no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="641f2-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="641f2-144">Adicionar uma credencial de logon do Azure como ativo</span><span class="sxs-lookup"><span data-stu-id="641f2-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="641f2-145">Automação do Azure usa a assinatura do Azure PowerShell tooconnect toothe e opera em artefatos de saudação existe.</span><span class="sxs-lookup"><span data-stu-id="641f2-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="641f2-146">Para isso, você precisa autenticar usando sua conta da Microsoft ou uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="641f2-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="641f2-147">Você pode armazenar as credenciais de conta de saudação em um toobe ativo com segurança usado pelo runbook hello.</span><span class="sxs-lookup"><span data-stu-id="641f2-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="641f2-148">Adicionar uma nova configuração ![](media/site-recovery-runbook-automation/04.png) em Olá ativos de automação do Azure e selecione![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="641f2-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="641f2-149">Selecione o tipo de credencial hello como **credencial do Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="641f2-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="641f2-150">Especifique nome hello como **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="641f2-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="641f2-151">Especifica Olá nome de usuário e senha toosign-em com.</span><span class="sxs-lookup"><span data-stu-id="641f2-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="641f2-152">Agora, essas duas configurações estão disponíveis em seus ativos.</span><span class="sxs-lookup"><span data-stu-id="641f2-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="641f2-153">Para obter mais informações sobre como tooconnect tooyour assinatura por meio do PowerShell é fornecida [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="641f2-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="641f2-154">Em seguida, você criará um runbook na automação do Azure que pode adicionar um ponto de extremidade da máquina virtual front-end de saudação após o failover.</span><span class="sxs-lookup"><span data-stu-id="641f2-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="641f2-155">Contexto de automação do Azure</span><span class="sxs-lookup"><span data-stu-id="641f2-155">Azure automation context</span></span>
<span data-ttu-id="641f2-156">ASR passa um toohelp do contexto toohello variável runbook gravar scripts determinísticas.</span><span class="sxs-lookup"><span data-stu-id="641f2-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="641f2-157">Alguém poderia argumentar que nomes de saudação do hello serviço de nuvem e Olá Máquina Virtual são previsíveis, mas acontece que não é sempre caso Olá devido a cenários de toocertain como Olá um onde nome de saudação do nome da máquina virtual Olá pode ter sido alterado devido toounsupported caracteres no Azure.</span><span class="sxs-lookup"><span data-stu-id="641f2-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="641f2-158">Portanto, essas informações são passadas toohello ASR plano de recuperação como parte da saudação *contexto*.</span><span class="sxs-lookup"><span data-stu-id="641f2-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="641f2-159">Abaixo está um exemplo da aparência de variável de contexto de saudação.</span><span class="sxs-lookup"><span data-stu-id="641f2-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="641f2-160">tabela de saudação abaixo contém o nome e uma descrição para cada variável no contexto de saudação.</span><span class="sxs-lookup"><span data-stu-id="641f2-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="641f2-161">**Nome da variável**</span><span class="sxs-lookup"><span data-stu-id="641f2-161">**Variable name**</span></span> | <span data-ttu-id="641f2-162">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="641f2-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="641f2-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="641f2-163">RecoveryPlanName</span></span> |<span data-ttu-id="641f2-164">Nome do plano de execução.</span><span class="sxs-lookup"><span data-stu-id="641f2-164">Name of plan being run.</span></span> <span data-ttu-id="641f2-165">Ajuda a você tomar uma ação com base no nome usando Olá mesmo script</span><span class="sxs-lookup"><span data-stu-id="641f2-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="641f2-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="641f2-166">FailoverType</span></span> |<span data-ttu-id="641f2-167">Especifica se o failover Olá é testar, planejado ou não planejado.</span><span class="sxs-lookup"><span data-stu-id="641f2-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="641f2-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="641f2-168">FailoverDirection</span></span> |<span data-ttu-id="641f2-169">Especifique se a recuperação é tooprimary ou secundário</span><span class="sxs-lookup"><span data-stu-id="641f2-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="641f2-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="641f2-170">GroupID</span></span> |<span data-ttu-id="641f2-171">Identifique o número de grupo de saudação no plano de recuperação de saudação quando plano hello está em execução</span><span class="sxs-lookup"><span data-stu-id="641f2-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="641f2-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="641f2-172">VmMap</span></span> |<span data-ttu-id="641f2-173">Matriz de todas as máquinas virtuais de saudação no grupo de saudação</span><span class="sxs-lookup"><span data-stu-id="641f2-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="641f2-174">Chave VMMap</span><span class="sxs-lookup"><span data-stu-id="641f2-174">VMMap key</span></span> |<span data-ttu-id="641f2-175">Chave exclusiva (GUID) para cada VM.</span><span class="sxs-lookup"><span data-stu-id="641f2-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="641f2-176">Ele tem Olá mesmas Olá VMM ID da máquina virtual de saudação onde aplicável.</span><span class="sxs-lookup"><span data-stu-id="641f2-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="641f2-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="641f2-177">RoleName</span></span> |<span data-ttu-id="641f2-178">Nome da saudação VM do Azure que está sendo recuperado</span><span class="sxs-lookup"><span data-stu-id="641f2-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="641f2-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="641f2-179">CloudServiceName</span></span> |<span data-ttu-id="641f2-180">Nome do serviço de nuvem do Azure, sob o qual Olá máquina virtual é criada.</span><span class="sxs-lookup"><span data-stu-id="641f2-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="641f2-181">Olá tooidentify VmMap Key no contexto de saudação também poderia acesse a página de propriedades VM toohello em ASR e examinar Olá propriedade GUID da VM.</span><span class="sxs-lookup"><span data-stu-id="641f2-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="641f2-182">Criar um runbook de automação</span><span class="sxs-lookup"><span data-stu-id="641f2-182">Author an Automation runbook</span></span>
<span data-ttu-id="641f2-183">Agora crie Olá runbook tooopen a porta 80 em máquina virtual front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="641f2-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="641f2-184">Criar um novo runbook em Olá conta de automação do Azure com o nome da saudação **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="641f2-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="641f2-185">Navegue toohello exibição autor de runbook hello e entrar no modo de rascunho hello.</span><span class="sxs-lookup"><span data-stu-id="641f2-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="641f2-186">Primeiro, especifique toouse variável hello como contexto de plano de recuperação de saudação</span><span class="sxs-lookup"><span data-stu-id="641f2-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="641f2-187">Em seguida conectar toohello assinatura usando o nome de credencial e assinatura Olá</span><span class="sxs-lookup"><span data-stu-id="641f2-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="641f2-188">Observe que você usa hello Azure ativos – **AzureCredential** e **AzureSubscriptionName** aqui.</span><span class="sxs-lookup"><span data-stu-id="641f2-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="641f2-189">Agora especifique os detalhes do ponto de extremidade hello e Olá GUID da máquina virtual de saudação do qual você deseja que o ponto de extremidade de saudação tooexpose.</span><span class="sxs-lookup"><span data-stu-id="641f2-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="641f2-190">Na saudação casos front-end da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="641f2-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="641f2-191">Isso especifica hello protocolo de ponto de extremidade do Azure, porta local Olá VM e sua porta pública mapeada.</span><span class="sxs-lookup"><span data-stu-id="641f2-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="641f2-192">Essas variáveis são parâmetros exigidos pelo Olá comandos do Azure que adicionar tooVMs de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="641f2-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="641f2-193">Olá VMGUID mantém Olá GUID da máquina virtual de saudação que precisar toooperate.</span><span class="sxs-lookup"><span data-stu-id="641f2-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="641f2-194">script Hello agora extrair contexto Olá Olá fornecido GUID da VM e criar um ponto de extremidade na máquina virtual de saudação referenciada por ele.</span><span class="sxs-lookup"><span data-stu-id="641f2-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="641f2-195">Depois que isso for concluído, ocorrências publicar ![](media/site-recovery-runbook-automation/20.png) tooallow sua toobe de script disponível para execução.</span><span class="sxs-lookup"><span data-stu-id="641f2-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="641f2-196">script completo Olá é fornecido abaixo para sua referência</span><span class="sxs-lookup"><span data-stu-id="641f2-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="641f2-197">Adicionar um plano de recuperação Olá script toohello</span><span class="sxs-lookup"><span data-stu-id="641f2-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="641f2-198">Depois que o script hello estiver pronto, você pode adicionar toohello plano de recuperação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="641f2-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="641f2-199">No plano de recuperação de saudação que você criou, escolha tooadd um script após o grupo 2.</span><span class="sxs-lookup"><span data-stu-id="641f2-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="641f2-200">Especifique um nome de script.</span><span class="sxs-lookup"><span data-stu-id="641f2-200">Specify a script name.</span></span> <span data-ttu-id="641f2-201">Isso é apenas um nome amigável para este script para mostrar no plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="641f2-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="641f2-202">No script de tooAzure de failover hello – selecione o nome da conta de automação do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="641f2-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="641f2-203">No hello Runbooks do Azure, selecione Olá runbook criado por você.</span><span class="sxs-lookup"><span data-stu-id="641f2-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="641f2-204">Scripts do lado principal</span><span class="sxs-lookup"><span data-stu-id="641f2-204">Primary side scripts</span></span>
<span data-ttu-id="641f2-205">Quando você estiver executando um failover tooAzure, também é possível tooexecute scripts do lado primário.</span><span class="sxs-lookup"><span data-stu-id="641f2-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="641f2-206">Esses scripts serão executados no servidor do VMM Olá durante o failover.</span><span class="sxs-lookup"><span data-stu-id="641f2-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="641f2-207">Scripts do lado principal só ficam disponíveis para estágios pré-desligamento e pós-desligamento.</span><span class="sxs-lookup"><span data-stu-id="641f2-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="641f2-208">Isso ocorre porque espera-se que Olá site primário toobe normalmente não está disponível quando um desastre ocorrer.</span><span class="sxs-lookup"><span data-stu-id="641f2-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="641f2-209">Durante um failover não planejado, somente se você aceitar participar de operações do site primário, ele tentará scripts do toorun Olá lado primário.</span><span class="sxs-lookup"><span data-stu-id="641f2-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="641f2-210">Se eles não estão acessíveis ou tempo limite, o failover de saudação continuarão toorecover Olá máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="641f2-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="641f2-211">Scripts do lado primário estão não disponíveis para Sites VMware/físicos/Hyper-v sem tooAzure VMM protegido - ao tooAzure do failover.</span><span class="sxs-lookup"><span data-stu-id="641f2-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="641f2-212">No entanto, quando você failback de instalações do Azure tooon, scripts do lado primário (Runbooks) pode ser usado para todos os destinos, exceto o VMware.</span><span class="sxs-lookup"><span data-stu-id="641f2-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="641f2-213">Plano de recuperação de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="641f2-213">Test hello recovery plan</span></span>
<span data-ttu-id="641f2-214">Depois que você adicionou Olá runbook toohello plano, poderá iniciar um failover de teste e ver em ação.</span><span class="sxs-lookup"><span data-stu-id="641f2-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="641f2-215">É sempre recomendável toorun um tootest de failover de teste sua tooensure de plano de recuperação de aplicativos e Olá que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="641f2-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="641f2-216">Selecione o plano de recuperação de saudação e iniciar um failover de teste.</span><span class="sxs-lookup"><span data-stu-id="641f2-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="641f2-217">Durante a execução do plano de saudação, você pode ver se o runbook Olá foi executado ou não por meio de seu status.</span><span class="sxs-lookup"><span data-stu-id="641f2-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="641f2-218">Você também pode ver Olá detalhadas de status de execução de runbook na página de trabalhos de automação do Azure Olá Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="641f2-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="641f2-219">Após a conclusão do failover hello, além de resultado da execução do runbook Olá, você pode ver se Olá execução for bem-sucedida ou não visitar a página de máquina virtual do Azure hello e olhando para pontos de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="641f2-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="641f2-220">Exemplos de scripts</span><span class="sxs-lookup"><span data-stu-id="641f2-220">Sample scripts</span></span>
<span data-ttu-id="641f2-221">Enquanto percorremos automatizar um comumente usada tarefa de adicionar um ponto de extremidade tooan máquina virtual do Azure neste tutorial, você pode fazer um número de outras tarefas de automação avançada usando a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="641f2-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="641f2-222">A Microsoft e Olá comunidade de automação do Azure fornecem runbooks de exemplo que podem ajudá-lo a começar a criar suas próprias soluções e runbooks do utilitário, que você pode usar como blocos de construção para tarefas de automação maior.</span><span class="sxs-lookup"><span data-stu-id="641f2-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="641f2-223">Começar a usá-los na Galeria de saudação e criar planos de recuperação de um clique poderosa para seus aplicativos usando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="641f2-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="641f2-224">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="641f2-224">Additional Resources</span></span>
[<span data-ttu-id="641f2-225">Visão geral da Automação</span><span class="sxs-lookup"><span data-stu-id="641f2-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Visão geral da Automação")

[<span data-ttu-id="641f2-226">Exemplos de scripts da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="641f2-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Exemplos de scripts da Automação do Azure")
