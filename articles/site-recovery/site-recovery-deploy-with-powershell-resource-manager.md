---
title: Replicar VMs do Hyper-V com PowerShell e o Azure Resource Manager | Microsoft Docs
description: "Automatize a replicação de VMs do Hyper-V no Azure com o Azure Site Recovery usando o PowerShell e o Azure Resource Manager."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: dbd562b73b0caecd0feb993bd6fb796dddb0438c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="3b317-103">Replicar entre máquinas virtuais locais do Hyper-V e o Azure usando o PowerShell e o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3b317-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b317-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3b317-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="3b317-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3b317-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="3b317-106">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="3b317-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="3b317-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3b317-107">Overview</span></span>
<span data-ttu-id="3b317-108">O Azure Site Recovery contribui para sua estratégia de continuidade dos negócios e recuperação de desastre orquestrando a replicação, o failover e a recuperação de máquinas virtuais em diversos cenários de implantação.</span><span class="sxs-lookup"><span data-stu-id="3b317-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="3b317-109">Para obter uma lista completa de cenários de implantação, confira a [visão geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b317-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="3b317-110">O PowerShell no Azure é um módulo que fornece cmdlets para gerenciar o Azure por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b317-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="3b317-111">Ele pode trabalhar com dois tipos de módulos: o módulo do Perfil do Azure ou o módulo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b317-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="3b317-112">Os cmdlets do PowerShell da Recuperação de Site disponíveis com o Azure PowerShell para o Azure Resource Manager permitem que você proteja e recupere seus servidores no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="3b317-113">Este artigo descreve como usar o Windows PowerShell, juntamente com o Azure Resource Manager, na implantação da Recuperação de Site para configurar e orquestrar a proteção de servidor no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="3b317-114">O exemplo usado neste artigo mostra como proteger, executar failover e recuperar máquinas virtuais em um host Hyper-V no Azure usando o Azure PowerShell com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b317-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="3b317-115">Atualmente, os cmdlets do PowerShell da Recuperação de Site permitem configurar o seguinte: um site do Virtual Machine Manager em outro, um site do Virtual Machine Manager no Azure e um site do Hyper-V no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-115">The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.</span></span>
>
>

