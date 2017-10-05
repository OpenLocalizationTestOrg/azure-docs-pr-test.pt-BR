---
title: "Adicionar runbooks de automação do Azure aos planos de recuperação no Portal Clássico | Microsoft Docs"
description: "Este artigo descreve como o Azure Site Recovery permite a ampliação dos planos de recuperação usando a Automação do Azure para concluir tarefas complexas durante a recuperação para o Azure"
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
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="7a555-103">Adicionar runbooks de automação do Azure aos planos de recuperação no Portal Clássico</span><span class="sxs-lookup"><span data-stu-id="7a555-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="7a555-104">Este tutorial descreve como o Azure Site Recovery é integrado à Automação do Azure para fornecer extensibilidade aos planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7a555-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="7a555-105">Os planos de recuperação podem coordenar a recuperação de máquinas virtuais protegidas usando o Azure Site Recovery para cenários de replicação na nuvem secundária e replicação no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="7a555-106">Eles também ajudam a tornar a recuperação **precisa de forma consistente**, **reproduzível** e **automatizada**.</span><span class="sxs-lookup"><span data-stu-id="7a555-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="7a555-107">Se você estiver realizando o failover de suas máquinas virtuais para o Azure, a integração com a Automação do Azure estende os planos de recuperação e oferece a capacidade de executar runbooks, possibilitando tarefas avançadas de automação.</span><span class="sxs-lookup"><span data-stu-id="7a555-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="7a555-108">Se você ainda não souber o que é a Automação do Azure, inscreva-se [aqui](https://azure.microsoft.com/services/automation/) e baixe os exemplos de script [aqui](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="7a555-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="7a555-109">Leia mais sobre o [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) e como coordenar a recuperação no Azure usando o planos de recuperação [aqui](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="7a555-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="7a555-110">Neste breve tutorial, veremos como você pode integrar os runbooks de automação do Azure aos planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7a555-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="7a555-111">Automatizaremos tarefas simples que exigiam uma intervenção manual e veremos como converter uma recuperação com várias etapa em uma ação de recuperação de clique único.</span><span class="sxs-lookup"><span data-stu-id="7a555-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="7a555-112">Também veremos como você pode solucionar problemas de um script simples, caso ocorra algum erro.</span><span class="sxs-lookup"><span data-stu-id="7a555-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="7a555-113">Proteger o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="7a555-113">Protect the application to Azure</span></span>
<span data-ttu-id="7a555-114">Vamos começa com um aplicativo simples composto por duas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7a555-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="7a555-115">Aqui, temos um aplicativo HRweb da Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="7a555-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="7a555-116">Fabrikam-HRweb-frontend e Fabrikam-Hrweb-backend são duas máquinas virtuais protegidas no Azure usando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7a555-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="7a555-117">Para proteger as máquinas virtuais com o Azure Site Recovery, execute as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="7a555-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="7a555-118">Habilite a proteção para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7a555-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="7a555-119">Verifique se as máquinas virtuais concluíram a replicação inicial e se estão replicando.</span><span class="sxs-lookup"><span data-stu-id="7a555-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="7a555-120">Aguarde até a conclusão da replicação inicial e o status de Replicação indicar Protegido.</span><span class="sxs-lookup"><span data-stu-id="7a555-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="7a555-121">Neste tutorial, criaremos um plano de recuperação para o aplicativo Fabrikam HRweb, a fim de realizar o failover do aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="7a555-122">Em seguida, realizaremos uma integração com um runbook que criará um ponto de extremidade na máquina virtual do Azure em estado de failover para servir páginas da Web na porta 80.</span><span class="sxs-lookup"><span data-stu-id="7a555-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="7a555-123">Primeiro, vamos criar um plano de recuperação para nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7a555-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="7a555-124">Criar o plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="7a555-124">Create the recovery plan</span></span>
<span data-ttu-id="7a555-125">Para recuperar o aplicativo no Azure, você precisa criar um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7a555-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="7a555-126">Com um plano de recuperação, você pode especificar a ordem de recuperação das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7a555-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="7a555-127">A máquina virtual colocada no grupo 1 será recuperada e iniciada primeiro, em seguida, a máquina virtual no grupo 2.</span><span class="sxs-lookup"><span data-stu-id="7a555-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="7a555-128">Crie um Plano de recuperação parecido com o exibido abaixo.</span><span class="sxs-lookup"><span data-stu-id="7a555-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="7a555-129">Para ler mais sobre os planos de recuperação, leia a documentação contida [aqui](https://msdn.microsoft.com/library/azure/dn788799.aspx "aqui").</span><span class="sxs-lookup"><span data-stu-id="7a555-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="7a555-130">Em seguida, vamos criar os artefatos necessários na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="7a555-131">Criar a conta de automação e seus ativos</span><span class="sxs-lookup"><span data-stu-id="7a555-131">Create the automation account and its assets</span></span>
<span data-ttu-id="7a555-132">Você precisa de uma conta de Automação do Azure para criar runbooks.</span><span class="sxs-lookup"><span data-stu-id="7a555-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="7a555-133">Se você ainda não tiver uma conta, navegue até a guia Automação do Azure indicada por ![](media/site-recovery-runbook-automation/02.png)e crie uma nova conta.</span><span class="sxs-lookup"><span data-stu-id="7a555-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="7a555-134">Dê um nome à conta para identificá-la.</span><span class="sxs-lookup"><span data-stu-id="7a555-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="7a555-135">Especifique uma região geográfica na qual você deseja colocar a conta.</span><span class="sxs-lookup"><span data-stu-id="7a555-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="7a555-136">É recomendável colocar a conta na mesma região que o cofre ASR.</span><span class="sxs-lookup"><span data-stu-id="7a555-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="7a555-137">Em seguida, crie os seguintes ativos na Conta.</span><span class="sxs-lookup"><span data-stu-id="7a555-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="7a555-138">Adicionar um nome de assinatura como ativo</span><span class="sxs-lookup"><span data-stu-id="7a555-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="7a555-139">Adicione uma nova configuração ![](media/site-recovery-runbook-automation/04.png) nos Ativos de Automação do Azure e selecione ![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="7a555-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="7a555-140">Selecione o tipo de variável como **String**</span><span class="sxs-lookup"><span data-stu-id="7a555-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="7a555-141">Especifique o nome da variável como **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="7a555-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="7a555-142">Especifique o nome real de sua Assinatura do Azure como o valor da variável.</span><span class="sxs-lookup"><span data-stu-id="7a555-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="7a555-143">Você pode identificar o nome de sua assinatura na página Configurações de sua conta no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="7a555-144">Adicionar uma credencial de logon do Azure como ativo</span><span class="sxs-lookup"><span data-stu-id="7a555-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="7a555-145">A Automação do Azure usa o Azure PowerShell para se conectar à assinatura e opera nos artefatos de lá.</span><span class="sxs-lookup"><span data-stu-id="7a555-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="7a555-146">Para isso, você precisa autenticar usando sua conta da Microsoft ou uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="7a555-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="7a555-147">Você pode armazenar as credenciais da conta em um ativo que será usado com segurança pelo runbook.</span><span class="sxs-lookup"><span data-stu-id="7a555-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="7a555-148">Adicione uma nova configuração ![](media/site-recovery-runbook-automation/04.png) nos Ativos de Automação do Azure e selecione ![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="7a555-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="7a555-149">Selecione o Tipo de credencial como **Credencial do Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="7a555-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="7a555-150">Especifique o nome como **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="7a555-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="7a555-151">Especifique o nome de usuário e a senha para logon.</span><span class="sxs-lookup"><span data-stu-id="7a555-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="7a555-152">Agora, essas duas configurações estão disponíveis em seus ativos.</span><span class="sxs-lookup"><span data-stu-id="7a555-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="7a555-153">Para saber mais sobre como se conectar à sua assinatura por meio do PowerShell clique [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a555-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="7a555-154">Em seguida, você criará um runbook na Automação do Azure que pode adicionar um ponto de extremidade à máquina virtual front-end após o failover.</span><span class="sxs-lookup"><span data-stu-id="7a555-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="7a555-155">Contexto de automação do Azure</span><span class="sxs-lookup"><span data-stu-id="7a555-155">Azure automation context</span></span>
<span data-ttu-id="7a555-156">ASR passa uma variável de contexto para o runbook a fim de ajudar você a escrever scripts deterministas.</span><span class="sxs-lookup"><span data-stu-id="7a555-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="7a555-157">Alguém poderia argumentar que os nomes do Serviço de nuvem e da Máquina virtual são previsíveis, mas nem sempre esse é o caso devido a certos cenários, por exemplo, aquele no qual o nome da máquina virtual pode ter sido alterado devido a caracteres sem suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="7a555-158">Portanto, essas informações são passadas ao plano de recuperação ASR como parte do *contexto*.</span><span class="sxs-lookup"><span data-stu-id="7a555-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="7a555-159">Veja abaixo um exemplo da aparência da variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="7a555-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="7a555-160">A tabela a seguir contém o nome e uma descrição para cada variável no contexto.</span><span class="sxs-lookup"><span data-stu-id="7a555-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="7a555-161">**Nome da variável**</span><span class="sxs-lookup"><span data-stu-id="7a555-161">**Variable name**</span></span> | <span data-ttu-id="7a555-162">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="7a555-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="7a555-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="7a555-163">RecoveryPlanName</span></span> |<span data-ttu-id="7a555-164">Nome do plano de execução.</span><span class="sxs-lookup"><span data-stu-id="7a555-164">Name of plan being run.</span></span> <span data-ttu-id="7a555-165">Ajuda você a agir com base no nome usando o mesmo script</span><span class="sxs-lookup"><span data-stu-id="7a555-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="7a555-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="7a555-166">FailoverType</span></span> |<span data-ttu-id="7a555-167">Especifica se o failover é de teste, planejado ou não planejado.</span><span class="sxs-lookup"><span data-stu-id="7a555-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="7a555-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="7a555-168">FailoverDirection</span></span> |<span data-ttu-id="7a555-169">Especifica se a recuperação é para o principal ou secundário</span><span class="sxs-lookup"><span data-stu-id="7a555-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="7a555-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="7a555-170">GroupID</span></span> |<span data-ttu-id="7a555-171">Identifica o número de grupo no plano de recuperação quando o plano está em execução</span><span class="sxs-lookup"><span data-stu-id="7a555-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="7a555-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="7a555-172">VmMap</span></span> |<span data-ttu-id="7a555-173">Matriz de todas as máquinas virtuais do grupo</span><span class="sxs-lookup"><span data-stu-id="7a555-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="7a555-174">Chave VMMap</span><span class="sxs-lookup"><span data-stu-id="7a555-174">VMMap key</span></span> |<span data-ttu-id="7a555-175">Chave exclusiva (GUID) para cada VM.</span><span class="sxs-lookup"><span data-stu-id="7a555-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="7a555-176">É igual à ID do VMM da máquina virtual onde aplicável.</span><span class="sxs-lookup"><span data-stu-id="7a555-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="7a555-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="7a555-177">RoleName</span></span> |<span data-ttu-id="7a555-178">Nome da VM do Azure que está sendo recuperada</span><span class="sxs-lookup"><span data-stu-id="7a555-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="7a555-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="7a555-179">CloudServiceName</span></span> |<span data-ttu-id="7a555-180">Nome do serviço de nuvem do Azure sob o qual a máquina virtual é criada.</span><span class="sxs-lookup"><span data-stu-id="7a555-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="7a555-181">Para identificar a Chave de VmMap no contexto, também é possível acessar a página de propriedades da VM no ASR e examinar a propriedade VM GUID.</span><span class="sxs-lookup"><span data-stu-id="7a555-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="7a555-182">Criar um runbook de automação</span><span class="sxs-lookup"><span data-stu-id="7a555-182">Author an Automation runbook</span></span>
<span data-ttu-id="7a555-183">Agora, crie o runbook para abrir a porta 80 na máquina virtual front-end.</span><span class="sxs-lookup"><span data-stu-id="7a555-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="7a555-184">Crie um novo runbook na conta de Automação do Azure com o nome **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="7a555-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="7a555-185">Navegue até o modo de exibição de Criação do runbook e entre no modo de rascunho.</span><span class="sxs-lookup"><span data-stu-id="7a555-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="7a555-186">Primeiro, especifique a variável a ser usada como o contexto do plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="7a555-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="7a555-187">Em seguida, conecte-se à assinatura usando o nome da credencial e da assinatura</span><span class="sxs-lookup"><span data-stu-id="7a555-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="7a555-188">Observe que você usa aqui os ativos do Azure – **AzureCredential** e **AzureSubscriptionName**.</span><span class="sxs-lookup"><span data-stu-id="7a555-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="7a555-189">Agora, especifique os detalhes do ponto de extremidade e o GUID da máquina virtual para a qual você deseja expor o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7a555-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="7a555-190">Neste caso, a máquina virtual de front-end.</span><span class="sxs-lookup"><span data-stu-id="7a555-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="7a555-191">Isso especifica o protocolo do ponto de extremidade do Azure, a porta local na VM e sua porta pública mapeada.</span><span class="sxs-lookup"><span data-stu-id="7a555-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="7a555-192">Essas variáveis são parâmetros exigidos pelos comandos do Azure que adicionam pontos de extremidade às máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7a555-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="7a555-193">O VMGUID contém o GUID da máquina virtual na qual você precisa operar.</span><span class="sxs-lookup"><span data-stu-id="7a555-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="7a555-194">Agora, o script extrairá o contexto do VM GUID determinado e criará um ponto de extremidade na máquina virtual indicada por ele.</span><span class="sxs-lookup"><span data-stu-id="7a555-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="7a555-195">Quando isso for concluído, pressione Publicar ![](media/site-recovery-runbook-automation/20.png) para permitir que seu script esteja disponível para execução.</span><span class="sxs-lookup"><span data-stu-id="7a555-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="7a555-196">O script completo é fornecido abaixo para sua referência</span><span class="sxs-lookup"><span data-stu-id="7a555-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="7a555-197">Adicione o script ao plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="7a555-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="7a555-198">Quando o script estiver pronto, você poderá adicioná-lo ao plano de recuperação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7a555-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="7a555-199">No plano de recuperação que você criou, escolha adicionar um script após o grupo 2.</span><span class="sxs-lookup"><span data-stu-id="7a555-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="7a555-200">Especifique um nome de script.</span><span class="sxs-lookup"><span data-stu-id="7a555-200">Specify a script name.</span></span> <span data-ttu-id="7a555-201">Esse é apenas um nome amigável para mostrar o script no Plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7a555-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="7a555-202">No script do failover para o Azure – Selecione o nome da Conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="7a555-203">Nos Runbooks do Azure, selecione o runbook criado por você.</span><span class="sxs-lookup"><span data-stu-id="7a555-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="7a555-204">Scripts do lado principal</span><span class="sxs-lookup"><span data-stu-id="7a555-204">Primary side scripts</span></span>
<span data-ttu-id="7a555-205">Quando você estiver executando um failover para o Azure, também poderá optar por executar scripts do lado principal.</span><span class="sxs-lookup"><span data-stu-id="7a555-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="7a555-206">Esses scripts serão executados no servidor VMM durante o failover.</span><span class="sxs-lookup"><span data-stu-id="7a555-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="7a555-207">Scripts do lado principal só ficam disponíveis para estágios pré-desligamento e pós-desligamento.</span><span class="sxs-lookup"><span data-stu-id="7a555-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="7a555-208">Isso ocorre porque esperamos que o site principal fique normalmente indisponível quando ocorre um desastre.</span><span class="sxs-lookup"><span data-stu-id="7a555-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="7a555-209">Durante um failover não planejado, apenas se você optar por operações de site principal, ele tentará executar os scripts do lado principal.</span><span class="sxs-lookup"><span data-stu-id="7a555-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="7a555-210">Se não for possível acessá-los ou tempo limite esgotar, o failover continuará a recuperar as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7a555-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="7a555-211">Scripts do lado principal não estão disponíveis para sites de VMware/físico/Hyper-v sem o VMM protegido para o Azure - durante o failover para o Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="7a555-212">No entanto, quando você realiza o failback do Azure para o local, os scripts do lado principal (Runbooks) podem ser usados em todos os destinos, exceto no VMware.</span><span class="sxs-lookup"><span data-stu-id="7a555-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="7a555-213">Testar o plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="7a555-213">Test the recovery plan</span></span>
<span data-ttu-id="7a555-214">Após adicionar o runbook ao plano, você poderá iniciar um failover de teste e vê-lo em ação.</span><span class="sxs-lookup"><span data-stu-id="7a555-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="7a555-215">É sempre recomendável executar um failover de teste para testar seu aplicativo e o plano de recuperação a fim de garantir que não exista erros.</span><span class="sxs-lookup"><span data-stu-id="7a555-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="7a555-216">Selecione o plano de recuperação e inicie um failover de teste.</span><span class="sxs-lookup"><span data-stu-id="7a555-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="7a555-217">Durante a execução do plano, você pode ver se o runbook foi executado ou não por meio do status.</span><span class="sxs-lookup"><span data-stu-id="7a555-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="7a555-218">Você também pode ver o status detalhado de execução do runbook na página de trabalhos da Automação do Azure para o runbook.</span><span class="sxs-lookup"><span data-stu-id="7a555-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="7a555-219">Após a conclusão do failover, exceto o resultado da execução do runbook, você poderá ver se a execução foi bem-sucedida ou não, visitando a página da máquina virtual do Azure e observando os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7a555-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="7a555-220">Exemplos de scripts</span><span class="sxs-lookup"><span data-stu-id="7a555-220">Sample scripts</span></span>
<span data-ttu-id="7a555-221">Embora tenhamos mostrado neste tutorial como automatizar uma tarefa usada normalmente, a adição de um ponto de extremidade a uma máquina virtual do Azure, você pode fazer várias outras tarefas avançadas de automação usando a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a555-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="7a555-222">A Microsoft e a comunidade da Automação do Azure fornecem exemplos de runbooks que podem ajudar você a começar a criar suas próprias soluções, e de runbooks utilitários, que você pode usar como blocos de construção para tarefas maiores de automação.</span><span class="sxs-lookup"><span data-stu-id="7a555-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="7a555-223">Comece a usá-los na galeria e crie planos de recuperação avançados e realizados com um único clique para seus aplicativos usando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7a555-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a555-224">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7a555-224">Additional Resources</span></span>
[<span data-ttu-id="7a555-225">Visão geral da Automação</span><span class="sxs-lookup"><span data-stu-id="7a555-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Visão geral da Automação")

[<span data-ttu-id="7a555-226">Exemplos de scripts da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="7a555-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Exemplos de scripts da Automação do Azure")