<span data-ttu-id="3b317-116">Não é preciso ser um especialista no PowerShell para usar este artigo, mas é necessário entender os conceitos básicos, como módulos, cmdlets e sessões.</span><span class="sxs-lookup"><span data-stu-id="3b317-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="3b317-117">Para obter mais informações sobre o Windows PowerShell, consulte [Introdução ao PowerShell do Microsoft Azure (a página pode estar em inglês)](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b317-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="3b317-118">Leia mais sobre isso em [Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3b317-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b317-119">Os parceiros da Microsoft que fazem parte do programa CSP (Provedor de Solução na Nuvem) podem configurar e gerenciar a proteção dos servidores de seus clientes em suas respectivas assinaturas de CSP dos clientes (assinaturas de locatário).</span><span class="sxs-lookup"><span data-stu-id="3b317-119">Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="3b317-120">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3b317-120">Before you start</span></span>
<span data-ttu-id="3b317-121">Verifique se estes pré-requisitos estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="3b317-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="3b317-122">Uma conta do [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="3b317-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="3b317-123">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b317-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="3b317-124">Além disso, você pode ler sobre [preços do Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="3b317-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="3b317-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="3b317-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="3b317-126">Para obter informações sobre essa versão e como instalá-la, confira [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="3b317-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="3b317-127">Os módulos [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/).</span><span class="sxs-lookup"><span data-stu-id="3b317-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="3b317-128">É possível obter as versões mais recentes desses módulos na [Galeria do PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="3b317-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="3b317-129">Este artigo ilustra como usar o Azure PowerShell com o Azure Resource Manager para configurar e gerenciar a proteção de seus servidores.</span><span class="sxs-lookup"><span data-stu-id="3b317-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="3b317-130">O exemplo usado neste artigo mostra como proteger uma máquina virtual, em execução em um host Hyper-V, no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="3b317-131">Os pré-requisitos a seguir são específicos a esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="3b317-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="3b317-132">Para obter um conjunto mais abrangente dos requisitos para os vários cenários da Recuperação de Site, consulte a documentação referente a um cenário específico.</span><span class="sxs-lookup"><span data-stu-id="3b317-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="3b317-133">Um host Hyper-V que executa o Windows Server 2012 R2 ou o Microsoft Hyper-V Server 2012 R2 contendo uma ou mais máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="3b317-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="3b317-134">Servidores Hyper-V conectados à Internet, diretamente ou por meio de um proxy.</span><span class="sxs-lookup"><span data-stu-id="3b317-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="3b317-135">As máquinas virtuais que você deseja proteger devem estar em conformidade com os [Pré-requisitos para Máquinas Virtuais](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="3b317-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="3b317-136">Etapa 1: Entrar em sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="3b317-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="3b317-137">Abra um console do PowerShell e execute este comando para entrar em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="3b317-138">O cmdlet abre uma página da Web que solicitará suas credenciais de conta.</span><span class="sxs-lookup"><span data-stu-id="3b317-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="3b317-139">Como alternativa, você também poderá incluir suas credenciais de conta como parâmetro para o cmdlet `Login-AzureRmAccount` usando o parâmetro `-Credential`.</span><span class="sxs-lookup"><span data-stu-id="3b317-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="3b317-140">Se você é um parceiro CSP trabalhando em nome de um locatário, especifique o cliente como um locatário usando sua tenantID ou o nome de domínio primário do locatário.</span><span class="sxs-lookup"><span data-stu-id="3b317-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="3b317-141">Uma conta pode ter várias assinaturas, de modo que você deverá associar à conta a assinatura que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="3b317-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="3b317-142">Verifique se sua assinatura está registrada para usar os provedores do Azure para os Serviços de Recuperação e o Site Recovery usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3b317-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="3b317-143">Na saída desses comandos, se o **RegistrationState** estiver definido como **Registrado**, você poderá seguir para a Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="3b317-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="3b317-144">Caso contrário, você deverá registrar o provedor ausente em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="3b317-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="3b317-145">Para registrar o provedor do Azure para a Recuperação de Site e os Serviços de Recuperação, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="3b317-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="3b317-146">Verifique se os provedores foram registrados com êxito usando os seguintes comandos: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="3b317-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="3b317-147">Etapa 2: configurar o cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="3b317-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="3b317-148">Crie um grupo de recursos do Azure Resource Manager no qual você criará o cofre ou use um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="3b317-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="3b317-149">Você pode criar um novo grupo de recursos usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3b317-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="3b317-150">em que a variável $ResourceGroupName contém o nome do grupo de recursos que você deseja criar e a variável $Geo contém a região do Azure na qual o grupo de recursos será criado (por exemplo, “Sul do Brasil”).</span><span class="sxs-lookup"><span data-stu-id="3b317-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="3b317-151">É possível obter uma lista de grupos de recursos em sua assinatura usando o cmdlet `Get-AzureRmResourceGroup` .</span><span class="sxs-lookup"><span data-stu-id="3b317-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="3b317-152">Crie um novo cofre dos Serviços de Recuperação do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="3b317-153">É possível recuperar uma lista de cofres existentes usando o cmdlet `Get-AzureRmRecoveryServicesVault`.</span><span class="sxs-lookup"><span data-stu-id="3b317-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="3b317-154">Se quiser executar operações nos cofres da Recuperação de Site criados usando o portal clássico ou o módulo do PowerShell do Gerenciamento de Serviços do Azure, você poderá recuperar uma lista de cofres desse tipo usando o cmdlet `Get-AzureRmSiteRecoveryVault`.</span><span class="sxs-lookup"><span data-stu-id="3b317-154">If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="3b317-155">É necessário criar um novo cofre dos Serviços de Recuperação para todas as novas operações.</span><span class="sxs-lookup"><span data-stu-id="3b317-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="3b317-156">Há suporte para os cofres da Recuperação de Site criados anteriormente, mas eles não têm os recursos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="3b317-156">The Site Recovery vaults you've created earlier are supported, but don't have the latest features.</span></span>
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="3b317-157">Etapa 3: Configurar o contexto do Cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="3b317-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="3b317-158">Defina o contexto de cofre executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3b317-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="3b317-159">Etapa 4: Criar um site do Hyper-V e gerar uma nova chave de registro do cofre para o site.</span><span class="sxs-lookup"><span data-stu-id="3b317-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="3b317-160">Crie um novo site do Hyper-V da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="3b317-161">Este cmdlet inicia um trabalho da Recuperação de Site para a criação do site e retorna um objeto de trabalho da Recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="3b317-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="3b317-162">Aguarde a conclusão do trabalho e verifique se ele foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="3b317-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="3b317-163">É possível recuperar o objeto de trabalho e verificar o status atual do trabalho usando o cmdlet Get-AzureRmSiteRecoveryJob.</span><span class="sxs-lookup"><span data-stu-id="3b317-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="3b317-164">Gere e baixe uma chave de registro para o site da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="3b317-165">Copie a chave baixada no host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3b317-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="3b317-166">Você precisa da chave para registrar o host Hyper-V no site.</span><span class="sxs-lookup"><span data-stu-id="3b317-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="3b317-167">Etapa 5: Instalar o provedor do Azure Site Recovery e o Agente dos Serviços de Recuperação do Azure no host Hyper-V</span><span class="sxs-lookup"><span data-stu-id="3b317-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="3b317-168">Baixe o instalador para obter a versão mais recente do provedor na [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="3b317-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="3b317-169">Execute o instalador no host Hyper-V e, ao final da instalação, siga para a etapa de registro.</span><span class="sxs-lookup"><span data-stu-id="3b317-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="3b317-170">Quando solicitado, forneça a chave de registro do site baixada e conclua o registro do host Hyper-V no site.</span><span class="sxs-lookup"><span data-stu-id="3b317-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="3b317-171">Verifique se o host Hyper-V foi registrado no site usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3b317-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="3b317-172">Etapa 6: Criar uma política de replicação e associá-la ao contêiner de proteção</span><span class="sxs-lookup"><span data-stu-id="3b317-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="3b317-173">Crie uma política de replicação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="3b317-174">Verifique o trabalho retornado para garantir que a criação da política de replicação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="3b317-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3b317-175">A conta de armazenamento especificada deve estar na mesma região do Azure que o cofre dos Serviços de Recuperação e deve ter a replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="3b317-175">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="3b317-176">Se a conta de armazenamento de Recuperação especificada for do tipo Armazenamento do Azure (Clássico), o failover dos computadores protegidos recuperará o computador no Azure IaaS (Clássico).</span><span class="sxs-lookup"><span data-stu-id="3b317-176">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="3b317-177">Se a conta de armazenamento de Recuperação especificada for do tipo Armazenamento do Azure (Azure Resource Manager), o failover dos computadores protegidos recuperará o computador no Azure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3b317-177">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="3b317-178">Obtenha o contêiner de proteção corresponde ao site da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="3b317-179">Inicie a associação do contêiner de proteção à política de replicação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="3b317-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="3b317-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="3b317-181">Aguarde a conclusão do trabalho de associação e certifique-se de que ele foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="3b317-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="3b317-182">Etapa 7: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="3b317-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="3b317-183">Obtenha a entidade de proteção correspondente à VM que você deseja proteger, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="3b317-184">Inicie a proteção da máquina virtual, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="3b317-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="3b317-185">A conta de armazenamento especificada deve estar na mesma região do Azure que o cofre dos Serviços de Recuperação e deve ter a replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="3b317-185">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="3b317-186">Se a conta de armazenamento de Recuperação especificada for do tipo Armazenamento do Azure (Clássico), o failover dos computadores protegidos recuperará o computador no Azure IaaS (Clássico).</span><span class="sxs-lookup"><span data-stu-id="3b317-186">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="3b317-187">Se a conta de armazenamento de Recuperação especificada for do tipo Armazenamento do Azure (Azure Resource Manager), o failover dos computadores protegidos recuperará o computador no Azure IaaS (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3b317-187">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="3b317-188">Se a VM que você estiver protegendo tiver mais de um disco anexado, será necessário especificar o disco do sistema operacional usando o parâmetro *OSDiskName* .</span><span class="sxs-lookup"><span data-stu-id="3b317-188">If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="3b317-189">Aguarde até que as máquinas virtuais atinjam um estado protegido após a replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="3b317-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="3b317-190">Isso pode demorar um pouco, dependendo de fatores como a quantidade de dados a serem replicados e a largura de banda upstream disponível no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="3b317-191">O State e StateDescription do trabalho são atualizados da seguinte maneira, depois que a VM atingir um estado protegido.</span><span class="sxs-lookup"><span data-stu-id="3b317-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="3b317-192">Atualize propriedades de recuperação, como o tamanho da função VM, e a rede do Azure que será usada para anexar placas de interface de rede da máquina virtual após o failover.</span><span class="sxs-lookup"><span data-stu-id="3b317-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update the virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="3b317-193">Etapa 8: executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="3b317-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="3b317-194">Execute um trabalho de failover de teste, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="3b317-195">Verifique se a VM de teste foi criada no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="3b317-196">(O trabalho de failover de teste é suspenso após a criação da VM de teste no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b317-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="3b317-197">O trabalho será concluído com a limpeza dos artefatos criados ao retomar o trabalho, conforme ilustrado na próxima etapa.)</span><span class="sxs-lookup"><span data-stu-id="3b317-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="3b317-198">Conclua o failover de teste da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b317-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="3b317-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b317-199">Next Steps</span></span>
<span data-ttu-id="3b317-200">[Leia mais](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b317-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
